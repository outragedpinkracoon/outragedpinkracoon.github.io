---
title: Set Up Jekyll with Bootstrap and No Theme
layout: post
categories: [jekyll, programming]
---
We've all been there - the themes for Jekyll are not the best and most of them have zero documentation or consistency. I've since moved to vanilla css but you might want to use a css framework, and here's how to do it.

This is valid as of Jekyll 4.2.0.

## INITIALISE JEKYLL PROJECT
Now we want to add the folder structure for Jekyll. I didn’t want to use a theme (we will add Bootstrap later), so we use the -blank argument to get the empty folders but no theme.

```bash
# use '.' to make the folder structure in the current folder
# make sure you are currently in /PROJECT_NAME
jekyll new . --blank
```
Now you’ll have the Jekyll project structure with empty folders.

```bash
# see the site running on port 4000
jekyll serve
```

## BOOTSTRAP
Download the latest Bootstrap files, version 4 in my case, and unzip them. Create a ‘bootstrap’ directory inside the existing empty ‘_sass’ folder

```bash
# inside PROJECT_NAME directory
cd _sass
mkdir bootstrap
```

Copy the files inside bootstrap-4.0.0->scss that you downloaded (NOT the scss folder itself just the contents) into the ‘_sass/bootstrap’ folder we just created inside your jekyll site.

Your folder structure should look like this:

```yaml
--outragedpinkracoon.github.io
  -- many other files
  --_sass
    -- bootstrap
      -- mixins
      -- bootstrap.scss
      -- many other files
```

Confusingly, there’s a different folder assets -> css that we need to go to now to add bootstrap as an import.

```scss
/* assets/css/main.scss */
@import 'bootstrap/bootstrap';
@import "main";
```

Add a fun button or whatever you fancy to check Bootstrap is working as expected.

## BOOTSTRAP JAVASCRIPT
Grab the links to the Bootstrap Javascript on the CDN and add them before the closing body tag in your site layout file. Make sure the scripts are in the right order, JQuery -> Popper -> Bootstrap!

Test it’s working by adding the nav burger menu or something else fun.

## BONUS: MINIFY SCSS
You might want to get Jekyll minifying your SCSS by adding this config line:

```yaml
# config.yml
sass:
  style: compressed
```
