Let's create comprehensive JUnit test cases for the `ProductRelationshipValidator` class. We'll need to mock its dependencies and test various scenarios including successful validations, missing relationships, quota product field mismatches, and error cases.

Here's the test class:

```java
package com.bnymellon.tsg.marketplace.validate;

import com.bnymellon.tsg.marketplace.catalog.types.ProductRelationship;
import com.bnymellon.tsg.marketplace.catalog.types.SelfServiceProductField;
import com.bnymellon.tsg.marketplace.model.ProductBundleDirectory;
import com.bnymellon.tsg.marketplace.model.ProductDirectory;
import com.bnymellon.tsg.marketplace.model.ProductID;
import com.bnymellon.tsg.snowclient.model.SelfServiceProduct;
import com.fasterxml.jackson.databind.ObjectMapper;
import org.eclipse.collections.impl.list.mutable.FastList;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.Mockito;

import java.util.*;
import java.util.function.BiFunction;

import static org.junit.jupiter.api.Assertions.*;
import static org.mockito.ArgumentMatchers.any;
import static org.mockito.Mockito.*;

class ProductRelationshipValidatorTest {

    private ProductRelationshipValidator validator;
    private ObjectMapper mapper;
    @SuppressWarnings("unchecked")
    private BiFunction<ProductRelationship, ProductBundleDirectory, SelfServiceProduct> productRelationshipLookup =
            mock(BiFunction.class);
    private ProductBundleDirectory productBundleDirectory;

    @BeforeEach
    void setUp() {
        mapper = new ObjectMapper();
        productBundleDirectory = mock(ProductBundleDirectory.class);
        validator = new ProductRelationshipValidator(mapper, productRelationshipLookup);
        reset(productRelationshipLookup, productBundleDirectory);
    }

    @Test
    void testNoRelationships() {
        // Arrange
        ProductDirectory productDir = mock(ProductDirectory.class);
        when(productDir.getProductDefinition(any())).thenReturn(null);
        when(productBundleDirectory.getGroups()).thenReturn(FastList.newListWith(
                mockProductGroupDirectory(productDir)));
        when(productBundleDirectory.getAllProductsInBundle()).thenReturn(new ArrayList<>());

        // Act
        List<ProductValidationMessage> result = validator.validate(productBundleDirectory);

        // Assert
        assertTrue(result.isEmpty());
        verify(productRelationshipLookup, never()).apply(any(), any());
    }

    @Test
    void testValidRelationship() {
        // Arrange
        ProductDirectory productDir = mock(ProductDirectory.class);
        Map<String, ProductRelationship> relationships = new HashMap<>();
        ProductRelationship relationship = new ProductRelationship();
        relationship.setProductName("relatedProduct");
        relationships.put("depends", relationship);
        
        SelfServiceProduct relatedProduct = new SelfServiceProduct();
        ProductDefinition productDef = mock(ProductDefinition.class);
        when(productDef.getRelationships()).thenReturn(relationships);
        when(productDef.getFields()).thenReturn(new HashMap<>());
        when(productDir.getProductDefinition(mapper)).thenReturn(productDef);
        
        when(productRelationshipLookup.apply(relationship, productBundleDirectory))
                .thenReturn(relatedProduct);
        
        when(productBundleDirectory.getGroups()).thenReturn(FastList.newListWith(
                mockProductGroupDirectory(productDir)));
        when(productBundleDirectory.getAllProductsInBundle()).thenReturn(new ArrayList<>());

        // Act
        List<ProductValidationMessage> result = validator.validate(productBundleDirectory);

        // Assert
        assertTrue(result.isEmpty());
        verify(productRelationshipLookup).apply(relationship, productBundleDirectory);
    }

    @Test
    void testMissingRelationship() {
        // Arrange
        ProductDirectory productDir = mock(ProductDirectory.class);
        Map<String, ProductRelationship> relationships = new HashMap<>();
        ProductRelationship relationship = new ProductRelationship();
        relationship.setProductName("missingProduct");
        relationship.setProductVersion("1.0");
        relationships.put("depends", relationship);
        
        ProductDefinition productDef = mock(ProductDefinition.class);
        when(productDef.getRelationships()).thenReturn(relationships);
        when(productDef.getFields()).thenReturn(new HashMap<>());
        when(productDir.getProductDefinition(mapper)).thenReturn(productDef);
        
        when(productRelationshipLookup.apply(relationship, productBundleDirectory))
                .thenReturn(null);
        
        when(productBundleDirectory.getGroups()).thenReturn(FastList.newListWith(
                mockProductGroupDirectory(productDir)));
        when(productBundleDirectory.getAllProductsInBundle()).thenReturn(new ArrayList<>());

        // Act
        List<ProductValidationMessage> result = validator.validate(productBundleDirectory);

        // Assert
        assertEquals(1, result.size());
        ProductValidationMessage msg = result.get(0);
        assertEquals("missingProduct", msg.getValidationTarget());
        assertEquals("Could not find product with product name missingProduct and product version 1.0 in catalog or published bundle",
                msg.getMessage());
        assertEquals(ValidationSeverity.ERROR, msg.getSeverity());
    }

    @Test
    void testQuotaRelationshipWithMissingFields() {
        // Arrange
        ProductDirectory productDir = mock(ProductDirectory.class);
        Map<String, ProductRelationship> relationships = new HashMap<>();
        ProductRelationship quotaRelationship = new ProductRelationship();
        quotaRelationship.setProductName("quotaProduct");
        relationships.put("quota", quotaRelationship);
        
        ProductDefinition productDef = mock(ProductDefinition.class);
        when(productDef.getProductName()).thenReturn("mainProduct");
        when(productDef.getRelationships()).thenReturn(relationships);
        
        Map<String, SelfServiceProductField> mainFields = new HashMap<>();
        when(productDef.getFields()).thenReturn(mainFields);
        
        when(productDir.getProductDefinition(mapper)).thenReturn(productDef);
        
        SelfServiceProduct quotaProduct = new SelfServiceProduct();
        Map<String, SelfServiceProductField> quotaFields = new HashMap<>();
        SelfServiceProductField quotaField = mock(SelfServiceProductField.class);
        quotaFields.put("extraField", quotaField);
        when(quotaProduct.getFields()).thenReturn(quotaFields);
        
        when(productRelationshipLookup.apply(quotaRelationship, productBundleDirectory))
                .thenReturn(quotaProduct);
        
        when(productBundleDirectory.getGroups()).thenReturn(FastList.newListWith(
                mockProductGroupDirectory(productDir)));
        when(productBundleDirectory.getAllProductsInBundle()).thenReturn(new ArrayList<>());

        // Act
        List<ProductValidationMessage> result = validator.validate(productBundleDirectory);

        // Assert
        assertEquals(1, result.size());
        ProductValidationMessage msg = result.get(0);
        assertEquals("Invalid Quota Product Fields", msg.getValidationTarget());
        assertTrue(msg.getMessage().contains("MainProductName=mainProduct"));
        assertTrue(msg.getMessage().contains("QuotaProductName=quotaProduct"));
        assertTrue(msg.getMessage().contains("FieldsMissingInMainProduct=[extraField]"));
        assertTrue(msg.getMessage().contains("FieldsDifferingInSchema=[]"));
        assertEquals(ValidationSeverity.ERROR, msg.getSeverity());
    }

    @Test
    void testQuotaRelationshipWithDifferingSchema() {
        // Arrange
        ProductDirectory productDir = mock(ProductDirectory.class);
        Map<String, ProductRelationship> relationships = new HashMap<>();
        ProductRelationship quotaRelationship = new ProductRelationship();
        quotaRelationship.setProductName("quotaProduct");
        relationships.put("quota", quotaRelationship);
        
        ProductDefinition productDef = mock(ProductDefinition.class);
        when(productDef.getProductName()).thenReturn("mainProduct");
        when(productDef.getRelationships()).thenReturn(relationships);
        
        Map<String, SelfServiceProductField> mainFields = new HashMap<>();
        SelfServiceProductField mainField = mock(SelfServiceProductField.class);
        mainFields.put("sharedField", mainField);
        when(productDef.getFields()).thenReturn(mainFields);
        
        when(productDir.getProductDefinition(mapper)).thenReturn(productDef);
        
        SelfServiceProduct quotaProduct = new SelfServiceProduct();
        Map<String, SelfServiceProductField> quotaFields = new HashMap<>();
        SelfServiceProductField quotaField = mock(SelfServiceProductField.class);
        when(quotaField.hasSameSchema(mainField)).thenReturn(false);
        quotaFields.put("sharedField", quotaField);
        when(quotaProduct.getFields()).thenReturn(quotaFields);
        
        when(productRelationshipLookup.apply(quotaRelationship, productBundleDirectory))
                .thenReturn(quotaProduct);
        
        when(productBundleDirectory.getGroups()).thenReturn(FastList.newListWith(
                mockProductGroupDirectory(productDir)));
        when(productBundleDirectory.getAllProductsInBundle()).thenReturn(new ArrayList<>());

        // Act
        List<ProductValidationMessage> result = validator.validate(productBundleDirectory);

        // Assert
        assertEquals(1, result.size());
        ProductValidationMessage msg = result.get(0);
        assertEquals("Invalid Quota Product Fields", msg.getValidationTarget());
        assertTrue(msg.getMessage().contains("MainProductName=mainProduct"));
        assertTrue(msg.getMessage().contains("QuotaProductName=quotaProduct"));
        assertTrue(msg.getMessage().contains("FieldsMissingInMainProduct=[]"));
        assertTrue(msg.getMessage().contains("FieldsDifferingInSchema=[sharedField]"));
        assertEquals(ValidationSeverity.ERROR, msg.getSeverity());
    }

    @Test
    void testEmptyProductBundle() {
        // Arrange
        when(productBundleDirectory.getGroups()).thenReturn(FastList.newList());
        when(productBundleDirectory.getAllProductsInBundle()).thenReturn(new ArrayList<>());

        // Act
        List<ProductValidationMessage> result = validator.validate(productBundleDirectory);

        // Assert
        assertTrue(result.isEmpty());
        verify(productRelationshipLookup, never()).apply(any(), any());
    }

    // Helper method to create a mock ProductGroupDirectory
    private ProductGroupDirectory mockProductGroupDirectory(ProductDirectory productDir) {
        ProductGroupDirectory groupDir = mock(ProductGroupDirectory.class);
        when(groupDir.getProducts()).thenReturn(FastList.newListWith(productDir));
        return groupDir;
    }
}
```

This test suite covers the following scenarios:

1. `testNoRelationships`: Verifies that no validation messages are generated when a product has no relationships.

2. `testValidRelationship`: Tests a successful case where a relationship exists and is found by the lookup function.

3. `testMissingRelationship`: Checks that an error message is generated when a relationship cannot be found, including version information.

4. `testQuotaRelationshipWithMissingFields`: Validates the quota relationship case where the main product is missing fields present in the quota product.

5. `testQuotaRelationshipWithDifferingSchema`: Tests the quota relationship case where fields exist in both products but have different schemas.

6. `testEmptyProductBundle`: Ensures no errors when the product bundle is empty.

Dependencies required in your `pom.xml` (in addition to those from the previous test):
```xml
<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>5.10.0</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-core</artifactId>
        <version>5.7.0</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-junit-jupiter</artifactId>
        <version>5.7.0</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.eclipse.collections</groupId>
        <artifactId>eclipse-collections-api</artifactId>
        <version>11.1.0</version>
    </dependency>
    <dependency>
        <groupId>org.eclipse.collections</groupId>
        <artifactId>eclipse-collections</artifactId>
        <version>11.1.0</version>
    </dependency>
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>2.15.2</version>
    </dependency>
</dependencies>
```

Additional notes:
- The tests assume a `ProductDefinition` class exists with methods like `getRelationships()`, `getFields()`, and `getProductName()`. You may need to adjust these if the actual class differs.
- The `SelfServiceProductField` class is mocked with a `hasSameSchema()` method; adjust this if the actual implementation differs.
- The tests use Mockito to mock dependencies and verify interactions.
- The helper method `mockProductGroupDirectory` simplifies setup of the group directory structure.

These tests should provide good coverage of the `ProductRelationshipValidator` class's functionality while remaining isolated from actual implementations of its dependencies.
