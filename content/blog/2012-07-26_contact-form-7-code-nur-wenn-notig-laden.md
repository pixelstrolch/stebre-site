---
title: "Contact Form 7 Code nur wenn nötig laden"
slug: "contact-form-7-code-nur-wenn-noetig-laden"
author: "Stefan Brechbühl"
date: "2012-07-26"
updated:
description: "Verwendet ihr das WordPress Plugin Contact Form 7 auf eurer Website? Vielleicht ist euch schon aufgefallen, dass eine JavaScript- und eine CSS-Datei auf jeder einzelnen Seite eurer Website in den Header geladen wird."
categories:
tags: ["Performance", "WordPress"]
featuredImage: "assets/2012-07-26/artikelbild_contact_form_7_code_nur_wenn_noetig_laden.jpg"
---
Verwendet ihr das WordPress Plugin [Contact Form 7](http://wordpress.org/plugins/contact-form-7/ "Contact Form 7 auf wordpress.org") auf eurer Website? Vielleicht ist euch schon aufgefallen, dass eine JavaScript- und eine CSS-Datei auf jeder einzelnen Seite eurer Website in den Header geladen wird.

Dies machen übrigens viele andere Plugins auch. Bei einem Plugin wie [Contact Form 7](http://wordpress.org/plugins/contact-form-7/ "Contact Form 7 auf wordpress.org"), welches in der Regel auf ein, zwei Seiten eingesetzt wird, ist es fraglich ob dies Sinn macht. Das Plugin erzeugt dadurch nämlich auf allen anderen Seiten unnötige [HTTP-Requests](http://de.wikipedia.org/wiki/Hypertext_Transfer_Protocol#HTTP-Request-Methoden "HTTP-Request auf wikipedia.org"), was die Seite verlangsamt.

Kürzlich bin ich über ein [passendes und nützliches Snippet auf wpsnipp.com gestolpert](http://wpsnipp.com/index.php/functions-php/enable-contact-form-7-on-specified-pages-only-otherwise-wp_deregister_script/ "Link zum Snippet auf wpsnipp.com"), welches dem entgegenwirkt. Dieses Snippet könnt ihr in euere functions.php des Themes einfügen. Falls ihr das [Toolbox-Plugin von Sergej Müller](http://playground.ebiene.de/toolbox-wordpress-plugin/ "Was ist das Toolbox-Plugin?") im Einsatz habt, könnt ihr euch auch ein neues Modul anlegen und den Code einsetzen.

``` php
add_action( 'wp_print_scripts', 'deregister_cf7_javascript', 100 );
function deregister_cf7_javascript() {
  if ( !is_page(array(8,10)) ) {
    wp_deregister_script( 'contact-form-7' );
  }
}
add_action( 'wp_print_styles', 'deregister_cf7_styles', 100 );
function deregister_cf7_styles() {
  if ( !is_page(array(8,10)) ) {
    wp_deregister_style( 'contact-form-7' );
  }
}
```

Danach müsst ihr nur noch die Ziffern in den zwei Arrays anpassen. Dort werden die ID's der Pages eingesetzt, in denen ein Formular von Contact Form 7 verwendet wird. Die ID findet ihr in der Backend-URL des Posts.

![Post ID in Backend URL](assets/2012-07-26/post-id-in-backend-url.jpg "Post ID in Backend URL")
