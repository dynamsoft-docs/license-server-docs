# Docs-Template-Repo

## Configuration Files

The following are some configuration files you may need to change:

- [_config.yml](_config.yml)
- [_layouts/default-layout.html](_layouts/default-layout.html)
- [_includes/liquid_breadcrumb.html](_includes/liquid_breadcrumb.html)

Please follow the explanation to replace the information with your product.


## Front Matter

You can use the front matter to change the value of page varibales or define your own custom varibales. Detailed information can be found in [Jekyll Documentation](https://jekyllrb.com/docs/front-matter/).

 Here is a basic example:

```
---
layout: defalut-layout
title: Homepage
keywords: homepage, doc
description: This page is the site homepage.
---
```

- layout: define the layout used for this page.
- title/keywords/description: for SEO, will be auto-generated as SEO tag in published site. 


There are three other custom variables we use in the template site:

- breadcrumbText: use to define the text shown at breadcrumb navigation, only valid for index pages.
- needAutoGenerateSidebar: use to define whether generating in-this-article content.
- needGenerateH3Content: use to define whether containing `<h3>` header in in-this-article content.

## URL

https://www.dynamsoft.com/license-server/docs/about/index.html


