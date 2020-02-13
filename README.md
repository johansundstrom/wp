# wp
Wordpress och Bootstrap

## PHP test
* Skapa test.php i ```wp-content/themes/<aktuell mapp>```
```php
<?php 
  $wp = 'WordPress';
  echo($wp . " ver. " . $wp_version);
?>
```
* Prova funktion
```php
<?php 
  function myFunction($data) {
      $myValue = $data + 8;
      echo "<p>" . $data . " + 8 = " . $myValue . "</p>";
  }

  myFunction(5);
?>
```

## filer i wp
* Alla privata filer tillsammans kallas ```theme files``` öcriga ```core files```
* Theme files placeras i ```wp-content/themes/<mapp>``` övriga kan tas bort
* Theme files består av
  * ```comments.php``` 
  * ```footer.php``` avslutande HTML och kod
  * ```functions.php``` PHP bibliotek (PHP-kod)
  * ```header.php``` inledande HTML och kod
  * ```index.php``` mittre HTML och kod
  * ```single.php``` en detaljsida ur en 
  * ```style.css``` stil
* Gemensamt för alla PHP-filer är att dekan inledas med, syns i Wordpress
```php
<?php
/*
Template Name: Beskrivning av innehåll
*/
?>
```
* Filen ```style.css``` inleds med 
```css
/*
    Theme Name: Johans Tema
    Theme URI: https://github.com/johansundstrom/wp/
    Description: Ett Bootstrap Tema
    Author: Johan Sundström
    Author URI: https://github.com/johansundstrom
    Version: 1.0
*/
```

### header.php
* inledande HTML5
* ```<html <?php language_attributes(); ?>>``` skapar "<html lang="sv-SE">" baserat på General Settings
* ```<title><?php wp_title(); ?></title>``` dynamisk titelframställare
* ```<link rel="pingback" href="<?php bloginfo( 'pingback_url' ); ?>" />``` meddelar andra bloggare om publicering 
* Triggar head... 
```php
    <?php wp_head(); ?>
</head>
```
* ```<body <?php body_class(isset($class) ? $class : ''); ?>>``` Sätter CSS klasser på BODY
* Special för Bootstrap
```
<?php wp_nav_menu( array('menu' => 'Main', 'menu_class' => 'nav navbar-nav navbar-right', 'depth'=> 3, 'container'=> false, 'walker'=> new Bootstrap_Walker_Nav_Menu)); ?>
```

### index.php
* ```<?php get_header(); ?>``` laddar in headermallen
* Loopen
  * ```<?php if(have_posts()) : ?>``` villkor för loop
  * Loopen
```php
<?php while(have_posts()) : the_post(); ?>
    <div id="post-<?php the_ID(); ?>" <?php post_class(); ?>>
        <?php the_title('<h2>','</h2>'); ?>
        <?php the_content(); ?>
    </div>
<?php endwhile; ?>
```
  * ```<?php endif; ?>``` avslutar villkor för loop
* ```<?php get_footer(); ?>``` laddar in footermallen

### footer.php
```php
    <?php wp_footer(); ?>
</head>
```

## Wp functions
<?php bloginfo('name'); ?> - Webb namn


## WP loop - enkel version

```php
<?php
    //loop av alla posts
    while(have_posts()) {
        //aktuell post i loopen
        the_post(); ?>
        <!-- länk till aktuell post, titel och content-->
        <h2><a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></h2>
        <?php the_content(); ?>
        <hr>
        <?php
    }
?>
```
* Filen single.php söks av WP för att visa single posts
* Skillnader mellan posts och pages men de hamnar på urls

## header
* skapa ```header.php``` och ```footer.php```
* Peta in i page.php och posts.php...
```php
get_header();
...
get_footer();
``` 


* I head...

```functions.php```
```<?php wp_head(); ?>```


## filen Functions.php

```php
<?php 
    function johan_files() {
        //
        wp_enqueue_style('johan_styles', get_stylesheet_uri());
    }
    add_action('wp_enqueue_scripts', 'johan_files');
?>
```

## Ett nytt tema
### index.php
```php

```
