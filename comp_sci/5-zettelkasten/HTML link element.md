### Meta
- - -
- 2024-09-15 21:20
- Tags: [[html]] [[html elements]] [[html metadata]]
- Status: #completed 

### What it looks like
- - -
```HTML file:index.html
<link href="/media/examples/link-element-example.css" rel="stylesheet" />
```

### What it does
- - -
-  Specifies relationships between the current document and an external resource.
- Most commonly used to link stylesheets.

### Linking stylesheets
---
```HTML file:index.html
<link href="main.css" rel="stylesheet" />
```

### Linking icons
---
```HTML file:index.html
<link
  rel="apple-touch-icon"
  sizes="114x114"
  href="apple-icon-114.png"
  type="image/png" />
```

### Other usage
- - -
- A `<link>` element can occur either in the `<head>` or `<body>` element, depending on whether it has a [[link type]] that is **body-ok**. For example, a `stylesheet` link type is body-ok, but is NOT a good practice. It makes more sense to separate your `<link>` elements from your body content, putting them in the `<head>`.
- When using a `<link>` to establish a favicon for a site, and your site uses a [[Content Security Policy]] (CSP) to enhance its security, the policy applies to the favicon.  If you encounter problems with the favicon not loading, verify that the `CSP`'s header's [[img-src]] directive is not preventing access to it.
- The HTML and XHTML specs define event handlers for the `<link>` element, but it is unclear how they could be used.
- Under XHTML 1.0, [[void elements]] such as `<link>` require a trailing slash: `<link />`.
- WebTV supports the use of the value `next` for `rel` to preload the next page in a document series.

### Attributes
- - -
- `as`
	- Required when `rel="preload"` has been set on the `<link>` element.
	- Optional when `rel="modulepreload` has been set.
	- Otherwise should NOT be used.
	- Specifies the type of content being loaded by the `<link>`, which is necessary for request matching, application of correct `CSP`, and setting of correct [[Accept]] request header.
	- Furthermore, `rel="preload"` uses this a sign for request prioritization. The table below lists the valid values for this attribute and the elements or resources they apply to.


| **Value** | **Applies to**                                                                                                                          |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| audio     | `<audio>` elements                                                                                                                      |
| document  | `<iframe>` and `<frame>` elements                                                                                                       |
| embed     | `<embed>` elements                                                                                                                      |
| fetch     | fetch, XHR<br><br>**Note**: This value also requires `<link>` to contain the `crossorigin` attribute. See [[CORS-enabled fetches]].     |
| font      | CSS @font-face<br><br>**Note**: This value also requires `<link>` to contain the `crossorigin` attribute. See [[CORS-enabled fetches]]. |
| image     | `<img>` and `<picture>` elements with `srcset` or `imgset` attributes, SVG `<image>` elements, CSS `*-image` rules                      |
| object    | `<object>` elements                                                                                                                     |
| script    | `<script>` elements, Worker `importScripts`                                                                                             |
| style     | `<link rel=stylesheet>` elements, CSS `@import`                                                                                         |
| track     | `<track>` elements                                                                                                                      |
| video     | `<video>` elements                                                                                                                      |
| worker    | Worker, SharedWorker                                                                                                                    |
- `crossorigin`
	- This [[enumerated]] attribute indicates whether [[CORS]] must be used when fetching the resource. [[CORS-enabled images]] can be reused in the `<canvas>` element without being *tainted*. The allowed rules are:
		- `anonymous`
			- A cross-origin request (i.e. with an [[Origin HTTP header]]) is performed, but no credential is sent (i.e. no cookie, X.509 certificate, or HTTP Basic authentication). If the server does not give credentials to the origin site (by not accessing the [[Access-Control-Allow-Origin HTTP header]]) the resource will be tainted and its usage restricted.
		- `use-credentials`
			- A cross-origin request (i.e. with an [[Origin HTTP header]]) is performed along with a credential sent (i.e. no cookie, X.509 certificate, or HTTP Basic authentication). If the server does not give credentials to the origin site (by not accessing the [[Access-Control-Allow-Origin HTTP header]]) the resource will be tainted and its usage restricted.
	- If the attribute is not present, the resource is fetched without a [[CORS]] request (i.e. without sending the `Origin` HTTP header), preventing its non-tainted usage. If invalid, it is handled as if the enumerated keyword **anonymous** was used. See [[CORS settings attributes]] for more info.
- `disabled`
	- For `rel="stylesheet"` only, the `disabled` Boolean attribute indicates whether the described stylesheet should be loaded and applied to the document.
	- If present, the stylesheet will be loaded on-demand. 
	- If changed to `false` or removed, the stylesheet will be loaded during page load.
	- Setting this property in the DOM causes the stylesheet to be removed from the document's [[Document.styleSheets]] list.
- `fetchpriority`
	- Provides a hint of the relative priority to use when fetching a preloaded resources.
	- Allowed values:
		- `high`
			- Signals a high-priority fetch relative to other resources of the same type.
		- `low`
			- Signals a low-priority fetch relative to other resources of the same type.
		- `auto`
			- Default.
			- Signals automatic determination of fetch priority relative to other resources of the same type.
- `href`
	- specifies the absolute or relative [[URL]] of the linked resource.
- `hreflang`
	- Indicates the language of the linked resource.
	- It is purely advisory.
	- Use only if `href` is present.
- `imagesrcset`
	- For `rel="preload"` and `as="image"` only.
	- Is a [[sourceset attribute]] that indicates to preload the appropriate resource used by an `img` element with corresponding values for its `srcset` and `sizes` attributes.
- `integrity`
	- Contains inline metadata -- a base64-encoded cryptographic has of the source (file) you're telling the browser to fetch.
	- The browser can use this to verify that the fetched resource has been delivered without unexpected manipulation.
	- The attribute must only be specified when `rel` is `stylesheet`, `preload`, or `modulepreload`.
	- See [[Subresource Integrity]].
- `media`
	- specifies the media that the linked resource applies to.
	- Its value must be a media type or [[media query]].
	- Allows the user agent to pick the best adapted stylesheet for the device it runs on.
- `referrerpolicy`
	- A string indicating which referrer to use when fetching the resource:
		- `no-referrer` means that the [[Referrer]] header will not be sent.
		- `no-referrer-when-downgrade` means that no `Referrer` will be sent when navigating to an origin without TLS (HTTPS). This is a user agent's default behavior, if no policy is otherwise specified.
		- `origin` means the referrer will be the origin of the page, which is roughly the scheme, the host, and the port.
		- `origin-when-cross-origin` means that navigation to other origins will be limited to the scheme, the host, and the port, while navigating on the same origin will include the referrer's path.
		- `unsafe-url` means the referrer will include the origin and the path (but not the fragment, password, or username). This case is unsafe because it can leak origins and paths from TLS-protected resources to insecure origins.
- `rel`
	- Names a relationship of the linked document to the current document.
	- See more at [[HTML rel attribute]].
- `sizes`
	- Defines the sizes of the icons for visual media contained in the resource.
	- Required only when `rel` is of type `icon` or non-standard (e.g. `apple-touch-icon).
	- Values:
		- `any`, meaning the icon can be scaled at will as if it were a vector image such as `image/svg+xml`.
		- a white-space separated list of sizes, in the format `<width in pixels>x<height in pixels>`. Each of these sizes must be contained in the resource.
		- **Note:** Most icon formats are only able to store one single icon; therefore, most of the time, the `sizes` attribute contains only one entry. Microsoft's ICO format and Apple's ICNS format can store multiple icon sizes in a single file. ICO has better browser support, so you should use this format if cross-browser support is a concern. 
- `title`
	- Has special semantics on the `<link>` element.
	- When used on `rel="stylesheet"` links, it defines a [[default or alternate stylesheet]].

### Further reading
- - -
- [<link>: The External Resource Link element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/link)
