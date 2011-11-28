--- 
layout: post
title: Setting up node.js and npm on Mac OSX
excerpt: node.js is gaining a lot of speed and is an exciting new development framework. Here's a quick overview of how to get node.js working on OSX along with npm, the package manager for node. 
categories: [node.js, JavaScript]
---

Update: There is now also a [package available][12] for OSX if you prefer a one click install for NodeJS and NPM.

## Install Homebrew

[Homebrew][1] is the package manager that Apple forgot. Written in Ruby it allows you to quickly and easily compile software on your Mac. Instructions for installing Homebrew are in the [README][2] so I won't repeat them here. You will need to install Developer Tools for Mac which you are installed as part of [Xcode][3]. Xcode is available for free - it is a pretty hefty download but you'll need it.

## Install node.js via homebrew

Once Homebrew is installed you can go ahead and install node.js

{% highlight bash %}brew install node{% endhighlight %}

Easy! Now create a file called server.js and paste in the example server code

{% highlight javascript %}var http = require('http');
http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Hello World\n');
}).listen(8124, "127.0.0.1");
console.log('Server running at http://127.0.0.1:8124/');
{% endhighlight %}

Save the file and from the console run

{% highlight bash %}node server.js{% endhighlight %}

Now you can visit http://127.0.0.1:8124/ with your favourite browser and you are up and running with server side JavaScript.

At this point it is probably a good idea to consult the excellent [node.js documentation][4]. This will help you understand what node.js is and what it can do. 

## Installing npm

node.js is pretty low level so lots of people have created modules for node. Thankfully there is already a package manager for node in [npm][5] to help you manage these.

For [various reasons][10] the package was recently removed from Homebrew so you'll need to install it manually.

{% highlight bash %}curl http://npmjs.org/install.sh | sh{% endhighlight %}

If executing scripts from curl makes you nervous you can download the source and then install:

{% highlight bash %}git clone http://github.com/isaacs/npm.git
cd npm
sudo make install
{% endhighlight %}

The install will spit out some advice about paths. I found on my setup everything worked other than having to set NODE\_PATH. 

NODE\_PATH tells node.js where to look for modules. This means you can do things like 

{% highlight javascript %}var client = require 'redis-client'{% endhighlight %}

instead of specifying the full path.

To make sure my shell knows where to find node modules I added 

{% highlight bash %}export NODE_PATH="/usr/local/lib/node"{% endhighlight %}

to my .bashrc file. As some modules have executables you will also need to add /usr/local/share/npm/bin to your PATH. Here's how mine looks

{% highlight bash %}export PATH="/usr/local/bin:/usr/local/sbin:/usr/local/mysql/bin:/usr/local/share/npm/bin:$PATH"{% endhighlight %}

My full .bashrc file is [available here][11] if you need an example. Make sure you reload your shell with 

{% highlight bash %}source ~/.bashrc{% endhighlight %}

so the changes are applied.

## Installing modules

Now we are set up we can install node modules using npm. [Express][6] is a good place to start - it is a node framework inspired by [Sinatra][7]. 

{% highlight bash %}npm install express{% endhighlight %}

This provides a solid base to start developing with node.js including [jade][8] the haml inspired node tempting engine. There is more [excellent documentation][9] available for express too.

That's it - go create!

[1]: http://github.com/mxcl/homebrew
[2]: http://github.com/mxcl/homebrew/blob/master/README.md
[3]: http://developer.apple.com/technologies/xcode.html
[4]: http://nodejs.org/api.html
[5]: http://github.com/isaacs/npm
[6]: http://expressjs.com/
[7]: http://www.sinatrarb.com/
[8]: http://jade-lang.com/
[9]: http://expressjs.com/guide.html
[10]: http://blog.izs.me/post/3295261330/on-npm-and-homebrew
[11]: https://github.com/shapeshed/dotfiles/blob/master/bashrc
[12]: https://sites.google.com/site/nodejsmacosx/