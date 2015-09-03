Development repo - [https://blog.torproject.org/](https://blog.torproject.org)
Linked with issue [10022](https://trac.torproject.org/projects/tor/ticket/10022)

A live copy of this repo can be found [here](http://tor.jmtodaro.com/).

This repo contains a reduced number of posts to shorten development compilation times. Get the most recent full dump of post/comment/event data at: [http://github.com/jmtodaro/tor-blog-data](http://github.com/jmtodaro/tor-blog-data).


```bash

cd ../tor-blog

gem install jekyll
bundle install
jekyll serve

```

Or build it to be served on any flat file server:

```bash

jekyll build

```
