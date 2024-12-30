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