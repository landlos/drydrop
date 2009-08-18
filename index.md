---
title: DryDrop
subtitle: deploy GAE sites by pushing to GitHub
layout: product
icon: /shared/img/drydrop-icon.png
repo: http://github.com/darwin/drydrop
support: http://github.com/darwin/drydrop/issues
downloadtitle: Install v0.2
download: http://github.com/darwin/drydrop
downloadboxwidth: 120px
donate:
subdownload: 
subdownloadlink:
mainshot: /shared/img/drydrop-mainshot.png
mainshotfull: /shared/img/drydrop-mainshot-full.png
overlaysx: 1109px
overlaysy: 856px
overlaycx: 25px
overlaycy: 10px
---

<div class="advertisement">
	<div class="plug">Recommended reading:</div>
	<a href="http://www.amazon.com/gp/product/0596009259?ie=UTF8&tag=firepython-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0596009259"><img border="0" src="/shared/img/amazon/41QbTFszYTL._SL110_.jpg"></a><img src="http://www.assoc-amazon.com/e/ir?t=firepython-20&l=as2&o=1&a=0596009259" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />
	
	<a href="http://www.amazon.com/gp/product/0596158068?ie=UTF8&tag=firepython-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0596158068"><img border="0" src="/shared/img/amazon/41Mu5RWG-1L._SL110_.jpg"></a><img src="http://www.assoc-amazon.com/e/ir?t=firepython-20&l=as2&o=1&a=0596158068" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />

	<a href="http://www.amazon.com/gp/product/0596007973?ie=UTF8&tag=firepython-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0596007973"><img border="0" src="/shared/img/amazon/41S-nPeF89L._SL110_.jpg"></a><img src="http://www.assoc-amazon.com/e/ir?t=firepython-20&l=as2&o=1&a=0596007973" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />
	
	<a href="http://www.amazon.com/gp/product/1430210478?ie=UTF8&tag=firepython-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=1430210478"><img border="0" src="/shared/img/amazon/516STCBRnOL._SL110_.jpg"></a><img src="http://www.assoc-amazon.com/e/ir?t=firepython-20&l=as2&o=1&a=1430210478" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />
	
	<a href="http://www.amazon.com/gp/product/059652272X?ie=UTF8&tag=firepython-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=059652272X"><img border="0" src="/shared/img/amazon/513CiT5BtYL._SL110_.jpg"></a><img src="http://www.assoc-amazon.com/e/ir?t=firepython-20&l=as2&o=1&a=059652272X" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />
	
	<div class="offer"><a href="mailto:antonin@binaryage.com">advertise here</a></div>
</div>
<script type="text/javascript" src="http://www.assoc-amazon.com/s/link-enhancer?tag=firepython-20&o=1">
</script>

## Features

#### Host your static site on Google App Engine and update it by pushing to GitHub.

DryDrop is a tool that lets you host your static site on Google App Engine and update it by pushing to GitHub. Thanks to GitHub post-receive hooks your App Engine site can be updated automatically when you push new content.

* DRY principle (set it up and forget)
* Zero cost (thanks to [Google App Engine][appengine])
* Zero maintenance (thanks to [GitHub][github])
* No Python knowledge needed, but you need to know basics of Git

### How it works

It is simple. Let's say you have GitHub repo containing static web site and you want to host it on App Engine. DryDrop is an application ready to be uploaded as your App Engine project. After you upload it first time, you should setup post-receive hook in your GitHub repo to point to your App Engine project, so every change you push to GitHub may be reflected on your App Engine site immediately.

Let's say someone visits your App Engine site. DryDrop has a simple cache. If requested page is not in the cache, DryDrop will try to fetch it from GitHub, store it in the cache and then serve it. Next time the same URL is requested, it will be served directly from DryDrop cache.

Let's say you did some changes to your files. In the moment you push file changes into GitHub, post-receive hook will ping DryDrop and that invalidates modified files in the cache. Next request will trigger downloading of fresh files from GitHub.

## Installation

- upload your static files as GitHub repository
- create GAE project and upload DryDrop
- point DryDrop site to your GitHub repo
- (optional) setup post-receive hook in GitHub repo pointing to your DryDrop site

#### Since then, every change pushed to github project will automatically propagate to your static site hosted by Google.

### Step 1: prepare your GitHub repository

You already know how to work with GitHub, right? 

Let's say you are user `darwin` and created repository `web-app-theme`.
So, your repository's content lives at <a href="http://github.com/darwin/web-app-theme/tree/master">http://github.com/darwin/web-app-theme/tree/master</a>

### Step 2: create your App Engine project and upload DryDrop

Now you've created project called `drydropsample` like this:

<a href="/shared/img/drydrop-create-app.png"><img src="/shared/img/drydrop-create-app.png" width="300"></a>

Then make sure you have latest <a href="http://code.google.com/appengine/downloads.html">Google App Engine SDK</a> available on your machine.

Then you have to download latest DryDrop and upload it to drydropsample project:

    git clone git://github.com/darwin/drydrop.git
	cd drydrop
	rake upload project=drydropsample
	
Note: You will be prompted for user name and password for your Google account by appcfg.py script.

My session looked like this:

<a href="/shared/img/drydrop-upload.png"><img src="/shared/img/drydrop-upload.png" width="300"></a>

Now you can visit your App Engine site at <a href="http://drydropsample.appspot.com">http://drydropsample.appspot.com</a> and you should see welcome page:

<a href="/shared/img/drydrop-welcome.png"><img src="/shared/img/drydrop-welcome.png" width="300"></a>

### Step 3: point DryDrop site to your GitHub repo

Go to admin section of your DryDrop site and switch to settings page:

<a href="/shared/img/drydrop-settings.png"><img src="/shared/img/drydrop-settings.png" width="300"></a>

Set "Pull from" to `http://github.com/darwin/web-app-theme/raw/master`. That "raw" in the URL is important!!!

When you go back to <a href="http://drydropsample.appspot.com">http://drydropsample.appspot.com</a>, you should see your repo's content (in case you have there index.html)

<a href="/shared/img/drydrop-site.png"><img src="/shared/img/drydrop-site.png" width="300"></a>

### Step 4 (optional): setup post-receive hook in GitHub repo pointing to your DryDrop site

Go to Admin section of your GitHub repo:

<a href="/shared/img/drydrop-hook.png"><img src="/shared/img/drydrop-hook.png" width="300"></a>

Set `http://drydropsample.appspot.com/hook/github` as post-receive hook.

### Step 5 (optional): test the hook

Now, let's try to push some change and check if it gets auto-published on <a href="http://drydropsample.appspot.com">http://drydropsample.appspot.com</a>.

<a href="/shared/img/drydrop-edit.png"><img src="/shared/img/drydrop-edit.png" width="300"></a>

Push it to GitHub ...

<a href="/shared/img/drydrop-push.png"><img src="/shared/img/drydrop-push.png" width="300"></a>

When you revisit <a href="http://drydropsample.appspot.com">http://drydropsample.appspot.com</a>, you should see updated version:

<a href="/shared/img/drydrop-updated.png"><img src="/shared/img/drydrop-updated.png" width="300"></a>

You can double check situation in admin section under Dashboard events:

<a href="/shared/img/drydrop-events.png"><img src="/shared/img/drydrop-events.png" width="300"></a>

Post-receive hook was triggered as you can see in the events list.

#### And that's it... Happy pushing! :-)

## FAQ

#### Do I need to understand Python to use this?
> Not at all. You just need to know how to use Git and how to create App Engine project on appspot.com.

#### How does DryDrop compare to <a href="http://pages.github.com">GitHub Pages</a>?
> GitHub Pages is solving same need of "live-hosting of GitHub repository as a static site on custom domain". I've started this project before GitHub Pages was announced and GitHub pages made it somewhat obsolete, especially because they support <a href="http://github.com/mojombo/jekyll/tree/master">jekyll</a>, which is cool. But I still see two valid use cases: 1) you have public repo and you don't want to pay for CNAME support on GitHub 2) GitHub had some performance issues recently, App Engine works more reliably and is really fast.

#### How can DryDrop serve files from GitHub?
> It is simple. DryDrop has a simple cache. If requested page is not in the cache, DryDrop will try to fetch it from GitHub, store it in the cache and then serve it. Next time the same URL is requested, it will be served directly from DryDrop cache. Let's say you did some changes to your files. In the moment you push file changes into GitHub, post-receive hook will call DryDrop and DryDrop will invalidate modified files in the cache. 

#### What if I want pretty URLs or some kind of routing?
> You can define `site.yaml` config file which defines mapping between your repository files and App Engine URLs. This config uses subset of App Engine's <a href="http://code.google.com/appengine/docs/python/config/appconfig.html">app.yaml syntax</a> and is kept in your GitHub repo, so you don't need to re-upload DryDrop after changing it. See admin/settings section of your DryDrop site for more info.

#### What about markdown/textile or some kind of static site generator like jekyll?
> You can use anything you want locally and push generated outputs into your github repo. You can point DryDrop site to subfolder of your GitHub repo, even to different branch, so you have quite flexible options how to keep original source with generated output in one repo. I'd prefer to keep DryDrop simple, but you are welcome to add support for your favorite stack.

#### Are you going to support bitbucket or some other code repository services?
> Maybe, if there is a demand for it.


## History

  * **v0.2** (09.08.2009) 
	* introducing support for GitHub and GitHub hooks
	* initial public version

  * **v0.1** (13.12.2008) 
	* initial experimental implementation
	
## Links

### Articles

  * [DryDrop mentioned on Google App Engine Blog](http://googleappengine.blogspot.com/2009/08/recent-happenings-ticktock-parallel.html)

### Related Sites
  * [GitHub][github] - social code hosting

[appengine]: http://code.google.com/appengine
[github]: http://github.com