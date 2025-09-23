# SALT34 Website

This repository houses [the website for SALT36](https://saltconf.github.io/salt36/). This website was forked directly from [the repository](https://github.com/saltconf/salt34) housing the [the SALT34 website](http://salt.linguistics.ucla.edu/34/), itself forked from [the repository](https://github.com/saltconf/salt29) housing the [the SALT29 website](http://salt.linguistics.ucla.edu/29/).

Following the SALT34 overhaul, the site uses jekyll to factor content from structure.

1. Change information site-wide by editing the [YAML](https://yaml.org/) files in `_data`.
2. Edit site-wide styles in `_sass`. Style files uses [SASS](https://sass-lang.com/) rather than vanilla CSS.
3. Edit page structure site-wide in `_layouts`. This page structure supports [liquid templates](https://shopify.github.io/liquid/), allowing flexible population of page contents, e.g., automatic construction of the program from YAML. 
