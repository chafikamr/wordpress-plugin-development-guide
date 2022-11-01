## create new table 
````php
   global $wpdb;

    $tableName = $wpdb->prefix . 'devplugin';
    $charset_collate = $wpdb->get_charset_collate();
   
   
    $query = "CREATE TABLE  $tableName (
       
       id mediumint(9) NOT NULL AUTO_INCREMENT,
  time datetime DEFAULT '0000-00-00 00:00:00' NOT NULL,
  name tinytext NOT NULL,
  text text NOT NULL,
  url varchar(55) DEFAULT '' NOT NULL,
  PRIMARY KEY  (id))";
   
   
       require_once(ABSPATH.'wp-admin/includes/upgrade.php');
   dbDelta($query);
````
## get row 
````php 
$res =  $wpdb->get_row("SELECT * FROM {$wpdb->prefix}posts WHERE post_name ='hello-world';",'ARRAY_A');
// https://developer.wordpress.org/reference/classes/wpdb/#select-a-row




````
