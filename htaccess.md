# Redirects
_These will work on  Cloudways or WP Engine. For other hosting, may need to change the https test condition (see below)._

## Force SSL and REMOVE the "www"
```
# Force SSL and remove www
RewriteEngine on
RewriteCond %{HTTP_HOST} ^www. [NC,OR]
RewriteCond %{HTTP:X-Forwarded-Proto} !https
RewriteRule ^(.*)$ https://DOMAIN.com/$1 [L,R=301]
```

## Force SSL and ADD the "www"
```
# Force SSL and add www 
RewriteEngine on
RewriteCond %{HTTP_HOST} !^www. [NC,OR]
RewriteCond %{HTTP:X-Forwarded-Proto} !https
RewriteRule ^(.*)$ https://www.DOMAIN.com/$1 [L,R=301]
```

## Force SSL
```
RewriteEngine On
RewriteCond %{HTTP:X-Forwarded-Proto} !https
RewriteRule ^(.*)$ https://%{HTTP_HOST}/$1 [R=301,L]
```

## Alternate ways to check for SSL
_This works on GoDaddy / Hostgator.
Do NOT use on WP Engine!_
```
RewriteCond %{SERVER_PORT} 80 
```
_Use this on Siteground / Bluehost / iPower._
```
RewriteCond %{HTTPS} off
```

## Redirect old permalink structures with RewriteRule, not RedirectMatch so it is processed in the correct order. 
_Put the appropriate one above the "Force SSL and STRIP www" rules so it is processed first._

### /year/month/postname/ -> /postname/
```
# Redirect old permalink structure /year/month/ 
RewriteEngine on
RewriteCond %{REQUEST_URI} ^/([0-9]{4})/([0-9]{2})/([^/]+)/? [NC]
RewriteRule ^(.*)$ https://www.DOMAIN.com/%3/ [L,R=301]
```

### /year/month/day/postname/ -> /postname/
```
## Redirect old permalink structure /year/month/day/ 
RewriteEngine on
RewriteCond %{REQUEST_URI} ^/([0-9]{4})/([0-9]{2})/([0-9]{2})/([^/]+)/? [NC]
RewriteRule ^(.*)$ https://www.DOMAIN.com/%4/ [L,R=301]
```

### /year/month/postname.html -> /postname/
```
# Redirect old permalink structure /%year%/%monthnum%/%postname%.html
RewriteEngine on
RewriteCond %{REQUEST_URI} ^/([0-9]{4})/([0-9]{2})/(.*)\.html [NC]
RewriteRule ^(.*)$ https://www.DOMAIN.com/%3/ [L,R=301]
```
## Redirect /amp/ URLs back to original
```
# Redirect /amp/ URLs back to original
# Homepage
RewriteEngine On
RewriteCond %{REQUEST_URI} ^/amp/?$
RewriteRule ^(.*) https://WWW.DOMAIN.com/ [L,R=301]
# All other pages
RewriteEngine On
RewriteCond %{REQUEST_URI} /amp/?$
RewriteRule ^(.*)/amp https://WWW.DOMAIN.com/$1/ [L,R=301]
```
## Full site redirect (use after a domain change)
```
# Redirect old domain
RewriteEngine on
RewriteCond %{HTTP_HOST} ^domain.com [NC,OR]
RewriteCond %{HTTP_HOST} ^www.domain.com [NC]
RewriteRule ^(.*)$ http://DOMNAIN.COM/$1 [L,R=301,NC]
```

# Security Stuff

## Extra Security Headers
_Use this for Mediavine Sites, after disabling "Extra Security Headers" in the Sucuri Firewall settings_
```
# Extra Security Headers
<IfModule mod_headers.c>
	Header set Content-Security-Policy: block-all-mixed-content
	Header set X-XSS-Protection "1; mode=block"
	Header always append X-Frame-Options SAMEORIGIN
	Header set X-Content-Type-Options nosniff
</IfModule>
```

## Content Security Policy to Block Mixed Content. 
_https://help.mediavine.com/mediavine-learning-resources/force-all-ads-secure-with-a-content-security-policy_
```
# Set Content Security Policy to Block Mixed Content. 
Header set Content-Security-Policy: block-all-mixed-content
```
## Prevent Sucuri Firewall Bypass
```
# Prevent Sucuri Firewall Bypass
<FilesMatch ".*">
    Order deny,allow
    Deny from all
    Allow from 192.88.134.0/23
    Allow from 185.93.228.0/22
    Allow from 2a02:fe80::/29
    Allow from 66.248.200.0/22
    Allow from 208.109.0.0/22
</FilesMatch>
```
## Protect wp-config.php
```
# Protect wp-config.php
<files wp-config.php>
order allow,deny
deny from all
</files>
```
## Block specific IP access

```
# Block specific IP access
Deny from 91.200.12.18
```

# Return 404s from Server instead of loading WordPress

```
# Use default server 404 error instead of WordPress error for missing static files
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f [OR]
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule \.(css|js|jpg|png|pdf|swf|jpeg|svg|gif|ico|txt|mp4|mp3)$ - [L,R=404]
```
```
# Use server 404 error instead of WordPress error for bad PDF URLs in root folder
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f [OR]
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)\.pdf$ - [L,R=404]
```
```
# Send hard 404 for evil timthumb scanners, before invoking WordPress
RewriteEngine on
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule (.*)thumb.php$ - [L,R=404]
```

# Miscellany

## Don't redirect for Let's Encrypt cert setup or renewal
_Add this line to a rewrite condition if wanting to NOT redirect for let's encrypt cert setup/renewal_
```
RewriteCond %{REQUEST_URI} !^/.well-known/
```

## Fix Pinterest Code Glitch. 
_"#_a5y_p=XXX" is being converted to "%23_a5y_p=XXX" which is causing 404s in Pinterest browser._
```
RewriteEngine on
RewriteRule ^(.*)\x23_a5y_p= https://domain.com/$1 [L,R=302,NE,NC]
```

##  Standard WordPress .htaccess block
```
# BEGIN WordPress
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteBase /
RewriteRule ^index\.php$ - [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.php [L]
</IfModule>
# END WordPress
```
