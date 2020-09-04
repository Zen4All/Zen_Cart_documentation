---
title: Information sidebox 
description: Making changes to the Information sidebox 
category: sideboxes
weight: 10
---

{{% content_links %}}

### How do I re-arrange the order of the links in the information sidebox?

1. Create (if you don't already have it) a directory named `includes/modules/sideboxes/YOURTEMPLATE/`

2. Copy the includes/modules/sideboxes/information.php file into your new directory

3. Edit the `if` blocks into the order that you would like them to appear.

For example, if you wished the terms and conditions link to appear first, you would move this entire block of php:

```
  if (DEFINE_CONDITIONS_STATUS <= 1) {
    $information[] = '<a href="' . zen_href_link(FILENAME_CONDITIONS) . '">' . BOX_INFORMATION_CONDITIONS . '</a>';
  }
```

 (taking care not to leave the curly bracket behind) to just below the line that says:
```
  unset ($information);
```


