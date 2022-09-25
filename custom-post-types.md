## custom post types 

Do you want to learn how to easily create custom post types in WordPress?<br>

Custom post types allow you to go beyond posts and pages and create different content types for your website. They transform your WordPress site from a blogging platform into a powerful content management system (CMS).


### What Is Custom Post Type in WordPress?
On your WordPress website, post types are used to help distinguish between different content types in WordPress. Posts and pages are both post types but are made to serve different purposes.

WordPress comes with a few different post types by default:

- Post
- Page
- Attachment
- Revision
- Nav Menu
- <br>
You can also create your own post types, known as custom post types. These are useful when creating content that has a different format than a standard post or page.

For instance, if you run a movie review website, then you would probably want to create a movie reviews post type. You could also create custom post types for portfolios, testimonials, and products.
<br>
### Example of creating a custom post type ( book )
````php

/**
 * Register a custom post type called "book".
 *
 * @see get_post_type_labels() for label keys.
 */
function wpdocs_codex_book_init() {
	$labels = array(
		'name'                  => _x( 'Books', 'Post type general name', 'textdomain' ),
		'singular_name'         => _x( 'Book', 'Post type singular name', 'textdomain' ),
		'menu_name'             => _x( 'Books', 'Admin Menu text', 'textdomain' ),
		'name_admin_bar'        => _x( 'Book', 'Add New on Toolbar', 'textdomain' ),
		'add_new'               => __( 'Add New', 'textdomain' ),
		'add_new_item'          => __( 'Add New Book', 'textdomain' ),
		'new_item'              => __( 'New Book', 'textdomain' ),
		'edit_item'             => __( 'Edit Book', 'textdomain' ),
		'view_item'             => __( 'View Book', 'textdomain' ),
		'all_items'             => __( 'All Books', 'textdomain' ),
		'search_items'          => __( 'Search Books', 'textdomain' ),
		'parent_item_colon'     => __( 'Parent Books:', 'textdomain' ),
		'not_found'             => __( 'No books found.', 'textdomain' ),
		'not_found_in_trash'    => __( 'No books found in Trash.', 'textdomain' ),
		'featured_image'        => _x( 'Book Cover Image', 'Overrides the “Featured Image” phrase for this post type. Added in 4.3', 'textdomain' ),
		'set_featured_image'    => _x( 'Set cover image', 'Overrides the “Set featured image” phrase for this post type. Added in 4.3', 'textdomain' ),
		'remove_featured_image' => _x( 'Remove cover image', 'Overrides the “Remove featured image” phrase for this post type. Added in 4.3', 'textdomain' ),
		'use_featured_image'    => _x( 'Use as cover image', 'Overrides the “Use as featured image” phrase for this post type. Added in 4.3', 'textdomain' ),
		'archives'              => _x( 'Book archives', 'The post type archive label used in nav menus. Default “Post Archives”. Added in 4.4', 'textdomain' ),
		'insert_into_item'      => _x( 'Insert into book', 'Overrides the “Insert into post”/”Insert into page” phrase (used when inserting media into a post). Added in 4.4', 'textdomain' ),
		'uploaded_to_this_item' => _x( 'Uploaded to this book', 'Overrides the “Uploaded to this post”/”Uploaded to this page” phrase (used when viewing media attached to a post). Added in 4.4', 'textdomain' ),
		'filter_items_list'     => _x( 'Filter books list', 'Screen reader text for the filter links heading on the post type listing screen. Default “Filter posts list”/”Filter pages list”. Added in 4.4', 'textdomain' ),
		'items_list_navigation' => _x( 'Books list navigation', 'Screen reader text for the pagination heading on the post type listing screen. Default “Posts list navigation”/”Pages list navigation”. Added in 4.4', 'textdomain' ),
		'items_list'            => _x( 'Books list', 'Screen reader text for the items list heading on the post type listing screen. Default “Posts list”/”Pages list”. Added in 4.4', 'textdomain' ),
	);

	$args = array(
		'labels'             => $labels,
		'public'             => true,
		'publicly_queryable' => true,
		'show_ui'            => true,
		'show_in_menu'       => true,
		'query_var'          => true,
		'rewrite'            => array( 'slug' => 'book' ),
		'capability_type'    => 'post',
		'has_archive'        => true,
		'hierarchical'       => false,
		'menu_position'      => null,
		'supports'           => array( 'title', 'editor', 'author', 'thumbnail', 'excerpt', 'comments' ),
	);

	register_post_type( 'book', $args );
}

add_action( 'init', 'wpdocs_codex_book_init' );

````


## unregister post type

similarly you can use `unregister_post_type()` function when deactivating the plugin , this function requirzs only one parametere that is the name of the custom post type


### manage custom post type  table columns 

to manage custom post type cilumns we use the hook `manage_{$post_type}_posts_columns` that Filters the columns displayed in the Posts list table for a specific post type.

````php
function add_book_columns($columns) {
    unset($columns['author']);
    return array_merge($columns, 
              array('publisher' => __('Publisher'),
                    'book_author' =>__( 'Book Author')));
}
add_filter('manage_book_posts_columns' , 'add_book_columns');

````

now we have added needed columns to CPT tablle , let us fill it with the data 
````php
/* Display custom column stickiness */
function display_posts_stickiness( $column, $post_id ) {
    if ($column == 'sticky'){
        echo '<input type="checkbox" disabled', ( is_sticky( $post_id ) ? ' checked' : ''), '/>';
    }
}
add_action( 'manage_posts_custom_column' , 'display_posts_stickiness', 10, 2 );

/* Add custom column to post list */
function add_sticky_column( $columns ) {
    return array_merge( $columns, 
        array( 'sticky' => __( 'Sticky', 'your_text_domain' ) ) );
}
add_filter( 'manage_posts_columns' , 'add_sticky_column' );



````
