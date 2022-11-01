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

## Execute query 
````php

$fivesdrafts = $wpdb->get_results(
	"
		SELECT ID, post_title
		FROM $wpdb->posts
		WHERE post_status = 'draft'
		AND post_author = 5
	"
);

foreach ( $fivesdrafts as $fivesdraft ) {
	echo $fivesdraft->post_title;
}



````

 ## get var
 
 ````php
 
public function get_var( $query = null, $x = 0, $y = 0 ) {
	$this->func_call = "\$db->get_var(\"$query\", $x, $y)";

	if ( $query ) {
		if ( $this->check_current_query && $this->check_safe_collation( $query ) ) {
			$this->check_current_query = false;
		}

		$this->query( $query );
	}

	// Extract var out of cached results based on x,y vals.
	if ( ! empty( $this->last_result[ $y ] ) ) {
		$values = array_values( get_object_vars( $this->last_result[ $y ] ) );
	}

	// If there is a value return it, else return null.
	return ( isset( $values[ $x ] ) && '' !== $values[ $x ] ) ? $values[ $x ] : null;
}

 
 
 ````
 ## insert 
 
````php
$wpdb->insert(
	'table',
	array(
		'column1' => 'value1',
		'column2' => 123,
	),
	array(
		'%s',
		'%d',
	)
);



````
