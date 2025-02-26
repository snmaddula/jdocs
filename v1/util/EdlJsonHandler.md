Below is the JavaDoc for the `EdlJsonHandler` class, including a class-level summary and detailed JavaDoc for all methods (public, private, and helper methods). The JavaDoc uses HTML formatting where applicable and skips import statements and implementation logic for brevity, focusing on summaries and high-level logic descriptions.

```java
package com.syf.synapps.iff.rest.util;

/**
 * <p>Component class responsible for building and handling JSON data for EDL (External Data Layer) requests.</p>
 * <p>This class constructs JSON payloads for various fraud detection and credit service queries, such as IFF, bust-out,
 * MSA, and hotlist checks. It processes applicant data, normalizes addresses, builds query parameters, and validates
 * input nodes from JSON structures. It integrates with {@link AppConfig} for configuration and uses logging and error
 * tracking for resilience. The class supports both primary and secondary applicant data processing.</p>
 */
@Slf4j
@Component
@RequiredArgsConstructor
public class EdlJsonHandler {

    private final AppConfig appConfig;

    /**
     * Builds a JSON request string for EDL queries.
     *
     * <p><b>Summary:</b> This method constructs a JSON string for EDL requests based on context parameters and applicant data.</p>
     *
     * <p><b>Logic Details:</b></p>
     * <ul>
     *   <li>Extracts root and application nodes from context parameters.</li>
     *   <li>Determines whether to read secondary applicant data.</li>
     *   <li>Adds transaction ID, keycode, event name, and timestamp to the JSON object.</li>
     *   <li>Builds and includes queries and parameters based on matching logic.</li>
     *   <li>Handles exceptions and updates resilience tracking.</li>
     * </ul>
     *
     * @param matchingLogic The logic type (e.g., IFF, bust-out) for the query.
     * @param applicationType The type of application (e.g., auth user).
     * @param isAutSecondaryUser Flag indicating if the user is a secondary authorized user.
     * @param readSecondaryApp Flag indicating whether to read secondary applicant data.
     * @param cparams The {@link ContextParameters} containing JSON nodes and applicant data.
     * @param resilienceDB The {@link ResilienceDbFields} object for error tracking.
     * @return A JSON string for the EDL request, or null if an error occurs.
     */
    public String requestJsonBuilder(String matchingLogic, String applicationType, boolean isAutSecondaryUser, boolean readSecondaryApp, ContextParameters cparams, ResilienceDbFields resilienceDB) {
        // Implementation skipped for brevity
    }

    /**
     * Builds a JSON object containing query parameters.
     *
     * <p><b>Summary:</b> This method constructs a JSON array of parameters based on applicant data and matching logic.</p>
     *
     * <p><b>Logic Details:</b></p>
     * <ul>
     *   <li>Handles merchant MSA queries by adding only the store zip code.</li>
     *   <li>For non-MSA queries, normalizes current and previous addresses.</li>
     *   <li>Adds LexID, SSN, name, address, phone, and other fields based on matching logic.</li>
     *   <li>Wraps parameters in a JSON array.</li>
     * </ul>
     *
     * @param dataNod The {@link ArrayNode} containing data source information.
     * @param csINodeIndex The index of the CSL node in the data array.
     * @param applicant The {@link Applicant} object with data to include.
     * @param readSecondaryApp Flag indicating whether to read secondary applicant data.
     * @param isMerchantMSA Flag indicating if the query is for a merchant MSA.
     * @param matchingLogic The logic type determining parameter inclusion.
     * @return A {@link JSONObject} containing the parameter array.
     */
    public JSONObject buildParams(ArrayNode dataNod, int csINodeIndex, Applicant applicant, boolean readSecondaryApp, boolean isMerchantMSA, String matchingLogic) {
        // Implementation skipped for brevity
    }

    /**
     * Adds internal parameters like phone number to a JSON object.
     *
     * <p><b>Summary:</b> This protected helper method adds phone-related parameters to a JSON object.</p>
     *
     * <p><b>Logic Details:</b></p>
     * <ul>
     *   <li>Validates phone number length and pattern.</li>
     *   <li>Adds the phone number or a blank space based on validation.</li>
     * </ul>
     *
     * @param param The {@link JSONObject} to update with parameters.
     * @param applicant The {@link Applicant} object containing phone data.
     */
    protected void buildParamsInternal(JSONObject param, Applicant applicant) {
        // Implementation skipped for brevity
    }

    /**
     * Adds SSN parameter to a JSON object.
     *
     * <p><b>Summary:</b> This protected helper method adds an SSN parameter to a JSON object.</p>
     *
     * <p><b>Logic Details:</b></p>
     * <ul>
     *   <li>Validates SSN length and pattern against exclusions.</li>
     *   <li>Adds the SSN or a blank space based on validation.</li>
     * </ul>
     *
     * @param applicant The {@link Applicant} object containing SSN data.
     * @param param The {@link JSONObject} to update with the SSN.
     */
    protected void buildParams(Applicant applicant, JSONObject param) {
        // Implementation skipped for brevity
    }

    /**
     * Adds LexID parameter to a JSON object from a data node.
     *
     * <p><b>Summary:</b> This protected helper method adds a LexID parameter to a JSON object from a data node.</p>
     *
     * <p><b>Logic Details:</b></p>
     * <ul>
     *   <li>Checks if CSL data is available in the node.</li>
     *   <li>Extracts and validates the LexID from the CSL node.</li>
     *   <li>Adds the LexID or a blank space to the JSON object.</li>
     * </ul>
     *
     * @param dataNode The {@link ArrayNode} containing CSL data.
     * @param csLNodeIndex The index of the CSL node.
     * @param readSecondaryApp Flag indicating whether to read secondary data.
     * @param param The {@link JSONObject} to update with the LexID.
     */
    protected void buildParams(ArrayNode dataNode, int csLNodeIndex, boolean readSecondaryApp, JSONObject param) {
        // Implementation skipped for brevity
    }

    /**
     * Builds a JSON array of queries based on matching logic.
     *
     * <p><b>Summary:</b> This method constructs a JSON array of query objects for EDL requests.</p>
     *
     * <p><b>Logic Details:</b></p>
     * <ul>
     *   <li>Retrieves queries based on the specified flag and application type.</li>
     *   <li>Iterates over query entries, adding SQL and query count to JSON objects.</li>
     *   <li>Populates a JSON array with query objects.</li>
     * </ul>
     *
     * @param flag The matching logic flag (e.g., IFF, bust-out).
     * @param applicationType The type of application.
     * @param readSecondaryApp Flag indicating whether to include secondary app queries.
     * @return A {@link JSONArray} of query objects.
     */
    public JSONArray buildQueries(String flag, String applicationType, boolean readSecondaryApp) {
        // Implementation skipped for brevity
    }

    /**
     * Builds a JSON object containing version information.
     *
     * <p><b>Summary:</b> This method constructs a JSON object with EDL version details.</p>
     *
     * <p><b>Logic Details:</b></p>
     * <ul>
     *   <li>Creates a version object with major, minor, and patch numbers.</li>
     *   <li>Adds version date and version details to the JSON object.</li>
     * </ul>
     *
     * @return A {@link JSONObject} containing version information.
     */
    public JSONObject buildVersion() {
        // Implementation skipped for brevity
    }

    /**
     * Checks if CSL (Customer Service Layer) data is available in a data node.
     *
     * <p><b>Summary:</b> This method determines if CSL data exists within a data node array.</p>
     *
     * <p><b>Logic Details:</b></p>
     * <ul>
     *   <li>Iterates through the data node array.</li>
     *   <li>Checks for a matching service ID indicating CSL presence.</li>
     *   <li>Returns true if CSL is found, false otherwise.</li>
     * </ul>
     *
     * @param dataNode The {@link ArrayNode} to check for CSL data.
     * @return True if CSL data is available, false otherwise.
     */
    public boolean isCsLAvailable(ArrayNode dataNode) {
        // Implementation skipped for brevity
    }

    /**
     * Verifies if required data is available for a query.
     *
     * <p><b>Summary:</b> This method checks if sufficient data exists in JSON nodes for query execution.</p>
     *
     * <p><b>Logic Details:</b></p>
     * <ul>
     *   <li>Extracts data nodes and checks CSL availability.</li>
     *   <li>Validates LexID presence in primary or secondary CSL nodes.</li>
     *   <li>Checks required fields in applicant node based on primary/secondary status.</li>
     * </ul>
     *
     * @param root The root {@link JsonNode} containing data.
     * @param cslIndex The index of the CSL node.
     * @param applicantNode The {@link JsonNode} with applicant data.
     * @param isPrimaryApplicant Flag indicating if the applicant is primary.
     * @return True if required data is available, false otherwise.
     */
    public boolean isRequiredDataAvailable(JsonNode root, int cslIndex, JsonNode applicantNode, boolean isPrimaryApplicant) {
        // Implementation skipped for brevity
    }

    /**
     * Checks if required nodes exist in a primary applicant JSON node.
     *
     * <p><b>Summary:</b> This method validates the presence of required fields for a primary applicant.</p>
     *
     * <p><b>Logic Details:</b></p>
     * <ul>
     *   <li>Validates presence of key fields like name, SSN, DOB, phone, and address.</li>
     *   <li>Returns true if any required field is present and valid.</li>
     * </ul>
     *
     * @param applicantNode The {@link JsonNode} with primary applicant data.
     * @return True if required fields are present, false otherwise.
     */
    public boolean checkRequiredNodes(JsonNode applicantNode) {
        // Implementation skipped for brevity
    }

    /**
     * Checks if required fields exist in a secondary applicant JSON node.
     *
     * <p><b>Summary:</b> This method validates the presence of required fields for a secondary applicant.</p>
     *
     * <p><b>Logic Details:</b></p>
     * <ul>
     *   <li>Validates presence of secondary applicant fields like name, SSN, DOB, phone, and address.</li>
     *   <li>Returns true if any required field is present and valid.</li>
     * </ul>
     *
     * @param applicantNode The {@link JsonNode} with secondary applicant data.
     * @return True if required fields are present, false otherwise.
     */
    public boolean checkRequiredFieldInSecondaryNodes(JsonNode applicantNode) {
        // Implementation skipped for brevity
    }

    /**
     * Validates if a JSON node contains a non-null, non-blank child node.
     *
     * <p><b>Summary:</b> This method checks if a specified child node exists and has valid content.</p>
     *
     * <p><b>Logic Details:</b></p>
     * <ul>
     *   <li>Verifies the child node exists and is non-null.</li>
     *   <li>Ensures the text value is not blank or empty.</li>
     * </ul>
     *
     * @param parent The parent {@link JsonNode} to check.
     * @param childName The name of the child node to validate.
     * @return True if the child node is valid, false otherwise.
     */
    public boolean validateNode(JsonNode parent, String childName) {
        // Implementation skipped for brevity
    }

    /**
     * Constructs a current address string from two address lines.
     *
     * <p><b>Summary:</b> This method concatenates two address lines into a single string.</p>
     *
     * <p><b>Logic Details:</b></p>
     * <ul>
     *   <li>Combines the first and second address lines.</li>
     *   <li>Returns the concatenated address string.</li>
     * </ul>
     *
     * @param line1 The first address line.
     * @param line2 The second address line.
     * @return The concatenated address string.
     */
    public String getCurrentAddress(String line1, String line2) {
        // Implementation skipped for brevity
    }

    /**
     * Retrieves queries based on matching logic and application type.
     *
     * <p><b>Summary:</b> This private method determines the appropriate queries for an EDL request.</p>
     *
     * <p><b>Logic Details:</b></p>
     * <ul>
     *   <li>Switches on the matching logic flag to select query set.</li>
     *   <li>Adjusts queries based on application type and secondary app status.</li>
     *   <li>Returns a map of query IDs to SQL statements.</li>
     * </ul>
     *
     * @param flag The matching logic flag (e.g., IFF, bust-out).
     * @param applicationType The type of application.
     * @param isSecondaryApp Flag indicating if the applicant is secondary.
     * @param readSecondaryApp Flag indicating whether to read secondary app data.
     * @return A map of query IDs to SQL statements.
     */
    private Map<String, String> getQuery(String flag, String applicationType, boolean isSecondaryApp, boolean readSecondaryApp) {
        // Implementation skipped for brevity
    }

    /**
     * Prepares queries for IFF matching logic.
     *
     * <p><b>Summary:</b> This private method prepares a query map for IFF logic based on application type.</p>
     *
     * <p><b>Logic Details:</b></p>
     * <ul>
     *   <li>Checks if the application is for an authorized user with a secondary applicant.</li>
     *   <li>Returns a specific query for secondary users or the full IFF query set.</li>
     * </ul>
     *
     * @param applicationType The type of application.
     * @param isSecondaryApp Flag indicating if the applicant is secondary.
     * @return A map of query IDs to SQL statements.
     */
    private Map<String, String> prepareQuery(String applicationType, boolean isSecondaryApp) {
        // Implementation skipped for brevity
    }

    /**
     * Prepares queries for hotlist matching logic.
     *
     * <p><b>Summary:</b> This private method constructs a query map for hotlist checks.</p>
     *
     * <p><b>Logic Details:</b></p>
     * <ul>
     *   <li>Retrieves the full hotlist query set from configuration.</li>
     *   <li>Adjusts the query set based on whether secondary app data is read.</li>
     *   <li>Returns a subset or full set of hotlist queries.</li>
     * </ul>
     *
     * @param readSecondaryApp Flag indicating whether to read secondary app data.
     * @return A map of query IDs to SQL statements.
     */
    private Map<String, String> prepareHotlistQuery(boolean readSecondaryApp) {
        // Implementation skipped for brevity
    }
}
```

### Notes:
1. **Class-Level Summary**: Describes the responsibility of `EdlJsonHandler` as building and handling JSON data for EDL requests, supporting various fraud detection queries.
2. **Method JavaDoc**: Each method includes a summary and a high-level logic overview using HTML `<ul>` lists, skipping detailed implementation for brevity.
3. **HTML Formatting**: Used for clarity with `<p>` for summaries and `<ul>` for logic steps.
4. **Consistency**: Reflects the purpose of each method based on its name, parameters, and role in the class.

Let me know if you need any adjustments or additional details!
