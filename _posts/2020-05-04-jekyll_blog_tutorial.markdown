---
layout: post
title:  "Plan of Jekyll Blog - Episode 1: Jekyll on Ubuntu & Nginx"
date:   2020-05-04 00:00:00
categories: post jekyll
---

This is my first blog. And this tutorial you will learn how to configure Jekyll on Ubuntu and Nginx

<!--more-->

# Jekyll On Ubuntu

The release of the Ubuntu is [Ubuntu 16.04 LTS (Xenial Xerus)](https://ubuntu.com/16-04).

You can follow this link [Jekyll on Ubuntu](https://jekyllrb.com/docs/installation/ubuntu/) to configure Jekyll

Before we install Jekyll, we need to install Ruby and other dependencies:

{% highlight shell %}
sudo apt-get install ruby-full build-essential zlib1g-dev
{% endhighlight %}

<strong>Remember, `sudo apt-get install ruby-full` command on Ubuntu 16.04 even 18.04 can only install Ruby2.5, it might take some unsuspected problem.</strong>

Avoid installing RubyGems packages (called gems) as the root user. (Well, AliCloud only provides `root` account and I am lazy about adding a new user account. So I think it doesn't matter to use `root` account.) Instead, set up a gem installation directory for your user account. The following commands will add environment variables to your `~/.bashrc` file to configure the gem installation path:

{% highlight shell %}
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
{% endhighlight %}

Finally, install Jekyll and Bundler:

{% highlight shell %}
gem install jekyll bundler
{% endhighlight %}

You can make a quick start for surfing the Jekyll blog:

{% highlight shell %}
jekyll new my-awesome-site
cd my-awesome-site
bundle exec jekyll serve
# => Now browse to http://localhost:4000
{% endhighlight %}

Or, clone the repository from GitHub and build Jekyll blog:

{% highlight shell %}
git clone https://github.com/ch1hfe1/ch1hfe1.github.io.old.git
cd ch1hfe1.github.io.old
jekyll serve
# => Now browse to http://localhost:4000
{% endhighlight %}

# Liquid warning

If you follow the step, congratulation, you cannot see any blog in your website.

Just like this:

![](../../../../../img/2020/05/04/unsuspected_error.jpg)

Well, because Ruby2.5 made its Bundler incompatible with Jekyll-4.0, so we have to uninstall Jekyll-4.0 and install the previous versions.

{% highlight shell %}
gem uninstall jekyll
gem install jekyll -v 3.1.3
{% endhighlight %}

# Jekyll Serve

`jekyll serve` will publish your site on localhost:4000. But you can change the port:

{% highlight shell %}
jekyll serve --port 4001
{% endhighlight %}

But you can't visit it on public network. So you can:

{% highlight shell %}
jekyll serve -w --host=0.0.0.0
{% endhighlight %}

After doing these jobs, we can't visit our website ethier.

# Nginx onfiguration

Because Jekyll uses port 4000, so we will make a Nginx "proxy" from port 4000 to port 80.

First, install Nginx:

{% highlight shell %}
sudo apt-get install nginx
{% endhighlight %}

Then, use your favourite text editor to edit `/etc/nginx/conf.d/jekyll.conf`:

{% highlight shell %}
root@blog:~# sudo nano /etc/nginx/conf.d/jekyll.conf

server {
    listen 80;
    server_name your.domain;
    location / {
        proxy_pass http://localhost:4000;
    }
}
{% endhighlight %}

![](../../../../../img/2020/05/04/your_domain.jpg)

Finally, `Ctrl+O` and `Ctrl+X` to save and exit, then restart `nginx.service`:

{% highlight shell %}
sudo systemctl restart nginx
jekyll serve --detach
{% endhighlight %}
