numfocus.org
============

NumFOCUS Website

This is the source of the Pelican-based NumFOCUS.org site.  These pages should
be generated from these sources and then pushed to the actual site.

The site is based on Pelican:  http://docs.getpelican.com/


Workflow
========
To add/modify content to the website, please fork the numfocus/numfocus.org
repository on github and make your changes as described below.  When your
changes are ready, please submit a pull request (PR) to have those changes
merged in.  Please apply all changes via PRs.  It makes is much easier for
others to follow changes.  Finally, if you merge a PR, you are responsible for
deploying it or delegating that task in the PR discussion.


Adding Content
==============

The site is organized as a set of pages and a blog with a set of post
categories.  All content is in the `content` directory. Inside `content`, the
blog is located at `articles`, generated pages are at `pages`, and various
files linked to in the pages or blog are in `media`. The theme is located in
the `theme` directory and is documented there.

Blog
----

Each post categorized post will show up in the news feed as well as in its designated
category.  To add new content, create a .rst file in the appropriate category
directory in content.  For example, to add a news story, you should add a file to the
`content/articles/News` directory.  Posts should provide a title and a date i.e

    inSCIght
    ########
    :date: 07-05-2013

Posts can optionally provide a `:slug:` field.  The slug is used to generate a
link name to the post.  If no slug is provided, the title ("inSCIght" in the
above example) will be used. The output url will be based upon the date and title, 


Pages
-----

Each page is set up via a file in the `content/pages` directory. Each page
should include a title, `save_as` field, optionally a url field can be added to
control what url page links use.

    Foundation
    ###########
    :url: foundation/
    :save_as: foundation/index.html
    
    
    NumFOCUS supports and promotes world-class, innovative, open source
    ...

The structure of the pages directory does not affect the output of the html
pages, only the `save_as` field. To make the top tabs work, the link structure
needs to mirror that of the directory.

Optionally if a special template page is included in the theme one can add if
as so.

    NumFOCUS Homepage
    #################
    :save_as: index.html
    :template: page-index

    Some rst content.

Theme
-----

We use a custom theme following the Pelican standard. It was written using Bootstrap, JQuery, and SASS. See `theme/README.md` for more details.

Redirects
---------

If a page is moved it is best to add a redirect to avoid breaking websites
linking to numfocus.org. To do this copy one of the redirect pages in the
`redirects` directory to the name of the moved page. The makefile will only
overwrite pages that are not generated by Pelican.

Internal Links
---------------

To link to a page that is generated by Pelican, prepend `|filename|` to the
path. If the link after `|filename|` starts with `/`, then it will link relative
to the `content` directory. For example:

```
    `Relative Link to file <|filename|file_in_same_dir.rst>`_
    `Absolute Link to file <|filename|/pages/file/in/another/dir.rst>`_
    `Link to media <|filename|/media/pdfs/bylaws.pdf>`_
```

Using the `|filename|` directive will make sure that Pelican issues a warning
for broken links and can generate links for the deploy environment more stably.

Adding Images
-------------

Images should be added to the with `content/media/images` directory.  If the
filename is `spam.jpg`, the path image path in RST is:
`|filename|/media/images/spam.jpg` 


Building and deploying the Site
===============================

Python Dependencies
-------------------
Note that you have to have the following packages installed for everything to
work properly (see requirements.txt):

* [Python 2.7](http://python.org)
* [pelican](http://getpelican.com/)
* [typogrify](https://github.com/mintchaos/typogrify)
* [ghp-import](https://github.com/davisp/ghp-import)

Non-Python dependencies
-----------------------
* [Make](http://en.wikipedia.org/wiki/Make_(software)]
* [sass-lang](http://sass-lang.com/)

````
    $ gem install sass
    $ sass -v
    Sass 3.3.8 (Maptastic Maple)     
````

Building
--------

Use the following to build the and serve the site locally:

    make html 
    make serve

To edit content and have the local repo update continually, you can use the dev server. Just remember to shut it down later.

    make devserver
    make stopserver

Deploying
----------

The site is deployed as a github page (see https://pages.github.com/ ). Use the following to push the results up to github:

    make github

For this to work, please set your github remote 'upstream' to 
'git@github.com:numfocus/numfocus.org.git'.

For more targets (such as debug to find errors) run:

    make help

