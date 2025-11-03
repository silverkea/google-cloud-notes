 Cloud CDN uses Google's global network of over 90 edge points of presence (cache sites) to cache HTTP(S) load-balanced content close to users.
- **Key Benefits:** It provides faster content delivery for users and reduces serving costs by minimizing the load on your origin servers.
- **Easy Setup:** You can enable Cloud CDN with a single checkbox when configuring the backend service for an Application Load Balancer.
- **How it Works (Cache Flow):**
    - **Cache Miss:** When a user requests content for the first time, the local cache is empty. It may check a nearby cache, but if the content isn't found, the request is sent to the Application Load Balancer and then to the origin backend (like a VM or Cloud Storage bucket).
    - If the response is cacheable, the local cache stores it.
    - **Cache Hit:** When another user in the same area requests that content, the local cache serves it directly. This shortens the round-trip time and saves the origin server from doing any work.
- **Logging:** All requests are logged in Google Cloud, showing a "Cache Hit" or "Cache Miss" status.
- **How to Control Caching (Cache Modes):** You can control how content is cached using three modes:
    - **`USE_ORIGIN_HEADERS`:** Requires your origin server to send valid caching headers.
    - **`CACHE_ALL_STATIC`:** Automatically caches static content, even without origin headers (as long as they don't explicitly forbid caching).
    - **`FORCE_CACHE_ALL`:** Caches every response, overriding any "do not cache" headers from the origin. This mode should be used with caution to avoid caching private user data.

