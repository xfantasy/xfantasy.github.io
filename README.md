jekyll-blog-template
===========

This repository provides a good starting point for a [Jekyll](https://github.com/mojombo/jekyll) blog. 

The blog comes set up with these features:
* valid HTML5 layout
* [CSS reset](http://meyerweb.com/eric/tools/css/reset/)
* [RSS feed](http://cyber.law.harvard.edu/rss/rss.html)
* [Apache](http://www.apache.org/) .htacess files to enable caching, charset, and 404 page.
* link rel="canonical/prev/next" tags to help search engines.

Getting started
---
Jekyll is [Ruby](www.ruby-lang.org) software, which means you'll first need to install Ruby. You might want to consider using [RVM](https://rvm.io/).
Once you have Ruby, download the template:
```
git clone git://github.com/ericlathrop/jekyll-blog-template.git
cd jekyll-blog-template
```
Then set up the required Ruby libraries:
```
gem install bundler
bundle install
```
Now you can run Jekyll with a built-in web server:
```
jekyll --server --auto --url http://localhost:4000
```
Point your web browser at http://localhost:4000 to see the site! If you leave Jekyll running, it will automatically update the affected pages.

Further Reading
---
Read more documentation at the [Jekyll wiki](https://github.com/mojombo/jekyll/wiki)
