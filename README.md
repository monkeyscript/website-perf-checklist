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

#### Reduce DNS lookups

#### Make fewer HTTP requests

#### Avoid empty src or href

#### Minify HTML, CSS and JS

#### Specify image dimensions
```
<img src="image.jpg" width="200" height="200" />
```

#### Avoid bad requests

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

#### Make AJAX cacheable

#### Remove duplicate CSS and JS

#### Reduce the number of DOM elements

#### Use cookie free domains

#### Enable keep-alive
```
<IfModule mod_headers.c>
    Header set Connection keep-alive
</IfModule>
```

#### Inline small CSS and JS

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

#### Specify a Vary:Accept-Encoding header
```
<IfModule mod_headers.c>
  <FilesMatch ".(js|css|xml|gz|html)$">
    Header append Vary: Accept-Encoding
  </FilesMatch>
</IfModule>
```

#### Use GET for AJAX requests

#### Avoid CSS expressions

#### Reduce cookie size

#### Make favicon small and cacheable

#### Make CSS and JS external

#### Eliminate render blocking resources

#### Remove unused CSS

#### Minimize main thread work

#### Reduce JS execution time

#### Defer offscreen images