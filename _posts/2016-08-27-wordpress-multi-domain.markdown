---
published: true
title: WordPress multi domain
layout: post
---
In wp-config.php add: 

/*
 * Handle multi domain into single instance of wordpress installation
 */
```
define('WP_SITEURL', 'http://' . $_SERVER['HTTP_HOST']);
define('WP_HOME', 'http://' . $_SERVER['HTTP_HOST']);
```