# apache
Domain Redirect<br/>
URL Rewrite<br/>
gzip compression<br/>
cache<br/>
ip to domain<br/>
http to www<br/>
http to https<br/>
Block ip<br/>
Remove File Extension<br/>
Folder Rename<br/>



<IfModule mod_rewrite.c>
RewriteEngine On

#http to https
RewriteCond %{SERVER_PORT} 80
RewriteCond %{HTTP_HOST} ^www\.abc\.org$
RewriteRule (.*) http://www.abc.org/$1 [R=301,L]

# Ip to Domain

#RewriteCond %{HTTP_HOST} ^103\.21\.59\.171
#RewriteRule (.*) https://www.abc.org/$1 [R=301,L]

# http to www
RewriteCond %{HTTP_HOST} ^abc.org [NC]
RewriteRule ^(.*)$ http://www.abc.org/$1 [L,R=301]

RewriteCond %{HTTP_USER_AGENT} libwww-perl.* 
RewriteRule .* ? [F,L]
Options +FollowSymlinks -Multiviews
# Prevent Directoy listing 
Options -Indexes

# Remove file .php extension start
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME}.php -f
RewriteRule ^(.*)$ $1.php [NC,L]

# Rename folder
RewriteRule ^folder/(.*) urlname/$1 
RewriteRule ^folder$ /urlname/ [L] 

</IfModule>
# Prevent Direct Access to files
<Files .htaccess>
order allow,deny
deny from all
</Files>

<FilesMatch "(?i)((\.tpl|\.ini|\.log|(?<!robots)\.txt))">
 Order deny,allow
 Deny from all
</FilesMatch>
# Remove file .php extension End
# Gzip start
<IfModule mod_deflate.c>
  # gzip Compress HTML, CSS, JavaScript, Text, XML and fonts
  AddOutputFilterByType DEFLATE application/javascript
  AddOutputFilterByType DEFLATE application/rss+xml
  AddOutputFilterByType DEFLATE application/vnd.ms-fontobject
  AddOutputFilterByType DEFLATE application/x-font
  AddOutputFilterByType DEFLATE application/x-font-opentype
  AddOutputFilterByType DEFLATE application/x-font-otf
  AddOutputFilterByType DEFLATE application/x-font-truetype
  AddOutputFilterByType DEFLATE application/x-font-ttf
  AddOutputFilterByType DEFLATE application/x-javascript
  AddOutputFilterByType DEFLATE application/xhtml+xml
  AddOutputFilterByType DEFLATE application/xml
  AddOutputFilterByType DEFLATE font/opentype
  AddOutputFilterByType DEFLATE font/otf
  AddOutputFilterByType DEFLATE font/ttf
  AddOutputFilterByType DEFLATE image/svg+xml
  AddOutputFilterByType DEFLATE image/x-icon
  AddOutputFilterByType DEFLATE text/css
  AddOutputFilterByType DEFLATE text/html
  AddOutputFilterByType DEFLATE text/javascript
  AddOutputFilterByType DEFLATE text/plain
  AddOutputFilterByType DEFLATE text/xml

  # Remove browser bugs (only needed for really old browsers)
  BrowserMatch ^Mozilla/4 gzip-only-text/html
  BrowserMatch ^Mozilla/4\.0[678] no-gzip
  BrowserMatch \bMSIE !no-gzip !gzip-only-text/html
  Header append Vary User-Agent
</IfModule>

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


# Gzip End
## EXPIRES CACHING ##
<IfModule mod_expires.c>
# Enable expirations
ExpiresActive On 
# Default directive
ExpiresDefault "access plus 1 month"
# My favicon
ExpiresByType image/x-icon "access plus 1 year"
# Images
ExpiresByType image/gif "access plus 1 month"
ExpiresByType image/png "access plus 1 month"
ExpiresByType image/jpg "access plus 1 month"
ExpiresByType image/jpeg "access plus 1 month"
# CSS
ExpiresByType text/css "access plus 1 month"
# Javascript
ExpiresByType application/javascript "access plus 1 year"
</IfModule>


<IfModule mod_expires.c>
</IfModule>
## EXPIRES CACHING ##
<IfModule mod_suphp.c>
suPHP_ConfigPath /home3/arcjovdb
<Files php.ini>
order allow,deny
deny from all
</Files>
</IfModule>
<Files ~ "^.*\.([Hh][Tt][Aa])">
 order allow,deny
 deny from all
 satisfy all
</Files>
<Files 403.shtml>
order allow,deny
allow from all
</Files>

deny from 91.78.27.170
