---
title: How to install a plugin
category: plugins
weight: 1
---

If you installed your Zen Cart using Fantastico or perhaps had a friend or subcontractor install it for you, installing a mod might seem daunting. Don't worry - there's nothing to it as long as you follow some basic principles.  

## Reading the instructions

This page shows you how to copy files into your cart. This is just one part of installation; there may be many associated tasks that need to be done. 
Most contributions come with a README file; please take the time to review it to get the whole picture of how installation is to be done.  

Reading the instructions **before** starting installation is a great way to reduce grief. 

## Getting Started

Before you start, you'll need to verify that you have some things.

*   Mods are provided in zip format, so you'll need a tool to unzip the file.
*   You'll need a tool to transfer the files from your local PC to your webserver.
*   You'll need a simple text editor to do customizations to files

## Zip File Structure

Here's the complete structure of the [Quantity Discounts](https://www.zen-cart.com/downloads.php?do=file&id=135) contribution, as an example. 

<pre class="code">./includes
./includes/languages
./includes/languages/english
./includes/languages/english/modules
./includes/languages/english/modules/order_total
./includes/languages/english/modules/order_total/ot_quantity_discount.php
./includes/modules
./includes/modules/order_total
./includes/modules/order_total/ot_quantity_discount.php
./README.txt
</pre>

There are only two code files here and one README; the other things you see are parent directories for those files. An abbreviated listing of this is

<pre class="code">
./includes/languages/english/modules/order_total/ot_quantity_discount.php
./includes/modules/order_total/ot_quantity_discount.php
./README.txt
</pre>

The hierarchy of these files is intended to exactly duplicate the structure of your cart. So if your cart is installed on your webserver under (say) 
<pre>/public_html/zencart</pre>, then to install the file `./includes/modules/order_total/ot_quantity_discount.php` you would ftp to your site, change directory to `public_html/zencart`, and then transfer the "includes" folder from the mod over.

If your cart is under (say)  /httpdocs/public_html/, the instructions would be the same; ftp to your site; cd to <code>/httpdocs/public_html/</code>
then transfer the <code>includes</code> folder over. 

So in fact, to install this contribution, all you have to do is copy these two files into your cart, turn on the Quantity Discounts order total module (under Admin->Modules->Order Totals), and you're done.  

## Templates and Core Files

I chose the example of Quantity Discounts because it's the simplest form of a mod - it contains only new, original files. What about something more complex which modifies existing files in the cart?  

Zen Cart has two facilities for dealing with situations like this, and you need to understand them prior to installing mods to save yourself grief the next time you upgrade your cart.  

Since changing the "skin" or "theme" of the cart is the most common customization, the user interface is built to accommodate relatively easy customization. Zen Cart calls this mechanism "template overrides" and provides guidelines on how to 
[create a custom template](https://docs.zen-cart.com/user/template/creating_template/).
A common convention is to assume the template name is "custom." So if you see a file with the name "custom" as part of its name, you know it's a template component. If you've used a name other than "custom" then you will have to move the file accordingly. **Note:** If you are using Zen Cart 1.5.5 or higher, your template name will be "responsive_classic" if you have not changed it.  

Some examples: the [Better Together Promotional Page](https://www.zen-cart.com/downloads.php?do=file&id=969) contains a file called

<pre class="code">./includes/templates/custom/templates/tpl_bettertogether_promo_default.php
</pre>

If your template name is "scott", you would install this file in

<pre class="code">./includes/templates/scott/templates/tpl_bettertogether_promo_default.php
</pre>

[What's On Sale](https://www.zen-cart.com/downloads.php?do=file&id=1185) contains a file called

<pre class="code">./includes/modules/custom/sales_index.php
</pre>

If your template name is "apple", you would install this file in

<pre class="code">./includes/modules/apple/sales_index.php
</pre>

Not all files can be handled by the template system. For instance, files in `includes/modules/pages` cannot be overridden. A recommendation for files like this is that during the installation process, you make a backup of the original file, and name it <original-filename>.orig. For instance, the [Gift Wrap at Checkout](https://www.zen-cart.com/downloads.php?do=file&id=267) contribution modifies the file `./admin/invoice.php` Prior to installation, rename this file `./admin/invoice.php.orig`  
This serves two purposes:

*   In the event of a problem, you can easily restore the original file
*   When it comes time to upgrade your cart, you can easily identify the core files you've changed by searching for files named `*.orig`.

Note that ".orig" should be a suffix onto the original filename. (Don't name the file `invoice_orig.php` or `orig_invoice.php`)  

## Merging Template Files

If a contribution includes a template file change, you can simply 
compare the file provided to the unaltered file from a fresh 
Zen Cart download (using either `template_default` or `responsive_classic` as the base template, as appropriate) to see how to apply 
those changes to your template files. 


## Database Changes

Some mods require database changes. For instance, Gift Wrap at Checkout includes a file called orders_wrap.sql, which modifies your database.  

These files are best run through the Zen Cart admin panel, which will take care of the prefix (if you have one). To do this, go to Admin->Tools->Install SQL patches.  

Alternately, you can run them using phpMyAdmin, but you will need to edit the .sql script to account for the prefix. errors occur during execution. Ask your host if you're not sure how to run this tool.  

For instance, if the file creates a table called "orders_giftwrap"

<pre>CREATE TABLE orders_giftwrap(
...
</pre>

you will need to change this to reflect your prefix, i.e.

<pre>CREATE TABLE zen_orders_giftwrap(
...
</pre>

assuming your prefix is `zen_`.  

If you have used a prefix, it is stored in `includes/configure.php`; look for the variable DB_PREFIX.  

If you do an install and get an error like

<pre>1146 Table 'yourdb.zen_better_together_admin' doesn't exist
in:
[SELECT * FROM zen_better_together_admin ORDER BY id DESC ]
If you were entering information, press the BACK button in your browser and re-check the information you had entered to be sure you left no blank fields.
</pre>

This means you used phpMyAdmin but forgot to edit the .sql file to include your prefix.  

The most important principle to remember when changing your database is that you must do a backup prior to making the change. You can do a backup using phpMyAdmin.  

Not all database modifications will be done through a .sql file; for instance, any file which requires you to click an "Install" link from Admin->Modules is modifying your database. Be sure to make a backup!  

Some mods use the "TYPE=MyISAM" syntax when doing a CREATE TABLE, which is not accepted by some newer versions of MySQL. If you get a message like this when running an SQL script:

<pre class="code">ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that
corresponds to your MySQL server version for the right syntax to use near 'TYPE=MyISAM'
at line 1
</pre>

To fix this, simply edit the .sql file and change all instances of

<pre class="code">TYPE=MyISAM
</pre>

to

<pre class="code">ENGINE=MyISAM
</pre>

## Uploading

The best way to upload is to upload the ENTIRE includes directory from the unzipped file onto your includes directory, and the ENTIRE admin directory (if one exists) from the unzipped file onto your admin directory (after the appropriate renames):

*   If your admin folder is named ABCDEF, rename the admin folder in the unzipped mod to ABCDEF, and upload the entire folder.
*   If the unzipped file contains template specific files, rename the containing directories to the name of your template. For instance, if your template is named "blue" and the mod has a directory named

    <pre>includes/modules/YOURTEMPLATE/
    </pre>

    rename this to

    <pre>includes/modules/blue
    </pre>

    Similarly, if the mod contains a directory called

    <pre>includes/templates/custom
    </pre>

    rename this to

    <pre>includes/templates/blue
    </pre>
