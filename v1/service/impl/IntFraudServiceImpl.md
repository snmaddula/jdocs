Certainly! Below is the Javadoc for the remaining methods in the `IntFraudServiceImpl` class, focusing on their purpose and logic without including the method implementations.

```java
package com.syf.synapps.iff.rest.service.impl;

/**
 * Implementation of the IntFraudService interface.
 * This service is responsible for handling fraud detection processes,
 * including retrieving records from various data sources and processing
 * the results.
 */
@Slf4j
@Service
public class IntFraudServiceImpl implements IntFraudService {

    /**
     * Retrieves records based on the provided choreo request and version.
     *
     * <p>This method performs the following steps:</p>
     * <ol>
     *     <li><strong>Initialize Variables:</strong> Sets up the necessary variables, including the start time and resilience database fields.</li>
     *     <li><strong>Extract MSI Switch:</strong> Calls the <code>extractMsiSwitch</code> method to determine the data source.</li>
     *     <li><strong>Process Data Source:</strong> Depending on the data source (MySQL, Gemfire, or both), it processes the request accordingly.</li>
     *     <li><strong>Log Response:</strong> Logs the response using the <code>logger</code> service.</li>
     *     <li><strong>Error Handling:</strong> Catches exceptions and constructs an error response if necessary.</li>
     * </ol>
     *
     * @param choreoRequest The request string to be processed.
     * @param isVersionV2   Indicates if the version is V2.
     * @return The response string from the data source.
     * @throws IOException If an I/O error occurs during processing.
     */
    @Override
    public String retrieveRecords(String choreoRequest, Boolean isVersionV2) throws IOException {
        // Implementation omitted for brevity
    }

    /**
     * Extracts the MSI switch from the provided JSON string.
     *
     * <p>This method performs the following steps:</p>
     * <ol>
     *     <li><strong>Parse JSON:</strong> Reads the JSON string and extracts the data source array node.</li>
     *     <li><strong>Find Data Source:</strong> Iterates through the data source nodes to find the one matching the service name.</li>
     *     <li><strong>Extract MSI Flag:</strong> Retrieves the MSI flag from the found node.</li>
     * </ol>
     *
     * @param jsonString   The JSON string containing the request data.
     * @param resilienceDB The resilience database fields to capture any errors.
     * @return The MSI database switch indicating the data source.
     */
    public MsiDbSwitch extractMsiSwitch(String jsonString, ResilienceDbFields resilienceDB) {
        // Implementation omitted for brevity
    }

    /**
     * Processes the SQL result based on the choreo request and version.
     *
     * <p>This method performs the following steps:</p>
     * <ol>
     *     <li><strong>Start Timer:</strong> Records the start time for logging.</li>
     *     <li><strong>Process Standin:</strong> Calls the <code>standinProcessing</code> method to handle the request.</li>
     *     <li><strong>Log JSON:</strong> Logs the response using the <code>logger</code> service.</li>
     * </ol>
     *
     * @param choreoRequest The request string to be processed.
     * @param isVersionV2   Indicates if the version is V2.
     * @param returnResponse The monitor return response object containing metadata.
     * @param resilienceDB  The resilience database fields to capture any errors.
     * @return The processed SQL response as a string.
     * @throws JsonProcessingException If an error occurs during JSON processing.
     */
    public String processSQLResult(String choreoRequest, Boolean isVersionV2, MonitorReturnResponse returnResponse, ResilienceDbFields resilienceDB) throws JsonProcessingException {
        // Implementation omitted for brevity
    }

    /**
     * Processes the DSG result based on the choreo request and version.
     *
     * <p>This method performs the following steps:</p>
     * <ol>
     *     <li><strong>Start Timer:</strong> Records the start time for logging.</li>
     *     <li><strong>Process EDL:</strong> Calls the <code>edlProcessing</code> method to handle the request.</li>
     *     <li><strong>Log JSON:</strong> Logs the response using the <code>logger</code> service.</li>
     * </ol>
     *
     * @param choreoRequest The request string to be processed.
     * @param isVersionV2   Indicates if the version is V2.
     * @param returnResponse The monitor return response object containing metadata.
     * @param resilienceDB  The resilience database fields to capture any errors.
     * @return The processed DSG response as a string.
     * @throws JsonProcessingException If an error occurs during JSON processing.
     */
    public String processDSGResult(String choreoRequest, Boolean isVersionV2, MonitorReturnResponse returnResponse, ResilienceDbFields resilienceDB) throws JsonProcessingException {
        // Implementation omitted for brevity
    }

    /**
     * Processes the EDL request based on the choreo request and version.
     *
     * <p>This method performs the following steps:</p>
     * <ol>
     *     <li><strong>Parse Request:</strong> Reads the choreo request and extracts necessary fields.</li>
     *     <li><strong>Validate Data:</strong> Checks for required data and prepares the request for EDL.</li>
     *     <li><strong>Make EDL Call:</strong> Executes the EDL API call and processes the response.</li>
     * </ol>
     *
     * @param choreoRequest The request string to be processed.
     * @param isVersionV2   Indicates if the version is V2.
     * @param splunkLogging The Splunk logging object to populate with attributes.
     * @param returnResponse The monitor return response object containing metadata.
     * @param resilienceDB  The resilience database fields to capture any errors.
     * @return The processed EDL response as a string.
     * @throws JsonProcessingException If an error occurs during JSON processing.
     */
    public String edlProcessing(String choreoRequest, Boolean isVersionV2, SplunkLogging splunkLogging, MonitorReturnResponse returnResponse, ResilienceDbFields resilienceDB) throws JsonProcessingException {
        // Implementation omitted for brevity
    }

    /**
     * Prepares the EDL request object based on the provided parameters.
     *
     * <p>This method constructs a map of request objects for EDL based on the applicant's data.</p>
     *
     * @param root                The root JSON node of the request.
     * @param appaNode           The applicant node.
     * @param primaryCsNode      The primary context node.
     * @param secondaryCsNode    The secondary context node.
     * @param applicationType     The type of application being processed.
     * @param applicant           The applicant object.
     * @param isValidPrimaryApplicant Indicates if the primary applicant is valid.
     * @param isValidSecondaryApplicant Indicates if the secondary applicant is valid.
     * @param resilienceDB        The resilience database fields to capture any errors.
     * @return A map of EDL request objects.
     */
    private Map<String, Map<String, String>> prepareEDLRequestObject(JsonNode root, JsonNode appaNode, JsonNode primaryCsNode, JsonNode secondaryCsNode, String applicationType, Applicant applicant, boolean isValidPrimaryApplicant, boolean isValidSecondaryApplicant, ResilienceDbFields resilienceDB) {
        // Implementation omitted for brevity
    }

    /**
     * Fetches EDL data based on the provided request objects.
     *
     * <p>This method executes asynchronous calls to the EDL service and collects the responses.</p>
     *
     * @param edlRequestObjects The request objects for EDL.
     * @param edlIFFResponseMapping The mapping for IFF responses.
     * @param edlBustOutResponseMapping The mapping for bust-out responses.
     * @param edlMSAResponseMapping The mapping for MSA responses.
     * @param edlHotlistResponseMapping The mapping for hotlist responses.
     * @param splunkLogging The Splunk logging object to populate with attributes.
     * @param resilienceDB The resilience database fields to capture any errors.
     * @return A map of computed EDL responses.
     */
    private Map<String, Map<String, String>> fetchEDLData(Map<String, String> edlRequestObjects, Map<String, Object> edlIFFResponseMapping, Map<String, Object> edlBustOutResponseMapping, Map<String, Object> edlMSAResponseMapping, Map<String, Object> edlHotlistResponseMapping, SplunkLogging splunkLogging, ResilienceDbFields resilienceDB) {
        // Implementation omitted for brevity
    }

    /**
     * Handles exceptions that occur during EDL data fetching.
     *
     * <p>This method processes the exception and updates the appropriate response mapping.</p>
     *
     * @param edlResponseMap The response map to update.
     * @param exceptionCause The cause of the exception.
     */
    protected void fetchEDLDataExceptionHandler(Map<String, Object> edlResponseMap, String exceptionCause) {
        // Implementation omitted for brevity
    }

    /**
     * Fetches EDL data based on the provided response object.
     *
     * <p>This method processes the response and updates the response object accordingly.</p>
     *
     * @param responseObject The response object to update.
     * @param k The key for the response.
     * @param response The CompletableFuture containing the response.
     * @throws InterruptedException If the thread is interrupted.
     * @throws ExecutionException If an error occurs during execution.
     */
    protected void fetchEDLData(Map<String, String> responseObject, String k, CompletableFuture<String> response) throws InterruptedException, ExecutionException {
        // Implementation omitted for brevity
    }

    /**
     * Asynchronously retrieves EDL data based on the provided request objects.
     *
     * <p>This method executes the requests in parallel and returns a map of CompletableFuture responses.</p>
     *
     * @param edlRequestObjects The request objects for EDL.
     * @return A map of CompletableFuture responses.
     */
    @Async
    public Map<String, CompletableFuture<String>> getEDLData(Map<String, String> edlRequestObjects) {
        // Implementation omitted for brevity
    }

    /**
     * Processes the EDL client exception based on the provided response map and exception cause.
     *

     /**
     * Processes the EDL data based on the provided response object and updates the response mapping.
     *
     * <p>This method checks the type of EDL response and updates the corresponding error response mapping.</p>
     *
     * @param edlResponseMap The response map to update based on the EDL call.
     * @param exceptionCause The cause of the exception that occurred during the EDL call.
     */
    protected void processEdlClientException(Map<String, Object> edlResponseMap, String exceptionCause) {
        // Implementation omitted for brevity
    }

    /**
     * Processes the response from the EDL call and updates the computed response map.
     *
     * <p>This method checks the key of the response and updates the response object accordingly.</p>
     *
     * @param responseObject The response object to update.
     * @param k The key for the response.
     * @param response The CompletableFuture containing the response.
     * @throws InterruptedException If the thread is interrupted.
     * @throws ExecutionException If an error occurs during execution.
     */
    protected void fetchEDLData(Map<String, String> responseObject, String k, CompletableFuture<String> response) throws InterruptedException, ExecutionException {
        // Implementation omitted for brevity
    }

    /**
     * Asynchronously retrieves EDL data based on the provided request objects.
     *
     * <p>This method executes the requests in parallel and returns a map of CompletableFuture responses.</p>
     *
     * @param edlRequestObjects The request objects for EDL.
     * @return A map of CompletableFuture responses.
     */
    @Async
    public Map<String, CompletableFuture<String>> getEDLData(Map<String, String> edlRequestObjects) {
        // Implementation omitted for brevity
    }
}
```

### Summary of the Methods

- **processEdlClientException**: This method processes exceptions that occur during EDL calls and updates the corresponding error response mapping based on the type of exception.

- **fetchEDLData**: This method processes the response from the EDL call, updating the computed response map based on the key of the response.

- **getEDLData**: This method retrieves EDL data asynchronously based on the provided request objects, executing the requests in parallel and returning a map of `CompletableFuture` responses.

If you need further details or additional methods documented, feel free to ask!
