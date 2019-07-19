# NGINX:v1.17.0 With modSecurity:v3.0.0 and Brotli Custom Docker Image for Production

NGINX Production ready config with docker-compose

As part of production Setup and Performance improvements we have integrated following changes.

1. All the API’s req/res are secured through IAM – Authorization and authentication.
2. NGINX as reverse proxy and load balancer for all the requests
   - UI static files
   - API Requests
3. Protocol change from HTTP/1.1 to HTTP/2 with server push
4. Encoding compression algorithm: upgradation from gzip to Brotli (introduced and used in Google’s infrastructure) reduced the content compression over the network for 80% and above compression (ie. 10MB over the network compressible to ~1.5MB)
5. Browser Cache: Cache the static UI files completely in browser for 365 days so the UI will be loading from browser’s in-memory/disk cache.
6. Rate Limiting: We can rate limit the API’s req/res to stop DDOS attack which makes our server’s to block such requests and improve HA (High availability). We are allowing 30 req/res for unique client IP’s.
7. API Req/res performance improvements:
   - Content type limiting
   - Security headers to avoid cross platform attacks through scripts (X-Frame-Options, X-XSS-Protection, X-Content-Type-Options, Referrer-Policy, Content-Security-Policy, Strict-Transport-Security)
   - Strict SSL Policies
   - HTTP/2.0
   - Cache control for OPTIONS Call etc…
8. Inhouse Custom NGINX Docker image for security and encoding req/res:
   - Concurrent Requests handling
   - Caching user IP’s till 2 \* 1,60,000 per second
   - Load balance config to handle Million requests per second
   - Efficient use of Buffers
   - Improving static file compression
   - HTTP/2.0 service with server push
   - Strict SSL policy
   - ModSecurity to handle 98% of Known Cyber attacks, suspicious requests, cross origin requests, anomaly detection etc..,
   - Brotli encoding with backward compatibility with gzip browsers
   - HTTP request timeouts to handle stalled requests
   - Header Content size limitation for handling bulk upload attacks
   - Black List and Whitelisting known and unknown source requests
   - Control Allowed Request headers
   - Improve TTFB – TIME to FIRST BYTE
