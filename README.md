# Website Performance Checklist

The tolerance of people for poor experience is declining over time and most of them will bounce from your website if it doesn't load in the first few seconds. Below are few measures that can increase the performance of your website.

<br>

### 1. Compress components with gzip

If your hosting provider has mod_gzip module enabled, the best way to compress your content is to add the following lines to your `.htaccess` file:

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

Or use Gzip, a software application for file compression, to reduce the size of your CSS, HTML, and JavaScript files that are larger than 150 bytes.

### 2. Add expire headers

Simply download the `.htaccess file` from the root of your host (it may be hidden) and add the code below:

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

### 4. Make fewer HTTP requests

- Combine CSS/JS files into a single file.
- Remove unnecessary plug-ins.
- Remove assets you do not need
- Enable lazy load

### 5. Avoid empty src or href

Avoid `<video poster="">`, `<script src="">` etc.

### 6. Minify HTML, CSS and JS

To minify JS, CSS and HTML files, comments and extra spaces need to be removed, as well as crunch variable names so as to minimize code and reduce file size. The minified file version provides the same functionality while reducing the bandwidth of network requests.

### 7. Specify image dimensions

Include height and weight of images.

```
<img src="image.jpg" width="200" height="200" />
```

### 8. Handle bad requests

Ensure all requests have a proper response and does not yield 404 or 410 status codes.

### 9. Defer parsing of JavaScript

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

### 10. Use a CDN

Content delivery networks are faster for loading styles and scripts.

### 11. Remove duplicate or unused CSS and JS

Remove unwanted and duplicate code in styles and scripts.

### 12. Reduce the number of DOM elements

A complex page means more bytes to download, and it also means slower DOM access in JavaScript.

### 13. Use cookie free domains

Try to avoid use of cookies. If you are using them, remember to set a cookie policy.

### 14. Enable keep-alive

Include the following lines in your `.htaccess` file.

```
<IfModule mod_headers.c>
    Header set Connection keep-alive
</IfModule>
```

### 15. Avoid inline CSS and JS

Use class and scripts.

### 16. Optimize images

Images size should be optimal. A high resolution image is sometimes unnecessary.

### 17. Optimize the order of styles and scripts

Relevant stylesheets should be loaded first. Scripts can be loaded at the bottom.

### 18. Combine images using CSS sprites

CSS sprites technique is a way to reduce the number of HTTP requests made for image resources, by combining images in a single file.

### 19. Avoid CSS @imports

Imports blocks parellel loading and reduce load speed. Instead, use link tags.

Replace,

```css
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100&display=swap');
```

with,

```html
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@100&display=swap" rel="stylesheet"> 
```

### 20. Specify a character set early

Include the following lines in your `.htaccess` file. 

```
AddType 'text/html; charset=UTF-8' html
```

And avoid character set in meta tag.

Remove `<meta http-equiv="content-type" content="text/html;charset=UTF-8">`

### 21. Specify a Vary:Accept-Encoding header

Include the following lines in your `.htaccess` file. 

```
<IfModule mod_headers.c>
  <FilesMatch ".(js|css|xml|gz|html)$">
    Header append Vary: Accept-Encoding
  </FilesMatch>
</IfModule>
```

### 22. Reduce CSS expressions

Avoid expressions like `color: expression( condition ? "black" : "white" );`

### 23. Include robots.txt

A robots.txt file tells search engine crawlers which URLs the crawler can access on your site. This is used mainly to avoid overloading your site with requests; it is not a mechanism for keeping a web page out of Google.

### 24. Include sitemap

A sitemap is a file where you provide information about the pages, videos, and other files on your site, and the relationships between them. Search engines like Google read this file to crawl your site more efficiently. A sitemap tells Google which pages and files you think are important in your site, and also provides valuable information about these files. For example, when the page was last updated and any alternate language versions of the page.

<br>

### Finally,
___

Once you're done with optimizations, head over to the below tools to test your website. They will analyze the web page and gives you a detailed report along with improvement opportunities.

- https://tools.pingdom.com/
- https://gtmetrix.com/
- https://developers.google.com/speed/pagespeed/insights/
- https://www.webpagetest.org/
- https://www.dareboost.com/en
- https://www.dotcom-tools.com/website-speed-test
- https://www.seobility.net/en/seocheck/
- https://www.git-tower.com/blog/seo-for-developers/
