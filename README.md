# Website Performance Checklist

The tolerance of people for poor experience is declining over time and most of them will bounce from your website if it doesn't load in the first few seconds. Below are few measures that can increase the performance of your website.

### 1. Compress components with gzip

Include the following lines in your `.htaccess` file. Make sure your hosting service has support for compression.

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

Include the following lines in your `.htaccess` file. This will enable caching of our page assets in browsers for the specified time interval.

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

Sprites are two-dimensional images which are made up of combining small images into one larger image at defined X and Y coordinates.

### 24. Avoid CSS @imports

Imports blocks parellel loading and reduce load speed.

### 25. Prefer asynchronous resources

Parellel or async loading reduce load time.

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

Remove inline css and use external CSS files.

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

### 41. Configure ET tags


### 42.From reducing bottlenecks to getting the most website speed out of your dedicated server, these tips will put you on track for a fast environment.


### 43. Optimize MySQL
Databases tend to get larger as your website grows, and queries take longer to execute due to vast amounts of data being stored. You’ll want to tweak your MySQL settings to increase overall speed of your database server, and take advantage of indexes to reduce the time a query needs to run. A properly configured my.cnf file will also go a long way when optimizing your MySQL server. For most servers, MySQL tends to be the biggest bottleneck; so you’ll want to place a lot of focus improving the reliability and speed of your MySQL queries.

Index frequently accessed data. When you know a table is going to be accessed a lot, it’s best to create the index as soon as you create the table. Tables that store a lot of information will benefit from indexes because it will speed up the time to perform queries when the data needs to be retrieved. The following example is how you create an indexed table for people storing their name, date of birth, and a unique ID.
```
CREATE TABLE people (
name VARCHAR(32),
dob DATE,
unique INT, INDEX (id)
)
```

Creating indexes can be done during the table’s creation, or after the table is created. It can also be managed through PHP while generating new unique tables that will be accessed frequently. To add an index to an existing table, the following would be used.
```
ALTER TABLE people (
ADD INDEX id(unique),
ADD INDEX name(name);
)
```

These methods are very simple, and large tables should always be indexed when there’re a lot of requests to retrieve data.

Consider modifying the default my.cnf file often located in /etc/my.cnf. Don’t forget to make a backup. Each configuration will be unique to each distribution, so read up on MySQL and find the best settings for your server. If you have dedicated server management with us, our level 3 techs will give you the best configuration for your server. Tell us about your environment, and submit a ticket and let us speed up your server’s performance.

### 44.Optimize PHP & Apache
Apache and PHP are both highly scalable in most environments, and are very powerful options to consider when deploying a dedicated server; however they both come with most modules and extensions enabled by default. You’ll want to fine tune your configuration to get the most speed out of your server, so you’ll have to make a few changes to your setup.

If you don’t need PHP and plan on serving mostly static pages, you can safely remove PHP from your configuration altogether. If however you do plan on running PHP scripts on your server, consider disabling unnecessary extensions by commenting them out in your php.ini or removing them from PHP entirely. There’re also many PHP extensions intended for speeding up the performance of PHP. Each has it’s own user case and may require certain functions to be called during execution, so research what works best for you. Caching and code optimizers should be options you would want to implement in your distribution. Don’t forget to configure the memory settings in your php.ini file as that will yield a substantial amount of benefits if you have, or are expecting heavy traffic.

When tuning Apache, you’ll want to pay attention to a few settings. KeepAlive, and MaxClients in particular. These options are situational to your web server so find some resources on the Apache Website. Tweaking one setting could substantially increase the speed of your server.

### tip 45.KeepAlive: Allows clients to reuse the same connection to facilitate the transfer of multiple files.
Note: KeepAlive comes with increased memory use.
MaxClients: Determines the maximum number of concurrent clients / connections that Apache will serve.
Note: MaxClients comes with the risk of Syn Floods if set too high..
A good PHP configuration and well tuned Apache configuration will result in a very fast dedicated server. There’re many settings to go over which are out of the scope of this article, so read a little bit about Apache and PHP to get a solid understanding, or look into our server management and let us handle the hard work for you.

Speeding Up a Dedicated Server
### summary::To summarize, make your site run faster with these tips:

# Optimize MySQL, and don’t forget the indexes!
# Each Apache configuration will be unique to every deployment.
# Disable unnecessary PHP extensions and fine tune memory use and other settings in the php.ini file.
# Optimize your files and reuse as much as possible to leverage browser storage.
CSS first, JavaScript last.
