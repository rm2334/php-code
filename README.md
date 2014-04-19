Function.php
***
```php
// Define Directory
define('THEMECSS', get_template_directory_uri().'/css/');

wp_enqueue_script('bootstrap',THEMEJS.'bootstrap.min.js',array(),'3.0.3',true);
```

```php
// Function Check
if(!function_exists('xxxx')):

  function xxx()
  {
    if(is_admin())
    {
      // Function goes to here
    }
  }

  add_action('admin_enqueue_scripts','xxx');

endif;
```

```php
// custom_function
function custom_function () {
    echo 'XXXXX';
    echo 'XXXXX';
}
add_action('wp_head', 'custom_function');
```

```php
// remove unwanted items
remove_action( 'wp_head', 'wp_shortlink_wp_head', 10, 0); // Display the links to the shortlink
remove_action( 'wp_head', 'rel_canonical'); // Display the links to the canonical link
remove_action( 'wp_head', 'feed_links_extra', 3); // Display the links to the extra feeds such as category feeds
remove_action( 'wp_head', 'feed_links', 2); // Display the links to the general feeds: Post and Comment Feed
remove_action( 'wp_head', 'rsd_link'); // Display the link to the Really Simple Discovery service endpoint, EditURI link
remove_action( 'wp_head', 'wlwmanifest_link' ); // Display the link to the Windows Live Writer manifest file.
remove_action( 'wp_head', 'index_rel_link' ); // index link
remove_action( 'wp_head', 'parent_post_rel_link'); // prev link
remove_action( 'wp_head', 'start_post_rel_link'); // start link
remove_action( 'wp_head', 'adjacent_posts_rel_link_wp_head', 10, 0); // Display relational links for the posts adjacent to the current post.
remove_action( 'wp_head', 'wp_generator'); // Display the XHTML generator that is generated on the wp_head hook, WP version			
```
PHP File
***

```php
// customize admin footer text
function custom_admin_footer() {
        echo '<p>Develop by: <a href="http://www.webnanny.ie">Webnanny</a>, Customize by: <a href="http://www.cookingwp.com" target="_blank" title="Developer">Tawhidul Islam</a> Powered by: Wordpress</p>';
} 
add_filter('admin_footer_text', 'custom_admin_footer');
```

```php
// PHP CSS
<?php
header('Content-type: text/css');

$parse_uri = explode('wp-content', $_SERVER['SCRIPT_FILENAME']);
$wp_load = $parse_uri[0].'wp-load.php';
require_once($wp_load);
?>
```

```php
// Themes Option Using PHP File
global $smof_data;
$output = '';

if(isset($smof_data['body_bg'])):
	$output .= 'body{ background: '.$smof_data['body_bg'] .'; }';
endif;

echo $output;
```

```php
// Themes Option Using Functions
$box_options = pukka_fp_box_settings();
	//add_image_size('thumb-content', 615, 9999, false); // single page
	add_image_size('thumb-brick-big', $box_options['big_img_width'], $box_options['big_img_height'], true); // big brick
```

```php
// Comment reply js
if ( is_singular() && comments_open() && get_option( 'thread_comments' ) ) {
		wp_enqueue_script( 'comment-reply' );
	}
```

```php
// Dynamic title
<?php
/**
 * Page titles
 */
function dw_timeline_title() {
  if (is_home()) {
    if (get_option('page_for_posts', true)) {
      return get_the_title(get_option('page_for_posts', true));
    } else {
      return get_bloginfo('name');
    }
  } elseif (is_archive()) {
    $term = get_term_by('slug', get_query_var('term'), get_query_var('taxonomy'));
    if ($term) {
      return apply_filters('single_term_title', $term->name);
    } elseif (is_post_type_archive()) {
      return apply_filters('the_title', get_queried_object()->labels->name);
    } elseif (is_day()) {
      return sprintf(__('Daily Archives: %s', 'dw-timeline'), get_the_date());
    } elseif (is_month()) {
      return sprintf(__('Monthly Archives: %s', 'dw-timeline'), get_the_date('F Y'));
    } elseif (is_year()) {
      return sprintf(__('Yearly Archives: %s', 'dw-timeline'), get_the_date('Y'));
    } elseif (is_author()) {
      $author = get_queried_object();
      return sprintf(__('Author Archives: %s', 'dw-timeline'), $author->display_name);
    } else {
      return single_cat_title('', false);
    }
  } elseif (is_search()) {
    return sprintf(__('Search Results for %s', 'dw-timeline'), get_search_query());
  } elseif (is_404()) {
    return __('Not Found', 'dw-timeline');
  } else {
    return get_the_title();
  }
}
```

```php
// Body Class
function dw_minion_body_classes( $classes ) {
	if ( is_multi_author() ) {
		$classes[] = 'group-blog';
	}
	return $classes;
}
add_filter( 'body_class', 'dw_minion_body_classes' );
```
Normal
***
```php
// Comment Number
<?php // conditional comment link text
		if (comments_open()) :
			comments_number(__('Post a Comment'), __('1 Response'), __('% Responses'));
		else :
			comments_number(__('Comments'), __('1 Response'), __('% Responses'));
		endif; ?>
```

```php
// IF
<?php $xxx = bloginfo('pingback_url'); ?>
	<?php if($xxx != ''): ?>
	<?php echo $xxx; ?>
<?php endif; ?>
```

```php
// Multi Dropdown
  <?php $video_source = rwmb_meta( 'cookingwp_video_source' ); ?>
            <?php $video = rwmb_meta( 'cookingwp_video' ); ?>

            <?php if($video_source == 1): ?>
                <?php echo rwmb_meta( 'cookingwp_video' ); ?>
            <?php elseif ($video_source == 2): ?>
                <?php echo ''.$video.''; ?>
            <?php elseif ($video_source == 3): ?>
                <?php echo ''.$video.''; ?>
            <?php endif; ?>
```

```php
// .htaccess
User-agent: *
Disallow: /feed/
Disallow: /trackback/
Disallow: /wp-admin/
Disallow: /wp-content/
Disallow: /wp-includes/
Disallow: /xmlrpc.php
Disallow: /wp-
Allow: /wp-content/uploads/
Sitemap: http://example.com/sitemap.xml

User-agent: *

Disallow: /feed/
Disallow: /cgi-bin/
Disallow: /wp-admin/
Disallow: /wp-content/
Disallow: /wp-includes/
Disallow: /trackback/
Disallow: /xmlrpc.php
Disallow: ?wptheme=
Disallow: /blackhole/
Disallow: /transfer/
Disallow: /tweets/
Disallow: /mint/

Allow: /tag/mint/
Allow: /tag/feed/
Allow: /wp-content/online/

Sitemap: http://perishablepress.com/sitemap-perish.xml
Sitemap: http://perishablepress.com/sitemap-press.xml

User-agent: ia_archiver
Disallow: /

User-agent: *
Disallow: /mint/
Disallow: /labs/
Disallow: /*/wp-*
Disallow: /*/feed/*
Disallow: /*/*?s=*
Disallow: /*/*.js$
Disallow: /*/*.inc$
Disallow: /transfer/
Disallow: /*/cgi-bin/*
Disallow: /*/blackhole/*
Disallow: /*/trackback/*
Disallow: /*/xmlrpc.php
Allow: /*/20*/wp-*
Allow: /press/feed/$
Allow: /press/tag/feed/$
Allow: /*/wp-content/online/*
Sitemap: http://perishablepress.com/sitemap.xml

User-agent: ia_archiver
Disallow: /
```
