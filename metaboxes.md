### What is ta data ?
Simply speaking, metadata is information about information. For example, think about a document on your computer. Any information about that document, like who created it and when, would be considered metadata for that document.

In WordPress, metadata is information about your posts, pages, users, comments, and other items on your site. For example, a post’s metadata would include information like the author, the publish date, the category and tags, and more.

In WordPress, your posts, pages, users, comments, and custom post types all have metadata.

All the metadata on your site is stored in the WordPress database. Your theme is what determines which metadata is displayed on your site, and where and how it’s displayed.

For example, with the Twenty Twenty theme, the category is displayed above the post title. Below the title, you can see the author and publish date.

As a wordpress plugin developer , you can add custom meta data to posts or you custom post type using the built in function`add_meta_box()`
### add_meta_boxes hook

the `add_meta_boxes` hook fires after all built in metaboxes have been added , it can be used rigger the function`add_meta_box()` to add a custom meta box 

````php

function adding_custom_meta_boxes( $post_type, $post ) {
    add_meta_box( 
        'my-meta-box',
        __( 'My Meta Box' ),
        'render_my_meta_box',
        'post',
        'normal',
        'default'
    );
}
add_action( 'add_meta_boxes', 'adding_custom_meta_boxes', 10, 2 );

````

### add_meta_box function 

this function is used to add metabox to one or more screens 
[see add_meta_box() and its arguments  in wordpress documentation ](https://developer.wordpress.org/reference/functions/add_meta_box/)
````php

/**
 * This function adds a meta box with a callback function of my_metabox_callback()
 */
function add_wpdocs_meta_box() {
	$var1 = 'this';
	$var2 = 'that';
	add_meta_box(
		'metabox_id',//this id will be  as id attribute of the metabox
		__( 'Metabox Title', 'textdomain' ),//  title of meta box that will appear in front end
		'wpdocs_metabox_callback',//Function that fills the box with the desired content.
//The function should echo its output.
		'page',//post type to which we want to add metabox 
		'normal', // The context within the screen where the box should display
		'low', // The priority within the context where the box should show.
		array( 'foo' => $var1, 'bar' => $var2 ) // Data that should be set as the $args property of the box array (which is the second parameter passed to your callback).
	);
}

/**
 * Get post meta in a callback
 *
 * @param WP_Post $post    The current post.
 * @param array   $metabox With metabox id, title, callback, and args elements.
 */

function wpdocs_metabox_callback( $post, $metabox ) {
	// Output last time the post was modified.
	echo 'Last Modified: ' . $post->post_modified;

	// Output 'this'.
	echo $metabox['args']['foo'];

	// Output 'that'.
	echo $metabox['args']['bar'];

	// Output value of custom field.
	echo get_post_meta( $post->ID, 'wpdocs_custom_field', true );
}


````


### add meta data callback 

The callback function mensioned in the add_meta_box function is used mainly to render fields in th efront end 
that call back function accepts one required parameter which is the $post 

````php 
function my_call_back_function($post){

require_once(PLUGIN_PATH . 'views/metabox_fields');


?>


}


````
### The view 

the fields created in the view file are that ones that will appear in the metabox 
````html
<label for=""meta-data-1"> meta data label </label>
<input type="text" name="meta-data-key-1" id="meta-data-1">
````

### Saving box data 
To save meta box data , we create a function that will be executed as the hook `save_post` fires 


````php 

add_action('save_post' , 'save_meta_box');


function save_metabox($post_id){


// doing the check 
if( isset($_POST['action']  && $_POST['action'] == 'editpost'){






}




}






````
to save post meta wordpress provies meta functions that are responsible for all crud operations with all post types 
|     	   | Add         | Get| Update | Delete |
| ------------- |:-------------:| -----:|------| ---|
| Posts  | add_post_meta | get_post_meta | update_post_meta | delete_post_meta |
| Users  | add_user_meta | get_user_meta | update_user_meta | delete_user_meta |
| Comments | add_comment_meta | get_comment_meta | update_comment_meta | delete_comment_meta |
| Terms | add_term_meta | get_term_meta | update_term_meta | delete_term_meta |


When using `get_post_meta' we pass 3 params to the function 
- param 1 : post id 
- param 2 : meta key
- param 3 : fetching methode<br> 

 [ee wp dev doc](https://developer.wordpress.org/reference/functions/get_post_meta/)
 
 it is always recommended to use update_post_meta to save data 
 - param 1 : post id 
 - param 2 : meta key that shouild be updated or added if not exist 
 - param 3 : new value 
 - param 4 : previous value <br>
 for more information take a look on [update_post_meta](https://developer.wordpress.org/reference/functions/update_post_meta/)
