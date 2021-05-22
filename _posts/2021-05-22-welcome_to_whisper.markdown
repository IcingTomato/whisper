---
layout: post
title:  "Welcome to Jekyll for Whisper Theme!"
date:   2021-05-22 10:00:00
categories: post welcome
---

You'll find this post in your `_posts` directory - edit this post and re-build (or run with the `-w` switch) to see your changes!
To add new posts, simply add a file in the `_posts` directory that follows the convention: `YYYY-MM-DD-name_of_post.markdown`.

<!--more-->

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

If you want to post this site on your ECS or VPS, please follow the code block to configuration this theme:

{% highlight shell %}
git clone -b main http://github.com/ch1hfe1/whisper.git
cd whisper
gem install jekyll
gem install jekyll-paginate
jekyll build -d /var/www/html/
{% endhighlight %}

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll's GitHub repo][jekyll-gh].

[jekyll-gh]: https://github.com/mojombo/jekyll
[jekyll]:    http://jekyllrb.com
