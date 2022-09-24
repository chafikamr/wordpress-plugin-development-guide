# wordpress-plugin-development-guide
This is a a guide to follow when creating wodpress plugin , I have created it help me and to function as a reference since the offical codex is overwhelming 

``` php
/*
 * Plugin Name:       NS Slider
 * Plugin URI:        https://example.com/plugins/the-basics/
 * Description:       This is not just a plugin, it symbolises the hope and enthusiasm of an entire generation summed up in two words sung most famously by Louis Armstrong: Hello, Dolly. When activated you will randomly see a lyric from Hello, Dolly in the upper right of your admin screen on every page.
 * Version:           1.10.3
 * Requires at least: 5.2
 * Requires PHP:      7.2
 * Author:            Chafik Amraoui
 * Author URI:        https://author.example.com/
 * License:           GPL v2 or later
 * License URI:       https://www.gnu.org/licenses/gpl-2.0.html
 * Update URI:        https://example.com/my-plugin/
 * Text Domain:       my-basics-plugin
 * Domain Path:       /languages
 */


/*
NS Slider is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 2 of the License, or
any later version.

NS Slider is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with NS Slider. If not, see https://www.gnu.org/licenses/gpl-2.0.html.
*/

```

### security checkers 
1 - create index file.php in the root of the folders 

```php
<?php
// silence is golden 
```

2 - check if add_action function exists 

```php
if ( !function_exists( 'add_action' ) ) {
	echo 'Hi there!  I\'m just a plugin, not much I can do when called directly.';
	exit;
}
```
3 - check if the absolute path (ABSPATH) is defined 

```php

// chekc method 2 
if(!defined('ABSPATH')){
	die('Hall ! What are you doing ');
	exit;

}

```
### create the main class 

```php

if( ! class_exists('NS_slider')){

	class NS_slider{
		function __construct()
		{

		}
	}
}

if( class_exists('NS_slider')){

	$NS_slider = new NS_slider();
}

```
### defining consonants 

1 - craete a functiojn in the main class `defining_constants`
```php
public function ()
{
    define('NS_SLIDER_PATH',plugin_dir_path(__FILE__));
    define('NS_SLIDER_URL',plugin_dir_url(__FILE__));
    define('NS_SLIDER_VERSION','1.0.0');

}
```

2- now go to the constructor of the main class and call the `definig_constants` method

```php
function __construct(){


// calling constants definig method
$this->defining_constants();



}

```
