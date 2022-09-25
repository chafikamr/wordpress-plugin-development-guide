### What are nonces in wordpress ?
Nonce is a number or key used once. WordPress uses Nonces to protect URLs and forms from getting misused by malicious hack attempts.

### Createing a new nonce for a form


To create a `nonce token ` we use the built in function provided by wordpresss `wp_create_nonce` : 
````php 
<input type="hidden" name="nonce_name" value="<?php wp_create_nonce( 'Nonce_name' ); ?>" >

````


### verifying nonce token 

To verify a nonce passed in some other context, call wp_verify_nonce() specifying the nonce and the string representing the action. For example:

````php

wp_verify_nonce( $_REQUEST['nonce_name'], 'nonce_name' );



````
