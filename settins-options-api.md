The Settings API, added in WordPress 2.7, allows admin pages containing settings forms to be managed semi-automatically. It lets you define settings pages, sections within those pages and fields within the sections.

### Add section 
In order to find our "General" section of options, we're going to need to use the add_settings_section function of the Settings API. According to the WordPress Codex, add_settings_section requires three arguments:

````php
add_action('admin_init', 'sandbox_initialize_theme_options');
function sandbox_initialize_theme_options() {
 
    // First, we register a section. This is necessary since all future options must belong to one.
    add_settings_section(
        'general_settings_section',         // ID used to identify this section and with which to register options
        'Sandbox Options',                  // Title to be displayed on the administration page
        'sandbox_general_options_callback', // Callback used to render the description of the section
        'general'                           // Page on which to add this section of options
    );
} // end sandbox_initialize_theme_options

````


### adding fields 
````php
// Next, we will introduce the fields for toggling the visibility of content elements.
add_settings_field( 
    'show_header',                      // ID used to identify the field throughout the theme
    'Header',                           // The label to the left of the option interface element
    'sandbox_toggle_header_callback',   // The name of the function responsible for rendering the option interface
    'general',                          // The page on which this option will be displayed
    'general_settings_section',         // The name of the section to which this field belongs
    array(                              // The array of arguments to pass to the callback. In this case, just a description.
        'Activate this setting to display the header.'
    )
);
````


### adding field content 
````php

/**
 * This function renders the interface elements for toggling the visibility of the header element.
 * 
 * It accepts an array of arguments and expects the first element in the array to be the description
 * to be displayed next to the checkbox.
 */
function sandbox_toggle_header_callback($args) {
     
    // Note the ID and the name attribute of the element should match that of the ID in the call to add_settings_field
    $html = '<input type="checkbox" id="show_header" name="show_header" value="1" ' . checked(1, get_option('show_header'), false) . '/>';
     
    // Here, we will take the first argument of the array and add it to a label next to the checkbox
    $html .= '<label for="show_header"> '  . $args[0] . '</label>';
     
    echo $html;
     
} // end sandbox_toggle_header_callback


````

### register settings 
````php



register_setting(
    'general_group',
    'show_content'
);
 

````

### form of options.php


- `settings_fields`Outputs nonce, action, and option_page fields for a settings page.

````php

settings_fields( 'wpdocs-plugin-settings-group' );



````
- `do_settings_sections `Prints out all settings sections added to a particular settings page
````php


do_settings_sections($page);


````
- `submit_button `Echoes a submit button, with provided text and appropriate class(es).

````php

submit_button( __( 'Reset', 'textdomain' ), 'secondary' );



````
- name of fields must be the id of the filed 
````html

<input type="text" name="options_id[field_id]">

````


### sanitization 

the sunitazation 

````php


register_setting('group','option','callback');


function callback($inputs)
{
return $inputs 
}

````



