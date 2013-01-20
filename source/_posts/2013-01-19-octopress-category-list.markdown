---
layout: post  
title: "Octopress Category List"  
date: 2013-01-19 23:25  
comments: true  
external-url:   
categories: [octopress, blogging]
---

I have added a list of post categories to my sidebar. It took about 10 minutes following [Dan Watson's instructions][1]. There is one minor change if you are running Octopress version 2.1, as Dan's instructions are for 2.0. and mention putting the new `category_list.html` template in `source/_includes/asides` and updating your `default_asides` line in `_config.yml`.

In 2.1, it appears that the `asides` directory has been deprecated and `_includes/sidebars` is used instead. Place the `category_list.html` template in the `_includes/sidebars/sections` folder, and add the following line:

    {% raw  %}{% include sidebars/sections/category_list.html %}{% endraw %}

to one or more of the following files, depending on what pages you want this category list to appear in the sidebar:

    blog_index_default.html  # For the main page
    page_default.html  # For individual post pages
    post_default.html  # For any archive page

Then generate and deploy. Done.

[1]: http://www.dotnetguy.co.uk/post/2012/06/25/octopress-category-list-plugin/ 