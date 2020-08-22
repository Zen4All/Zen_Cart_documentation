---
title: Order Total Modules - Miscellaneous Questions
category: order_total 
weight: 5
---

{{< misc >}} 

---
### How can I build an order total module? 
See the development page on [building order total modules](/dev/code/modules/order_total_modules/). 

--- 
### Why don't order total modules change the prices of products in the cart? 
That's not how they work. They apply to the **total** order value, not to
any individual product.  So they are line items which are added or subtracted after the Sub-Total is computed. 

There are ways to reduce individual product prices - you can use [Sales](/user/admin_pages/catalog/salemaker/) or [Specials](/user/admin_pages/catalog/specials/).

There are ways to increase individual product prices through [attributes](/user/products/attributes/). 

---
<!-- please keep this at the end --> 
{{< faq_questions >}}

