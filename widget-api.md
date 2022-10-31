## Quick start 

````php 

class chafik_widget extends WP_Widget{

    public function __construct()
    {
        $arr= array(
            'discrition' => 'the description option'
        );
        parent::__construct(
            'id-base',// id of the widget type
            'name of widget',// name appears as a title 
            $arr, // widgets options
        );

        add_action('widgets_init',function(){
            register_widget('chafik_widget');
        });


    }

    public function form($instance){

        $the_title = isset($instance['title']) ? $instance['title'] : '';
        $number = isset($instance['number']) ? (int) $instance['number'] : 5;

        /*
        $this->get_field_id('title') => widget-base-id-3-title
        $this->get_field_name('title') =>widget-base-id-[2][title]
        */
        ?>
        <p>
            <label>Title</label>
            <input type="text" name="<?php echo $this->get_field_name('title');?>" id="" class="widefat" value="<?php echo $the_title ?>">

        </p>
        <p>
            <label>Number</label>
            <input type="text" name="<?php echo $this->get_field_name('number');?>" id="" value="<?php echo $number ?>" class="widefat">

        </p>


<?php

    }

    public function widget($args , $instance){

    }

    public function update($new_instance , $old_nstance){

        $instance = $old_nstance;
        $instance['title'] = sanitize_text_field($new_instance['title']);
        $instance['number'] = absint($new_instance['number']);
        return $instance;
    }
}


$chafik_wdgt = new chafik_widget();







````

## frontend


````php

   public function widget($args , $instance){

        // set defaults 
        echo $args['before_widget'];
        echo $args['before_title'];
        echo $args['after_title'];
        echo $args['after_widget'];

    }


``````
