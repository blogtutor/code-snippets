# wp-config.php Tidbits

## Standard NerdPress Additions
```
// BEGIN NERDPRESS EDITS
define( 'DISALLOW_FILE_EDIT', true ); 
define( 'SUCURISCAN_HIDE_ADS', true ); 
define( 'WP_POST_REVISIONS', 10 ); 
define( 'FORCE_SSL_ADMIN', true ); 
#define( 'SHORTPIXEL_HIDE_API_KEY', true ); 
// END NERDPRESS EDITS
```

```
define( 'WP_MEMORY_LIMIT', '256M' );
```

## Enable Debug logging
_Saves debug.log in /wp-content/ folder_
```
# Enable Debug logging
define( 'WP_DEBUG', true );
if ( WP_DEBUG ) {
  define( 'WP_DEBUG_LOG', true );
  define( 'WP_DEBUG_DISPLAY', false );
  @ini_set( 'display_errors', 0 );
}
```

## Fix dashboard javascript issues
_Disabled concatenation of scripts in the admin dashboard_
```
define('CONCATENATE_SCRIPTS', false );
```

```
// Use X-Forwarded-For HTTP Header to Get Visitor's Real IP Address
if ( isset( $_SERVER['HTTP_X_FORWARDED_FOR'] ) ) {
	$http_x_headers_ajw = explode( ',', $_SERVER['HTTP_X_FORWARDED_FOR'] );

	$_SERVER['REMOTE_ADDR'] = $http_x_headers_ajw[0];
}
```
```
# VAULTPRES CONFIG TO WORK AROUND GENERIC REVERSE PROXY
# https://help.vaultpress.com/connection-issues/
if ( !empty( $_SERVER['HTTP_X_FORWARDED_FOR'] ) ) {
    $forwarded_ips = explode( ',', $_SERVER['HTTP_X_FORWARDED_FOR'] );
    $_SERVER['REMOTE_ADDR'] = $forwarded_ips[0];
    unset( $forwarded_ips );
}
```
```
# VAULTPRES CONFIG TO WORK AROUND CLOUDPROXY
if ( !empty( $_SERVER['HTTP_X_SUCURI_CLIENTIP'] ) ) {
    $forwarded_ips = explode( ',', $_SERVER['HTTP_X_SUCURI_CLIENTIP'] );
    $_SERVER['REMOTE_ADDR'] = $forwarded_ips[0];
    unset( $forwarded_ips );
}
```
```
# FIX WOOCOMMERCE NOT SEEING REAL IP ADDRESS - WITH CLOUDPROXY ON CLOUDWAYS
if (isset($_SERVER['HTTP_X_SUCURI_CLIENTIP']))
{
    $_SERVER["HTTP_X_REAL_IP"] = $_SERVER['HTTP_X_SUCURI_CLIENTIP'];
}
```
```
# FIX JETPACK LOCKOUT SCREENS FOR CLOUDPROXY
if (isset($_SERVER['HTTP_X_SUCURI_CLIENTIP'])) {
	$_SERVER["HTTP_X_REAL_IP"] = $_SERVER['HTTP_X_SUCURI_CLIENTIP'];
	
    $forwarded_ips = explode( ',', $_SERVER['HTTP_X_SUCURI_CLIENTIP'] );
    $_SERVER['REMOTE_ADDR'] = $forwarded_ips[0];
    unset( $forwarded_ips );	
}
```
```
# FIX JETPACK LOCKOUT SCREENS FOR CLOUDFLARE ORANGE CLOUD ENABLED
if (isset($_SERVER['HTTP_CF_CONNECTING_IP'])) {
	$_SERVER["HTTP_X_REAL_IP"] = $_SERVER['HTTP_CF_CONNECTING_IP'];
	
    $forwarded_ips = explode( ',', $_SERVER['HTTP_CF_CONNECTING_IP'] );
    $_SERVER['REMOTE_ADDR'] = $forwarded_ips[0];
    unset( $forwarded_ips );	
}
```

## Fix redirect loop when trying to run all-SSL
```
# Fix redirect loop when trying to run all-SSL
if (strpos($_SERVER['HTTP_X_FORWARDED_PROTO'], 'https') !== false)  
    $_SERVER['HTTPS']='on';
```


## Override Site URL and Home Settings
```
define( 'WP_SITEURL', 'https://domain.com' );
define( 'WP_HOME', 'https://domain.com' );
```

```
# Set Site/Home to whatever URL the site is using	
define('SP_REQUEST_URL', ($_SERVER['HTTPS'] ? 'https://' : 'http://') . $_SERVER['HTTP_HOST']);
define('WP_SITEURL', SP_REQUEST_URL);
define('WP_HOME', SP_REQUEST_URL);
```
