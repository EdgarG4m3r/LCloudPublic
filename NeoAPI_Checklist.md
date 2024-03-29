### LuckyNetwork Neo & Circle Media API Checklist

### Authentication
- Bearer Authentication requires a minimum of 120 characters, Enforce using strong validation with a well-defined pattern.
- Do not process inputs before authenticated. Pre-Authentication should only process Bearer Token.
- For user-specific action, use DynamicGlobalAuth Authentication API (DGA). DynamicGlobalAuth provides a secure authentication service to authenticate using LuckyNetwork Account Credentials.
- For Public API, Bearer Token should be obtained, validated, and stored by TackleAuthenticationService (TAS) via TackleAuthenticationProtocol (TAP). TAS provides zero-trust, tamper-resistant, and fast token storage while TAP ensures token integrity at rest.

### Security
- Both API Client and API Server should be made secure by design. Security functions should fail close by design.
- Private APIs should not be exposed to the public.
- HTTP(s) is optional while the API endpoint is using Level 1 & Level 2 Intranet. Both Intranet already comes with strong encryption and authentication mechanism
- For Private API, If the API should be accessible by a human/staff operator, then use Level 1 Intranet.

### Inputs
- Inputs should be validated and well-defined.
- The Server and Client should communicate via JSON or Preshared Delimiter Serialization

### Server Outputs
- Do not use spaces,
- Use ErrorFactory and ResultFactory to generate Error or Result Object to return to the Client,
- ErrorFactory is reserved for pre-processing errors. ResultFactory should be returned if there is no logical error while running the code,
- Error Messages with no dynamic field should be memorized to reuse JSON Objects,

### Resilience
- API Should be made with failover ability by design,
- API Server should be able to absorb request spikes to resist DDoS up to 3x of the rated capacity,
- API Server should have a builtin rate limiter, with circuit breaker pattern and bulkhead design by default,
- If API Server relies on another API Server, then there should be a well-defined caching strategy and built-in mechanism to prevent failure from propagating

### Performance
- API Server should be able to respond in sub-millisecond latency
- API Client should be able to process in sub-millisecond latency
- Caching strategy should be implemented to reduce roundtrip and hitting the database
- API Request should be cut off if it takes longer than 100ms by the client.
- API Server should provide Bulk Endpoint to process multiple entries.
- API Address should be set to HTTP to allow Infrastructure HTTPLink. Therefore, API should be accessed via Intranet only

### Clients
- Client should be able to self-throttle to prevent overloading the API Server
- Client should have a builtin circuit breaker pattern to prevent failure from propagating

### General Don'ts
- Don't trust The API Client or The API Server. Strong validation should be done at both ends. It is always recommended for Private API to use Level 2 Intranet as it provides strong cryptographic authentication by default on the network level.
- Don't reuse the API key, the API key should be random and stored in a secure location where it is not accessible during API runtime by functions that can expose the key. For Public API, use a Token generated by TackleAuthenticationService.


### General Dos
- If a feature requires multiple API to work (Ex: Friends requires PlayerLookupAPI, NeoConstellationAPI, NeoKratosGlobalAPI) unless it is beneficial to prevent failure from propagating, do not let the client directly communicate to those APIs. Instead, let FriendsAPI communicate to those APIs.
- For Public API that is user-specific (for example, viewing LuckyCoins), the Token generated by TAS should be bound with a secret derived by DGA using TAP. This will ensure that the token can only access the user resource.
- Do implement with NeoGuard. NeoGuard is a SOAR platform.
- Do log everything with NeoLogger. NeoLogger also functions as a SIEM feeding data to NeoGuard without requiring direct integration. But it is recommended to both integrate into NeoGuard and use NeoLogger for automated security responses.
- HTTPLink is an infrastructure feature that will significantly reduce HTTP overhead by increasing connection priority and dynamic keep-alive on the fly. HTTPLink is automatically enabled for all of internal REST API call that is not SSL and is traveling via Intranet Level 1-2 between multiple V7 Servers. HTTPLink will be triggered automatically after 10 or more conneections based on the usage pattern. Developer might see significant decrease of latency for long lived non HTTP connection once HTTPLink is triggered. Therefore, it is recommended for developers to use the default implementation of connection pooling since HTTPLink has been trained with such pattern.
