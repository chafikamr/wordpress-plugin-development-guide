### uninstall.php file 

Your plugin may need to do some clean-up when it is uninstalled from a site.<br/>

A plugin is considered uninstalled if a user has deactivated the plugin, and then clicks the delete link within the WordPress Admin.<br/>

When your plugin is uninstalled, you’ll want to clear out any plugin options and/or settings specific to to the plugin, and/or other database entities such as tables.<br/>
To use this method you need to create an <b>uninstall.php</b> file inside the root folder of your plugin. This magic file is run automatically when the users deletes the plugin.

For example: <b>/plugin-name/uninstall.php</b>
````php


// if uninstall.php is not called by WordPress, die
if (!defined('WP_UNINSTALL_PLUGIN')) {
    die;
}

$option_name = 'wporg_option';

delete_option($option_name);

// for site options in Multisite
delete_site_option($option_name);

// drop a custom database table
global $wpdb;
$wpdb->query("DROP TABLE IF EXISTS {$wpdb->prefix}mytable");

````
