---
id: 87171
date: '2022-01-15T01:55:23-05:00'
author: Tux
layout: revision
guid: 'https://mindlesstux.com/?p=87171'
permalink: '/?p=87171'
---

```
<pre class="command-line" data-output="2-21">```bash
diff -u single.php.orig single.php
--- single.php.orig     2022-01-15 01:49:45.258556123 -0500
+++ single.php  2022-01-15 01:47:56.898608750 -0500
@@ -34,6 +34,17 @@
                                                <?php wp_link_pages(array('before'=>'<div class="post-pages">'.esc_html__('Pages:','blogstream'),'after'=>'</div>')); ?>
                                                <div class="clear"></div>
                                                <?php the_tags('<p class="post-tags"><span>'.esc_html__('Tags:','blogstream').'</span> ','','</p>'); ?>
+                                               <?php 
+                                                       $mykey_values = get_post_custom_values('Reference_URL');
+                                                       if(!empty($mykey_values)) {
+                                                               echo '<p class="post-tags"><span>Referenced URL/Sites:';
+                                                               foreach ( $mykey_values as $key => $value ) {
+                                                                       // echo "$key => $value<br />"; 
+                                                                       echo "<a href=\"$value\">$value</a>";
+                                                               }
+                                                               echo '</span></p>';
+                                                       }
+                                               ?>
                                                <?php do_action( 'alx_ext_sharrre' ); ?>
                                        </div><!--/.entry-->
                                </div>
```
```

Easier to copy/paste code.

```
<pre class="line-numbers">```php
$mykey_values = get_post_custom_values('Reference_URL');
if(!empty($mykey_values)) {
    echo '<p class="post-tags"><span>Referenced URL/Sites:';
    foreach ( $mykey_values as $key => $value ) {
        echo "<a href=\"$value\">$value</a>";
    }
    echo '</span></p>';
}
```
```