# SALT Template Website

This repository houses a template [website](https://saltconf.github.io/salt3X/) for a SALT conference. The content and design are based on the [the SALT29 website](http://salt.linguistics.ucla.edu/29/), with source code substantially refactored following [the repository](https://github.com/saltconf/salt34) housing the [the SALT34 website](http://salt.linguistics.ucla.edu/34/). 

Future SALTs may start by forking this repo. Then:

1. Change information site-wide by editing the [YAML](https://yaml.org/) files in `_data`, starting with `_config.yml`.
2. Edit site-wide styles in `_sass`. Style files uses [SASS](https://sass-lang.com/) rather than vanilla CSS. In particular, the primary and accent colors can be adjusted in `_config.scss`.
3. Edit page structure site-wide in `_layouts`. This page structure supports [liquid templates](https://shopify.github.io/liquid/), allowing flexible population of page contents, e.g., automatic construction of the program from YAML. 
4. Upload banner images, bullet icons, and favicons to provide local color, as desired.
