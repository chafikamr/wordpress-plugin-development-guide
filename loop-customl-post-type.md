### CPT loop 
Custom post types give WordPress developers the flexibility to store different kinds of data without polluting built-in posts and pages. The possibilities are endless: you can create custom post types for things like recipes, documents, projects, and books. That data is useless, however, if we are not able to display them where we want it. Enter the WP_Query class. It is a powerful tool that can fetch all kinds of data from the WordPress database. Here, I’ll show you how to use the WP_Query class to construct a loop to retrieve custom post types.
````php

<?php
$loop = new WP_Query(
    array(
        'post_type' => 'yourposttypehere' // This is the name of your post type - change this as required,
        'posts_per_page' => 50 // This is the amount of posts per page you want to show
    )
);
while ( $loop->have_posts() ) : $loop->the_post();
// The content you want to loop goes in here:
?>
 
<div class="col-sm-4">
My column content
</div>
 
<?php endwhile;
wp_reset_postdata();
?>


````
### WP_Query class 
The WP_Query class is one of the most important parts of the WordPress codebase. Among other things, it determines the query you need on any given page and pulls posts accordingly. It also saves a lot of information about the requests it makes, which helps a great deal when optimizing pages (and troubleshooting them).

The other role of WP_Query is to enable us to perform complex database queries in a safe, simple and modular manner.<br>

[see wordpress doccs](https://developer.wordpress.org/reference/classes/wp_query/)
