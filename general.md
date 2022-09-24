## general Informations 

#### 1 - Actvation & deactivation hooks 
Activation and deactivation hooks provide ways to perform actions when plugins are activated or deactivated.
- On activation, plugins can run a routine to add rewrite rules, add custom database tables, or set default option values.
- On deactivation, plugins can run a routine to remove temporary data such as cache and temp files and directories.
The hook `register_activation_hook`  can be used to perfom certain action when the plugin is activated :
- in this example we use `register_activation_hook` to create a page when the plugin is installed
````php
//this code creates a new page when the plugin is activated 

register_activation_hook( __FILE__, 'create_page_function' );


function create_page_function(){

  $page_title = 'Hello WP developers!';
  $page = array(
  'post_title' => $page_title,
  'post_content' => 'page content',
  'page_status' => 'publish',
  'post_type' =>'page'
}


wp_insert_post($page);


````

- we can also  use `register_activation_hook` to create a new table in the database when our plugin is installed 


````php

register_activation_hook( __FILE__, 'create_sql_table' );


function create_sql_table(){

   global $wpdb;
$welcome_name = 'Mr. WordPress';
$welcome_text = 'Congratulations, you just completed the installation!';

$table_name = $wpdb->prefix . 'liveshoutbox';

$wpdb->insert( 
	$table_name, 
	array( 
		'time' => current_time( 'mysql' ), 
		'name' => $welcome_name, 
		'text' => $welcome_text, 
	) 
);
}


````

whle the `register_activation_hook` can be used to perforction when a pugin is installed , `register_deactivation_hook` works as 
a counterpart of it ; it is fired when the pulugin is desactivated , so that it can be used to delete plugin tables from wp databases that were created in installation . 

````php

register_deactivation_hook( __FILE__, 'drop_plugin_table' );


function drop_plugin_table(){
 global $wpdb;
    $wpdb->query( "DROP TABLE IF EXISTS NestoNovo" );




``
