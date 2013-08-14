## Getting started

Because I always forget how to use RVM.

### Install RVM

Use the [RVM docs](https://rvm.io)

### Use the `source` branch

The master branch is the statically-built
deployable version.
Change things on the `source` branch.

    $ git clone git@github.com:winhamwr/winhamwr.github.com.git
    $ cd winhamwr.github.com
    $ git checkout source

Note: If you get a message about installing ruby when you cd,
follow the instructions
to install that version with `rvm`.

### Install all the things

    $ bundle install

## Create a new blog post

    $ rake new_post["Awesome New Title"]
    $ gvim source/_posts/<date>-awesome-new-title.markdown

hack hack hack

    $ git commit source/_posts/<date>-awesome-new-title.markdown
    $ git push

## Deploy

I forget?


## What is Octopress?

Octopress is [Jekyll](https://github.com/mojombo/jekyll) blogging at its finest.

1. **Octopress sports a clean responsive theme** written in semantic HTML5, focused on readability and friendliness toward mobile devices.
2. **Code blogging is easy and beautiful.** Embed code (with [Solarized](http://ethanschoonover.com/solarized) styling) in your posts from gists or from your filesystem.
3. **Third party integration is simple** with built-in support for Twitter, Pinboard, Delicious, Disqus Comments, and Google Analytics.
4. **It's easy to use.** A collection of rake tasks simplifies development and makes deploying a cinch.
5. **Ships with great plugins** some original and others from the Jekyll community &mdash; tested and improved.

## Documentation

Check out [Octopress.org](http://octopress.org/docs) for guides and documentation.

## License
(The MIT License)

Copyright © 2009-2011 Brandon Mathis

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the ‘Software’), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED ‘AS IS’, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

#### If you want to be awesome.
- Proudly display the 'Powered by Octopress' credit in the footer.
- Add your site to the wiki so we can watch the community grow.
