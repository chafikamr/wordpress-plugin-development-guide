### enquee Front End 
#### Hook 
`wp_enqueue_scripts` is the proper hook to use when enqueuing scripts and styles that are meant to appear on the front end. Despite the name, it is used for enqueuing both scripts and styles.

````php

add_action( 'wp_enqueue_scripts', 'my_callback' );


function my_callback(){

// block of code



}



````

````php

add_action( 'admin_enqueue_scripts', 'my_callback' );


function my_callback(){

// block of code



}



````

#### register script / style 


Registers a script to be enqueued later using the wp_enqueue_script() function.

````php

wp_register_script( $handle, $src, $deps, $ver, $in_footer );

````


register stylsheet 
````php

 wp_register_style( $handle, $src, $deps = array(), $ver = false, $media = 'all' ) 



````


#### enquee script and style 


````php
wp_enqueue_style( 'my-plugin' );
wp_enqueue_sscript( 'my-plugin' );

````



#### add html script to header front end 

````php

add_action('wp_head', 'inject_required_scripts');

````
