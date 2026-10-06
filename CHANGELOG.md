# Datapower Monitoring Extension CHANGELOG

### 1.0.0: 
*  Initial Release
    
### 1.1.0: 
*  Added support to filter by domains
    
### 1.1.2: 
*  Support for Encryption
    
### 1.2.0: 
*  Support for domains and domains-regex
    
### 1.3.2: 
*  Support for multiple DP servers and TLS support
    
### 1.3.4: 
*  Workbench Support
    
### 1.3.5: 
*  Http client builder upgrade
    
### 1.3.6: 
*  Updated the commons library, fixed multiplier issue in metrics.xml
    
### 1.3.7: 
*  Updated licenses
    
### 2.0.0:
*  Revamp to 2.2.4 extension commons.

### 2.0.1:
*  Updated extension commons to 2.2.13.

### 2.0.2:
*  Fixed an XXE vulnerability in the XML parser used to read DataPower responses.
*  Changed the sample config.yml to enable TLS certificate/hostname verification and TLSv1.2 by default.
*  Updated extension commons to 2.2.20 and refreshed build tooling (Maven plugins, mockito, junit).

### 2.0.3:
*  Fixed appliance-wide status providers (SystemUsage, MemoryStatus, FilesystemStatus) being
   queried against the wrong (non-default) domain when multiple domains are configured; they
   now consistently use the `default` domain via `use-domain="default"` in metrics.xml, matching
   the existing CPUUsage behavior.
*  Added automatic retry (once, by default) when a request fails with NoHttpResponseException,
   which typically indicates a stale pooled/keep-alive connection being reused after the server
   or a network intermediary closed it. Configurable via the new `connection.noHttpResponseRetryCount`
   setting in config.yml.
*  Downgraded the "<stat> returned null" log message from ERROR to WARN, since an empty
   `<dp:status/>` response is a valid, successful DataPower response (no data for that status
   provider/domain in the polled interval), not a fetch or parsing failure.
*  Added a DEBUG log message on every successful fetch (domain, operation, and which attempt
   number out of maxAttempts succeeded), so enabling DEBUG logging on MetricFetcher/
   BulkApiMetricFetcher makes it easy to gauge how often the NoHttpResponseException retry is
   actually being used.
    