## To use the log

Install [Jekyll](http://jekyllrb.com/). Edition was built with [Jekyll](http://jekyllrb.com/) version 3.3.1, but should support newer versions as well.

Install [Ruby](https://www.ruby-lang.org/en/downloads/), if necessary.

With command line, cd into folder:

Install the dependencies with [Bundler](http://bundler.io/) (`gem install bundler` if you don't have it):

~~~bash
$ bundle install
~~~

Run `jekyll` commands through Bundler to ensure you're using the right versions. This allows a preview version on local host:

~~~bash
$ bundle exec jekyll serve
~~~

### How to edit the site

* Add, update or remove a documentation page in the *Documentation* collection.
* Change the category of a documentation page to move it to another section in the navigation.
* Documentation pages are organised in the navigation by category, with URLs based on the path inside the `_docs` folder.
