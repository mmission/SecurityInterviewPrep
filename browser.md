## Browser Security Concepts

* Same Origin Policy (SOP)
    * Restricts how content can be loaded from other origins and restricts how content from other origins can interact with content on your current origin
    * Origins must match for JS to be able to directly interact with the DOM
    * Cross-origin writes are typically allowed (refer to CORS) - primarily for "simple requests" otherwise they pre-flight
    * Cross-origin reads are typically disallowed, but embedding may leak data
    * Cross-origin embedding is typically allowed
        * The following items can all be embedded cross-origin:
            * JS, CSS, images, video, audio, applets (object, embed, applet), fonts, frames
* Cross-Origin Resource Sharing (CORS)
    * Allows websites to make cross-origin requests without breaking the SOP model
    * The server being requested returns a collection of special HTTP Headers which define what cross-origin requests are allowed (explained below)
        * If no CORS headers are returned, it is assumed the server cannot have cross-origin requests made to it (an error is shown in the JS Console)
    * Uses extra headers (`Access-Control-Allow-Origin`) to define what origin is allowed to make cross-origin requests
    * Employs other headers to define what headers can also be included in the cross-origin request
        * `Access-Control-Allow-Methods` - What methods can be used cross-origin
        * `Access-Control-Allow-Headers` - What headers can be sent cross-origin
        * `Access-Control-Max-Age` - How long until you need to make another pre-flighted request
    * "Simple requests" do not trigger a pre-flight request
        * Methods: `GET`, `HEAD`, `POST`
    * All other requests trigger a pre-flight request which is an HTTP `OPTIONS` request to determine the CORS requirements of the cross-origin site being requested
* Security Headers
    * X-Frame-Options
        * Controls the ability for other websites to frame your content
        * `deny` - Cannot render within a frame
        * `sameorigin` - Can only frame from the same origin
        * `allow-from: DOMAIN` - Allows framing only from DOMAIN
    * HTTP Strict Transport Security (HSTS)
        * Controls whether a site should ONLY be loaded via HTTPS
        * Only works over HTTPS connections, HTTP connections ignore this header
    * X-XSS-Protection
        * Controls the XSS auditor in the browser
        * `0` - Auditor is disabled
        * `1` - Auditor is enabled, will attempt to sanitize attacks
        * `1; mode=block` - Auditor is enabled, will block rendering of pages containing XSS attacks
        * `1; report=https://url/to/report-to` - Auditor is enabled, will sanitize attacks and report to the URL provided
    * X-Content-Type-Options
        * Controls whether the browser will attempt to MIME-sniff the content and adjust the MIME-type on-the-fly
        * `nosniff` - Tells the browser to not guess the MIME-type of the content (even if it looks like something else)
    * Content-Security-Policy (CSP)
        * Controls many aspects of the security of your page and can prevent multiple types of security issues. It also means CSP can also drastically break your website, so test thoroughly and extensively.
* Subresource Integrity (SRI)
    * Ensures content fetched by your browser matches a cryptographic hash
    * Extremely useful when fetching JS/CSS payloads from a CDN or resource you do not control
* Content Security Policy
