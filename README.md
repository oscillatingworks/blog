blog
====

#### :warning:Deprecated:warning:

This is the source code of ~~[blog.oscillating.works](http://blog.oscillating.works)~~.
It's based on [Jekyll](http://jekyllrb.com/) and hosted on
[GitHub Pages](https://pages.github.com/).

Getting started
---------------

Firstly you need `ruby` installed, preferably version 2.2.0.
Run `ruby -v` to make sure you have it setup.

Done? Now you need to install all dependencies:

~~~
bundle install
~~~

> Problems when running bundle? Report an issue, so we can improve
this guide by adding a Troubleshooting section.

Running locally
---------------

You can run the blog locally with this command:

~~~
bundle exec jekyll serve
~~~

Open `http://localhost:4000/` in your browser and that's it. Jekyll takes care
of reloading automatically after every change in the application content, so
you don't need to restart the server manually.

Create a blog post
------------------

This repo comes with a nice post generator, `jekyll-post`. Run `jekyll-post -h`
to learn more about its usage. However most of the times you just need to run
the same command to create a basic blog post:

~~~
./jekyll-post -D=_posts "This is post title and it's mandatory"
~~~

You will find the new blog post file inside the `_posts` directory, ready
to be redacted.

Writting the blog post
----------------------

Blog posts are written in Markdown. If you know how to use Markdown,
then you know how to write a blog post. Remember to fill in the values
in the header as long you need them.

### Syntax Highlighting

You can use the classic code blocks in your markdown, but unfortunately
the syntax won't be highlighted. To fix this, `jekyll` parser uses `rouge`,
which is a Ruby library that set the highlighting correctly, i.e.
set this notation to provide proper syntax highlighting:

~~~markdown
{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}
~~~

Deploy
------

As this is based on GitHub Pages, you just need to push into `gh-pages` branch
to get your changes deployed. These changes can be of any kind: new posts
creation, modification of existing ones, changes in the templates, etc.


Anyway, if you are a contributor of this blog, we appreciate Pull Requests-based
deployments. This means that you can work on a separate branch, push all what you
do there, make sure that your commit history looks clean and your commit messages
are acceptable, and create a Pull Request against `gh-pages` branch. The Pull
Request will be reviewed and merged, triggering the deployment this way.

License
-------

MIT


