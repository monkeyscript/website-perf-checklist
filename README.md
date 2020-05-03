# Website Performance Checklist

The tolerance of people for poor experience is declining over time and most of them will bounce from your website if it doesn't load in the first few seconds. Below are few measures that can increase the performance of your website.

### 1. Compress components with gzip

Include the following lines in your `.htaccess` file.

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

### 2. Add expire headers (Browser caching)

Include the following lines in your `.htaccess` file.

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

### 3. Avoid URL redirects

Include the following lines in your `.htaccess` file.

```
RewriteEngine On

RewriteCond %{HTTP_HOST} ^www.example.com [NC]
RewriteRule (.*)$ http://example.com/$1 [R=301,L]
```

### 4. Reduce DNS lookups

Built over time by domain authority and other factors.

### 5. Make fewer HTTP requests

Reduce number of files i.e. combine css, js etc.

### 6. Avoid empty src or href

Avoid `<video poster="">`, `<script src="">` etc.

### 7. Minify HTML, CSS and JS

Minify all files thus reducing file size.

### 8. Specify image dimensions

Include height and weight of images.

```
<img src="image.jpg" width="200" height="200" />
```

### 9. Avoid bad requests

Ensure all requests have a proper response and does not yield 404 or 410 status codes.

### 10. Defer parsing of JavaScript

Javascript parsing will block all other process. Therefore a bulk code can slow down the rendering. Use the following code to delay the parsing.

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

### 11. Use a CDN

Content delivery networks are faster for loading styles and scripts.

### 12. Make AJAX cacheable

Make use of Cache-Control and Future-Expire headers.

### 13. Remove duplicate or unused CSS and JS

Remove unwanted and duplicate code in styles and scripts.

### 14. Reduce the number of DOM elements

A complex page means more bytes to download, and it also means slower DOM access in JavaScript.

### 15. Use cookie free domains

Try to avoid use of cookies. If you are using them, remember to set a cookie policy.

### 16. Enable keep-alive

Include the following lines in your `.htaccess` file.

```
<IfModule mod_headers.c>
    Header set Connection keep-alive
</IfModule>
```

### 17. Inline small CSS and JS

Use class and scripts.

### 18. Optimize images

Images size should be optimal. A high resolution image is sometimes unnecessary.

### 19. Optimize the order of styles and scripts

Relevant stylesheets should be loaded first. Scripts can be loaded at the bottom.

### 20. Serve resources from a consistent URL

If you are using CDN, make sure they're reliable.

### 21. Serve scaled images

Scale images from server side to specifed dimension to avoid delay.

### 22. Specify a cache validator

Include the following lines in your `.htaccess` file.

```
<filesMatch ".(ico|pdf|flv|jpg|jpeg|png|gif|js|css|swf)$">
    Header set Cache-Control "max-age=604800, public"
</filesMatch>
```

### 23. Combine images using CSS sprites

### 24. Avoid CSS @imports

### 25. Prefer asynchronous resources

### 26. Specify a character set early

Include the following lines in your `.htaccess` file. 

```
AddType 'text/html; charset=UTF-8' html
```

And avoid character set in meta tag.

Avoid `<meta http-equiv="content-type" content="text/html;charset=UTF-8">`

### 27. Specify a Vary:Accept-Encoding header

Include the following lines in your `.htaccess` file. 

```
<IfModule mod_headers.c>
  <FilesMatch ".(js|css|xml|gz|html)$">
    Header append Vary: Accept-Encoding
  </FilesMatch>
</IfModule>
```

### 28. Use GET for AJAX requests

Avoid POST calls.

### 29. Avoid CSS expressions

Remove expression like `color: expression( condition ? "black" : "white" );`

### 30. Reduce cookie size

Minimize their size small as posible to avoid large request headers.

### 31. Make favicon small and cacheable

Include the following lines in your `.htaccess` file. 

```
<filesMatch ".(ico|pdf|flv|jpg|jpeg|png|gif|js|css|swf)$">
    Header set Cache-Control "max-age=84600, public"
</filesMatch>
```

### 32. Make CSS and JS external

### 33. Eliminate render blocking resources

### 34. Minimize main thread work

### 35. Reduce JS execution time

### 36. Defer offscreen images

Load them once the initial loading is complete.

### 37. Include robots.txt file

Include a robots.txt file.

### 38. Include sitemap

Include a sitemap file.

### 39. Use proper URL

Try to include a keyword in URL and avoid self-generated ugly URLs.

### 40. Proper heading hierarchy

Only one h1 per page. Two or three h2 and so on.