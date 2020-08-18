---
title: Miscellaneous Beginner Questions 
description: Questions people ask when starting with Zen Cart 
category: running 
weight: -1 
---

{{< misc >}} 

---
### What if I don't have a file that some instructions mention? 

In all likelihood, the file is a 
[template file](/user/first_steps/overrides/#template-files).

Examples of template files are: 

```
includes/templates/responsive_sheffield_blue/common/tpl_header.php
includes/modules/theme872/product_listing.php
includes/modules/sideboxes/goodwin/whats_new.php
includes/languages/english/responsive_classic/shopping_cart.php 
```

If the file is a template file, you create it by copying the associated default file.  

**Example:**
To create 

```
includes/languages/english/YOURTEMPLATE/header.php
```

copy 
```
includes/languages/english/header.php to includes/languages/english/YOURTEMPLATE/header.php
```

See the [I don't have the file ...](/user/new_user_topics/no_such_file/) FAQ for more detail. 

The list of possibly overridden files is longer than you might think - see 
[what can I override](/user/template/template_overrides/#what-can-i-override) for 
a complete list of folders. 

---
<!-- please keep this at the end --> 
{{< faq_questions >}}
