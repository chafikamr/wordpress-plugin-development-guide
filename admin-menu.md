### Admin panel custom menu

Sometimes when we work with plugins or theme and we need to show some features or any information in admin page then we can use this code snippet to create the same.

As we know WordPress provide hook using which we can easily add custom admin menu. So, for this we’ll use ‘admin_menu’ hook and add action to this hook

- hook the admin menu 
Add this code in functions.php file of your plugin or theme.

````php
add_action('admin_menu', 'custom_menu');

````
In above line of code, first parameter is the hook we discuss about, Second parameter is name of callback function. In callback function you have to write what you want to alter in admin menu.

- create callback function 

````php
function custom_menu() { 

  add_menu_page( 
      'Page Title', // First parameter is page title. the title tag of the page when the menu is selected..
      'Menu Title', // Second parameter is menu title. The text to be used for menu title.
      'edit_posts',  // Third one is capability, The capability required for this menu to be displayed to the user
      'menu_slug',  // Fourth parameter is menu slug, which is used for creating page URL. Keep this unique.
      'page_callback_function', // Fifth parameter is page callback function. The function to be called to output the content for this page.
      'dashicons-media-spreadsheet' //Sixth parameter is for icon, either you can provide a URL of image or you can choose predefined WordPress icons. https://developer.wordpress.org/resource/dashicons/

     );
}

````
As you can see in custom_menu() function I just used add_menu_page(). This function allow you to create a menu in admin sidebar and map that menu to a page.
In custom_menu() function
 
 calback function 
 
 ````php
 /**
 * Disply callback for the Unsub page.
 */
 function page_callback_function() {
     echo 'Unsubscribe Email List';
 }
 
 
 ````
