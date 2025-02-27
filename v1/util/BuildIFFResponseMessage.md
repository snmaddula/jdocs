Certainly! Below is the Javadoc for the `BuildIFFResponseMessage` class, including detailed explanations for all methods, formatted with HTML tags for clarity. This documentation provides a summary of the class's responsibility and detailed descriptions of each method's logic.

```java
package com.syf.synapps.iff.rest.service.impl;

/**
 * <h1>BuildIFFResponseMessage</h1>
 * 
 * <p>
 * This class is responsible for constructing and managing the response messages
 * for the IFF (Integrated Fraud Framework) service. It processes responses from
 * the EDL (External Data Layer) service, handles error scenarios, and prepares
 * structured response messages based on various conditions.
 * </p>
 */
public class BuildIFFResponseMessage {

    /**
     * Sets the return response based on the provided response entity.
     * 
     * <p>This method checks if the merchant MSA (Multi-Service Agreement) is enabled
     * and processes the response accordingly. If there are errors in the MSA response,
     * it prepares the response for MSA failure; otherwise, it sets a success response.</p>
     * 
     * @param responseEntity The entity containing the response data.
     * @param isMySqlCall Indicates if the call is to MySQL.
     * @param applicant The applicant identifier (primary or secondary).
     */
    public void setReturnResponse(BuildIFFResponseMessageEntity responseEntity, boolean isMySqlCall, String applicant) {
        // Implementation omitted for brevity
    }

    /**
     * Prepares the response when MSA is disabled.
     * 
     * <p>This method constructs the response based on the status of the IFF and Bustout
     * services. It checks for errors in the responses and sets appropriate response codes
     * and messages based on the conditions.</p>
     * 
     * @param responseEntity The entity containing the response data.
     * @param isMySqlCall Indicates if the call is to MySQL.
     * @param applicant The applicant identifier (primary or secondary).
     */
    public void prepareResponseMSADisabled(BuildIFFResponseMessageEntity responseEntity, boolean isMySqlCall, String applicant) {
        // Implementation omitted for brevity
    }

    /**
     * Prepares the response for Bustout when IFF is enabled.
     * 
     * <p>This method constructs the response when Bustout occurs and IFF fails.
     * It checks for various error codes and sets the appropriate response messages
     * based on the conditions.</p>
     * 
     * @param responseEntity The entity containing the response data.
     * @param isMySqlCall Indicates if the call is to MySQL.
     * @param applicant The applicant identifier (primary or secondary).
     * @param edlIffResponseMapping The mapping for IFF responses.
     * @param edlBustOutResponseMapping The mapping for Bustout responses.
     */
    public void prepareResponseForBustoutIFF(BuildIFFResponseMessageEntity responseEntity, boolean isMySqlCall,
                                             String applicant, Map<String, Object> edlIffResponseMapping,
                                             Map<String, Object> edlBustOutResponseMapping) {
        // Implementation omitted for brevity
    }

    /**
     * Prepares the response for Bustout based on the provided mappings.
     * 
     * <p>This method constructs the response when Bustout occurs and IFF fails.
     * It checks for various error codes and sets the appropriate response messages
     * based on the conditions.</p>
     * 
     * @param responseEntity The entity containing the response data.
     * @param isMySqlCall Indicates if the call is to MySQL.
     * @param applicant The applicant identifier (primary or secondary).
     * @param edlIffResponseMapping The mapping for IFF responses.
     * @param edlBustoutResponseMapping The mapping for Bustout responses.
     */
    public void prepareResponseForBustout(BuildIFFResponseMessageEntity responseEntity, boolean isMySqlCall,
                                          String applicant, Map<String, Object> edlIffResponseMapping, Map<String, Object> edlBustoutResponseMapping) {
        // Implementation omitted for brevity
    }

    /**
     * Prepares the response for IFF based on the provided mappings.
     * 
     * <p>This method constructs the response when Bustout fails and IFF succeeds.
     * It checks for various error codes and sets the appropriate response messages
     * based on the conditions.</p>
     * 
     * @param responseEntity The entity containing the response data.
     * @param isMySqlCall Indicates if the call is to MySQL.
     * @param applicant The applicant identifier (primary or secondary).
     * @param edlIffResponseMapping The mapping for IFF responses.
     * @param edlBustOutResponseMapping The mapping for Bustout responses.
     * @param edlNASSResponseMapping The mapping for NASS responses.
     */
    public void prepareResponseForIFF(BuildIFFResponseMessageEntity responseEntity, boolean isMySqlCall,
                                      String applicant, Map<String, Object> edlIffResponseMapping, Map<String, Object> edlBustOutResponseMapping,
                                      Map<String, Object> edlNASSResponseMapping) {
        // Implementation omitted for brevity
    }

    /**
     * Prepares the response for MSA based on the provided mappings.
     * 
     * <p>This method constructs the response when MSA processing occurs.
     * It checks for various error codes and sets the appropriate response messages
     * based on the conditions.</p>
     * 
     * @param responseEntity The entity containing the response data.
     * @param edlMSAResponseMapping The mapping for MSA responses.
     * @param isMySqlCall Indicates if the call is to MySQL.
     * @param applicant The applicant identifier (primary or secondary).
     */
    public void prepareResponseForMSA(BuildIFFResponseMessageEntity responseEntity,
                                      Map<String, Object> edlMSAResponseMapping, boolean isMySqlCall, String applicant) {
        // Implementation omitted for brevity
    }

    /**
     * Prepares the response for MSA failure based on the provided mappings.
     * 
     * <p>This method constructs the response when MSA processing fails.
     * It checks for various error codes and sets the appropriate response messages
     * based on the conditions.</p>
     * 
     * @param responseEntity The entity containing the response data.
     * @param edlIffResponseMapping The mapping for IFF responses.
     * @param edlBustoutResponseMapping The mapping for Bustout responses.
     * @param edlMSAResponseMapping The mapping for MSA responses.
     * @param isMySqlCall Indicates if the call is to MySQL.
     * @param applicant The applicant identifier (primary or secondary).
     */
    public void prepareResponseForMSAFailed(BuildIFFResponseMessageEntity responseEntity,
                                            Map<String, Object> edlIffResponseMapping, Map<String, Object> edlBustoutResponseMapping,
                                            Map<String, Object> edlMSAResponseMapping, boolean isMySqlCall, String applicant) {
        // Implementation omitted for brevity
    }

    /**
     * Processes exception messages based on the provided response mapping.
     * 
     * <p>This method checks for error codes in the response mapping and sets
     * the appropriate response codes and messages based on the conditions.</p>
     * 
     * @param responseEntity The entity containing the response data.
     * @param edlResponseMapping The mapping for EDL responses.
     * @param applicant The applicant identifier (primary or secondary).
     */
    public void processingExceptionMessage(BuildIFFResponseMessageEntity responseEntity, Map<String, Object> edlResponseMapping, String applicant) {
        // Implementation omitted for brevity
    }

    /**
     * Sets default values in the response entity based on the provided parameters.
     * 
     * <p>This method updates the response entity with default values for various
     * attributes based on the applicant type and the response status.</p>
     * 
     * @param flag The response flag to set.
     * @param respCode The response code to set.
     * @param msg The response message to set.
     * @param responseEntity The entity containing the response data.
     * @param applicant The applicant identifier (primary or secondary).
     */
    public void setDefaultValues(String flag, String respCode, String msg, BuildIFFResponseMessageEntity responseEntity, String applicant) {
        // Implementation omitted for brevity
    }

    /**
     * Sets default values in the response entity based on the provided parameters.
     * 
     * <p>This method updates the response entity with default values for various
     * attributes based on the response status.</p>
     * 
     * @param flag The response flag to set.
     * @param respCode The response code to set.
     * @param msg The response message to set.
     * @param responseEntity The entity containing the response data.
     */
    public void setDefaultValues(String flag, String respCode, String msg, BuildIFFResponseMessageEntity responseEntity) {
        // Implementation omitted for brevity
    }

    /**
     * Builds the final response message based on individual responses.
     * 
     * <p>This method constructs the final response message by evaluating the individual
     * response codes and determining the overall response status.</p>
     * 
     * @param individualResponse A list of individual response codes.
     * @param returnNode The node to populate with the final response.
     * @param isMySqlCall Indicates if the call is to MySQL.
     */
    public void buildSynappsIFFServiceResponse(List<String> individualResponse, ObjectNode returnNode, boolean isMySqlCall) {
        // Implementation omitted for brevity
    }

    /**
     * Fetches the response mappings for the Synapps service based on the MySQL call status.
     * 
     * <p>This method constructs a multimap of response codes and messages based on the
     * service configuration and the type of call being made.</p>
     * 
     * @param isMySqlCall Indicates if the call is to MySQL.
     * @return A multimap containing response codes and messages.
     */
    private Multimap<String, String> fetchSynappsResonse(boolean isMySqlCall) {
        // Implementation omitted for brevity
    }

    /**
     * Constructs a response flag based on the individual response codes.
     * 
     * <p>This method evaluates the individual response codes and constructs a combined
     * response flag indicating the overall status of the requests.</p>
     * 
     * @param individualResponse A list of individual response codes.
     * @return A string representing the combined response flag.
     */
    private String constructResponseFlag(List<String> individualResponse) {
        // Implementation omitted for brevity
    }
}
```

### Summary of the Methods

- **setReturnResponse**: Sets the return response based on the provided response entity, checking if the merchant MSA is enabled and processing the response accordingly.
----------

Certainly! Below is the Javadoc for the remaining methods in the `BuildIFFResponseMessage` class that you specified, including detailed explanations for each method, formatted with HTML tags for clarity.

```java
package com.syf.synapps.iff.rest.service.impl;

/**
 * <h1>BuildIFFResponseMessage</h1>
 * 
 * <p>
 * This class is responsible for constructing and managing the response messages
 * for the IFF (Integrated Fraud Framework) service. It processes responses from
 * the EDL (External Data Layer) service, handles error scenarios, and prepares
 * structured response messages based on various conditions.
 * </p>
 */

public class BuildIFFResponseMessage {

    /**
     * Sets default values in the response entity based on the provided parameters.
     * 
     * <p>This method updates the response entity with default values for various
     * attributes based on the applicant type and the response status.</p>
     * 
     * @param matchingLogic The logic determining which response values to set.
     * @param responseEntity The entity containing the response data.
     */
    public void setDefaultValuesForEDLResponse(String matchingLogic, BuildIFFResponseMessageEntity responseEntity) {
        // Implementation omitted for brevity
    }

    /**
     * Prepares default values for the EDL response based on the applicant type.
     * 
     * <p>This method updates the provided response node with default values
     * based on the matching logic provided.</p>
     * 
     * @param matchingLogic The logic determining which response values to set.
     * @param responseNode The response node to update with default values.
     */
    private void prepareDefaultValueForEDLResponseByApplicant(String matchingLogic, ObjectNode responseNode) {
        // Implementation omitted for brevity
    }

    /**
     * Sets default values in the response entity based on the provided parameters.
     * 
     * <p>This method updates the response entity with default values for various
     * attributes based on the response status and the applicant type.</p>
     * 
     * @param flag The response flag to set.
     * @param respCode The response code to set.
     * @param msg The response message to set.
     * @param responseEntity The entity containing the response data.
     * @param applicant The applicant identifier (primary or secondary).
     */
    public void setDefaultValues(String flag, String respCode, String msg, BuildIFFResponseMessageEntity responseEntity, String applicant) {
        // Implementation omitted for brevity
    }

    /**
     * Prepares the response for the primary applicant based on the provided parameters.
     * 
     * <p>This method constructs the response node for the primary applicant,
     * setting various attributes based on the response entity.</p>
     * 
     * @param responseEntity The entity containing the response data.
     * @param applicant The applicant identifier (primary or secondary).
     * @return The updated response entity.
     */
    private BuildIFFResponseMessageEntity prepareResponseNode(BuildIFFResponseMessageEntity responseEntity, String applicant) {
        // Implementation omitted for brevity
    }

    /**
     * Sets the response code in the return node of the response entity.
     * 
     * <p>This method updates the return node with the specified flag, code, and message.</p>
     * 
     * @param responseEntity The entity containing the response data.
     * @param responseFlag The response flag to set.
     * @param responseCode The response code to set.
     * @param responseMsg The response message to set.
     */
    private void returnResponseCode(BuildIFFResponseMessageEntity responseEntity, String responseFlag, String responseCode, String responseMsg) {
        // Implementation omitted for brevity
    }

    /**
     * Sets the response code in the return node of the response entity.
     * 
     * <p>This method updates the return node with the specified flag, code, and message.</p>
     * 
     * @param responseEntity The entity containing the response data.
     * @param responseFlag The response flag to set.
     * @param responseCode The response code to set.
     * @param responseMsg The response message to set.
     */
    private void returnResponseCode(BuiltIFFResponseMessageEntity responseEntity, String responseFlag, String responseCode, String responseMsg) {
        // Implementation omitted for brevity
    }
}
```

### Summary of the Methods

- **setDefaultValuesForEDLResponse**: This method sets default values in the response entity based on the provided matching logic, updating the response node accordingly.

- **prepareDefaultValueForEDLResponseByApplicant**: This method prepares default values for the EDL response based on the applicant type, updating the response node with appropriate flags.

- **setDefaultValues**: This method sets default values in the response entity based on the provided parameters, updating various attributes based on the applicant type and response status.

- **prepareResponseNode**: This method prepares the response node for the primary applicant, setting various attributes based on the response entity.

- **returnResponseCode**: This method sets the response code in the return node of the response entity, updating it with the specified flag, code, and message.

If you need further details or additional methods documented, feel free to ask!



Certainly! Below is the Javadoc for the two specified methods in the `BuildIFFResponseMessage` class, focusing solely on the method descriptions without including the method implementations or code.

```java
package com.syf.synapps.iff.rest.service.impl;

/**
 * <h1>BuildIFFResponseMessage</h1>
 * 
 * <p>
 * This class is responsible for constructing and managing the response messages
 * for the IFF (Integrated Fraud Framework) service. It processes responses from
 * the EDL (External Data Layer) service, handles error scenarios, and prepares
 * structured response messages based on various conditions.
 * </p>
 */

public class BuildIFFResponseMessage {

    /**
     * Prepares the response for the primary applicant based on the provided parameters.
     * 
     * <p>This method constructs the response node for the primary applicant,
     * setting various attributes based on the response entity. It checks if the
     * IFF and Bustout services are enabled and updates the response node accordingly.</p>
     * 
     * @param responseEntity The entity containing the response data.
     */
    private void preparePrimaryOnlyApplicantResponse(BuildIFFResponseMessageEntity responseEntity) {
        // Implementation omitted for brevity
    }

    /**
     * Sets default values in the response entity based on the provided parameters.
     * 
     * <p>This method updates the response entity with default values for various
     * attributes based on the applicant type and the response status.</p>
     * 
     * @param flag The response flag to set.
     * @param respCode The response code to set.
     * @param msg The response message to set.
     * @param responseEntity The entity containing the response data.
     */
    public void setDefaultValues(String flag, String respCode, String msg, BuildIFFResponseMessageEntity responseEntity) {
        // Implementation omitted for brevity
    }
}
```

### Summary of the Methods

- **preparePrimaryOnlyApplicantResponse**: This method prepares the response for the primary applicant by setting various attributes in the response node based on the response entity. It checks if the IFF and Bustout services are enabled and updates the response node accordingly.

- **setDefaultValues**: This method sets default values in the response entity based on the provided parameters, updating various attributes based on the applicant type and response status.

If you need further details or additional methods documented, feel free to ask!
