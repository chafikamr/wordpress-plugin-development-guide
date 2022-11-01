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
