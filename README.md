# Wordpress Configurations
These are the configurations I am doing for my WordPress website projects.

## Register style.css file to the WordPress

```php
/* Add style.css file Start */
function load_scripts() {
    wp_enqueue_style( 'stylecss', get_stylesheet_uri() );  
}
add_action('wp_enqueue_scripts', 'load_scripts' );
/* Add style.css file end */
```

## Disable Auto-updates

Disable WordPress Core Updates.
```php
define('WP_AUTO_UPDATE_CORE', false);
```
Disable WordPress Theme & PluginsUpdates.
```php
add_filter('auto_update_plugin', '__return_false');
add_filter('auto_update_theme', '__return_false');
```
## Change wp_mail reply-to address.

Simply copy and paste this snippet into `funtion.php` file in the theme editor. On **line 8**, you’ll need to replace `Your Name` and `youremail@example.com` with your desired reply-to name and email address.

```php
/* Change wp_mail reply-to mail address start */
function wp_mail_smtp_dev_reply_to( $args ) {

    $reply_to = 'Reply-To: Your Name <youremail@example.com>';
  
    if ( ! empty( $args[ 'headers' ] ) ) {
        if ( ! is_array( $args[ 'headers' ] ) ) {
            $args[ 'headers' ] = array_filter( explode( "\n", str_replace( "\r\n", "\n", $args[ 'headers' ] ) ) );
    }
  
    // Filter out all other Reply-To headers.
    $args[ 'headers' ] = array_filter( $args[ 'headers' ], function ( $header ) {
        return strpos( strtolower( $header ), 'reply-to' ) !== 0;
    } );
    } else {
        $args[ 'headers' ] = [];
    }
 
    $args[ 'headers' ][] = $reply_to;
    return $args;
}
add_filter( 'wp_mail', 'wp_mail_smtp_dev_reply_to', PHP_INT_MAX );
/* Change wp_mail reply-to mail address end */
```