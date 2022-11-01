## create page with shortcode programmatically 

````php

$currentUser = wp_get_current_user();

 
    $page = array(
        'post-title' => 'the title',
        'post_name' =>'the-name',
        'post_status' => 'publish' ,
        'post_author' => $currentUser->ID,
        'post_type' => 'page',
        'post_content' => '<!-- wp:shortcode --> [my_short_code] <!-- /wp:shortcode -->'
    ); 

    wp_insert_post($page);
````
