### What are Shortcodes?
Shortcodes in WordPress are code shortcuts that help you add dynamic content to WordPress posts, pages, and sidebar widgets. They are displayed inside square brackets like this:

[myshortcode]

To better understand shortcodes, let’s take a look at the background of why they were added in the first place.

WordPress filters all content to make sure that no one uses posts and page content to insert malicious code into the database. This means that you can write basic HTML in your posts, but you cannot write PHP code.

But what if you wanted to run some custom code inside your posts to display related posts, banner ads, contact forms, galleries, etc?

This is where Shortcode API comes in.

Basically, it allows developers to add their code inside a function and then register that function with WordPress as a shortcode, so users can easily use it without having any coding knowledge.

When WordPress finds the shortcode it will automatically run the code associated with it.

Let’s see how to easily add shortcodes to your WordPress posts and pages.

### create custom short code 

````php

// function that runs when shortcode is called
function wpb_demo_shortcode() { 
  
// Things that you want to do.
$message = 'Hello world!'; 
  
// Output needs to be return
return $message;
}
// register shortcode
add_shortcode('greeting', 'wpb_demo_shortcode');



````



### short code with arguments 

````php

[myshortcode foo="bar" bar="bing"]

````


the arguments are available in the callback function as an array 

````php


function call_back($arguments){

print_r($arguments);

}

````
