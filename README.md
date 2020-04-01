# Website Performance Checklist

#### Compress components with gzip
```
<ifModule mod_gzip.c>
    mod_gzip_on Yes
    mod_gzip_dechunk Yes
    mod_gzip_item_include file .(html?|txt|css|js|php|pl)$
    mod_gzip_item_include handler ^cgi-script$
    mod_gzip_item_include mime ^text/.*
    mod_gzip_item_include mime ^application/x-javascript.*
    mod_gzip_item_exclude mime ^image/.*
    mod_gzip_item_exclude rspheader ^Content-Encoding:.*gzip.*
</ifModule>
```

#### Add expire headers (Browser caching)
```
<IfModule mod_expires.c>
  ExpiresActive On

  # Images
  ExpiresByType image/jpeg "access plus 1 year"
  ExpiresByType image/gif "access plus 1 year"
  ExpiresByType image/png "access plus 1 year"
  ExpiresByType image/webp "access plus 1 year"
  ExpiresByType image/svg+xml "access plus 1 year"
  ExpiresByType image/x-icon "access plus 1 year"

  # Video
  ExpiresByType video/mp4 "access plus 1 year"
  ExpiresByType video/mpeg "access plus 1 year"

  # CSS, JavaScript
  ExpiresByType text/css "access plus 1 month"
  ExpiresByType text/javascript "access plus 1 month"
  ExpiresByType application/javascript "access plus 1 month"

  # Others
  ExpiresByType application/pdf "access plus 1 month"
  ExpiresByType application/x-shockwave-flash "access plus 1 month"
  ExpiresDefault "access 2 days"
</IfModule>
```

#### Avoid URL redirects
```
RewriteEngine On

RewriteCond %{HTTP_HOST} ^www.example.com [NC]
RewriteRule (.*)$ http://example.com/$1 [R=301,L]
```

#### Reduce DNS lookups

Built over time by domain authority and other factors.

#### Make fewer HTTP requests

Reduce number of files i.e. combine css, js etc.

#### Avoid empty src or href

Avoid `<video poster="">`, `<script src="">` etc.

#### Minify HTML, CSS and JS

Minify all files thus reducing file size.

#### Specify image dimensions
```
<img src="image.jpg" width="200" height="200" />
```

#### Avoid bad requests

Ensure all requests have a proper response and does not yield 404 or 410 status codes.

#### Defer parsing of JavaScript
```
<script type="text/javascript">
    function downloadJSAtOnload() {
        var element = document.createElement("script");
        element.src = "example.js";
        document.body.appendChild(element);
    }
    if (window.addEventListener)
        window.addEventListener("load", downloadJSAtOnload, false);
    else if (window.attachEvent)
        window.attachEvent("onload", downloadJSAtOnload);
    else window.onload = downloadJSAtOnload;
</script>
```

#### Use a CDN

Content delivery networks are faster for loading styles and scripts.

#### Make AJAX cacheable

Make use of Cache-Control and Future-Expire headers.

#### Remove duplicate or unused CSS and JS

Remove unwanted and duplicate code in styles and scripts.

#### Reduce the number of DOM elements

A complex page means more bytes to download, and it also means slower DOM access in JavaScript.

#### Use cookie free domains

Try to avoid use of cookies. If you are using them, remember to set a cookie policy.

#### Enable keep-alive
```
<IfModule mod_headers.c>
    Header set Connection keep-alive
</IfModule>
```

#### Inline small CSS and JS

Use class and scripts.

#### Minimize redirects

#### Minimize request size

#### Optimize images

#### Optimize the order of styles and scripts

#### Put CSS in the document head

#### Serve resources from a consistent URL

#### Serve scaled images

#### Specify a cache validator
```
<filesMatch ".(ico|pdf|flv|jpg|jpeg|png|gif|js|css|swf)$">
    Header set Cache-Control "max-age=604800, public"
</filesMatch>
```

#### Combine images using CSS sprites

#### Avoid CSS @imports

#### Prefer asynchronous resources

#### Specify a character set early
```
AddType 'text/html; charset=UTF-8' html
```

#### Avoid a character set in meta tag

Avoid `<meta http-equiv="content-type" content="text/html;charset=UTF-8">`

and use the below in .htaccess,

```
AddType 'text/html; charset=UTF-8' html
```

#### Specify a Vary:Accept-Encoding header
```
<IfModule mod_headers.c>
  <FilesMatch ".(js|css|xml|gz|html)$">
    Header append Vary: Accept-Encoding
  </FilesMatch>
</IfModule>
```

#### Use GET for AJAX requests

Avoid POST calls.

#### Avoid CSS expressions

Remove expression like `color: expression( condition ? "black" : "white" );`

#### Reduce cookie size

Minimize their size small as posible to avoid large request headers.

#### Make favicon small and cacheable

```
<filesMatch ".(ico|pdf|flv|jpg|jpeg|png|gif|js|css|swf)$">
    Header set Cache-Control "max-age=84600, public"
</filesMatch>
```

#### Make CSS and JS external

#### Eliminate render blocking resources

#### Minimize main thread work

#### Reduce JS execution time

#### Defer offscreen images

#### Include robots.txt file

#### Include sitemap