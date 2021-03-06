# Wordpress Notes
## Errors
* *WordPress database error  for query SHOW FULL COLUMNS FROM*
    * *Found it... Security patch in 4.1.2 added a new function, 'wpdb->process_field_lengths()', that causes an insert or update query not to be run if the data is longer than the permissible size based on the database schema.*
    * [Error fix](https://github.com/andyplak/events-manager-pro-sage-pay/issues/19)

## API Notes
* Configure headers for API Rest Calls
* [Access Control Headers for Wordpress Rest API](https://joshpress.net/access-control-headers-for-the-wordpress-rest-api/)
    * Added below code to plugin startup file. Let's one change headers and permissions.
```php
/**
 * Use * for origin
 */
 add_action( 'rest_api_init', function() {

 remove_filter( 'rest_pre_serve_request', 'rest_send_cors_headers' );
 add_filter( 'rest_pre_serve_request', function( $value ) {
 	header( 'Access-Control-Allow-Origin: *' );
 	header( 'Access-Control-Allow-Methods: POST, GET, OPTIONS, PUT, DELETE' );
 	header( 'Access-Control-Allow-Credentials: true' );
 	header( 'Access-Control-Expose-Headers: X-WP-Total, X-WP-TotalPages, PAS-Fingerprint, PAS-Check, PAS-Nonce, PAS-Captcha');
 	header('Access-Control-Allow-Headers: Authorization, Content-Type, PAS-Nonce, PAS-Fingerprint, PAS-Check');
 	return $value;
 });
 }, 15 );
```
## Wordpress Resources
* [WP Hasty](https://www.wp-hasty.com/)
* Using jquery-ui with wordpress. 
    * [How to use jquery-ui in Wordpress](http://jafty.com/blog/tag/how-to-use-jquery-ui-in-wordpress/)


## Setting up S3 Plugin
* [S3 Uploads Plugin](https://github.com/humanmade/S3-Uploads) - made by [Human Made](https://hmn.md/).
* Using Composer with S3.
```json
"require": {
    "humanmade/s3-uploads":"dev-master"
}
"repositories": [
    {
      "type": "vcs",
      "url": "https://github.com/humanmade/S3-Uploads.git"
    }
]
```
* Setup S3 Bucket
    * bucket name
* Edit wp-config.php
```php
define( 'S3_UPLOADS_BUCKET', 'my-bucket' );
define( 'S3_UPLOADS_KEY', '' );
define( 'S3_UPLOADS_SECRET', '' );
define( 'S3_UPLOADS_REGION', '' );
```

* need wp-cli installed
* Be sure to be in public folder
* verify - `wp s3-uploads verify`
* enable - `wp s3-uploads enable`

