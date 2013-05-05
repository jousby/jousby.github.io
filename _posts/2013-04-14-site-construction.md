---
layout: post
title: "Notes on how I built this site"
---

This post is primarily a documentation exercise but in case your curious...

### Github Pages

Follow these pages for creating a 'user' repo/page in github and pointing a custom domain name at it:

- [Github User Page] (https://help.github.com/articles/user-organization-and-project-pages)
- [Github Custom Domain Name] (https://help.github.com/articles/setting-up-a-custom-domain-with-pages)

### Domain Name

I used [Crazy Domains] (http://www.crazydomains.com.au/) to register my domain name ($3 AUD/yr) and added 
DNS services ($12 AUD/yr) required for redirecting my domain to github pages as outlined in the Github
Custom Domain Name instructions. 

<!--more-->

### Jekyll

Jekyll is the static site generator used internally by Github to power 
Github Pages. If you upload a Jekyll project to your master branch on your 'user' page then Github will 
generate and serve up the resulting site for you. You are also free to use another 'static site generator' 
or just write some plain old html and upload the resulting to your master branch to be served as is. 

I started using [Jekyll Bootstrap] (http://jekyllbootstrap.com/) which provides some extra ruby magic to add theme
support and do some of the more common things you might want to do with a blog like add anaytics tracking, a
comments provider etc. I would still recommend it and it's a great way to learn how some of these features work. 

I then decided that starting with a barebones Jekyll site and building it up with just the pieces I needed would
be an interesting learning exercise. This github repo is what I used as my barebones Jekyll starting point 
[jekyll-starter] (https://github.com/cnunciato/jekyll-starter).

But something to watch out for when using Jekyll and Github Pages ...

### Github Pages doesn't let you run Jekyll Plugins

Unless you have really simple blog requirements then you will probably end up wanting to make use of one of the
many Jekyll plugins that are available. Unfortunately Github Pages doesn't let you run arbitrary plugins as part
of the site generation process. As soon as you add a plugin you are looking at having to generate the site
before pushing to your remote, rather than letting Github do the generation for you. It's not really a big deal 
but once your at this point then there is no real advantage to using Jekyll as the static site generator, you may
as well be using one of the many other static site generation tools out there. It's been an interesting learning
experience so far but down the track I may look at whats available in Java / Scala to see how they stack up.

I ended up using the following Jekyll plugins:

- [Post Summaries Solution] (http://stackoverflow.com/questions/10859175/how-to-show-a-preview-of-a-post-using-jekyll-bootstrap-theme)
- [Less Pre Processing] (https://github.com/zroger/jekyll-less)
 
I then used the approach outlined on this blog for pushing my site source code to a 'source' branch and the generated
site to the 'master' branch.

- [Generate Site before push to Remote](http://arademaker.github.io/blog/2011/12/01/github-pages-jekyll-plugins.html)

### Comments Provider

I used [Disqus](https://disqus.com/) as the means for allowing people to comment on my posts. There are other options
out there but in short these services all allow you to
keep the site deployment simple by avoiding the need to have a database to track and store post comments. It's
free if you are happy to have the disqus code block at the bottom of your post display some ads. After creating
a disqus account you just need to add the code block they provide to the bottom of each post. Something along the
lines of:

    <div id="disqus_thread"></div>
    <script type="text/javascript">
        {% if site.safe == false %}var disqus_developer = 1;{% endif %}
        var disqus_shortname = '<disqus-account-name-here>'; 
        /* * * DON'T EDIT BELOW THIS LINE * * */
        (function() {
            var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
            dsq.src = 'http://' + disqus_shortname + '.disqus.com/embed.js';
            (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
        })();
    </script>
    <noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
    <a href="http://disqus.com" class="dsq-brlink">blog comments powered by <span class="logo-disqus">Disqus</span></a>

### Analytics

Similar to the comments provider there are a few options here. I went with [Google Analytics](http://www.google.com/analytics/).
If you already have a google account then its as simple as logging into the Analytics website and adding a `profile`
for your site. You then get another code block that you need to include on every page. Something along the lines of:

    <script type="text/javascript">
       (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
       (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
       m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
       })(window,document,'script','//www.google-analytics.com/analytics.js','ga');
        
       ga('create', '<google tracking id here>', '<your site domain here>');
       ga('send', 'pageview');
        
    </script> 

### Site Style

> Imitate before you innovate

The design of my blog is based on a free wordpress theme from [Elmastudio](http://ari.elmastudio.de/) called Ari. There's
some really cool responsive blog design's on this site. I plan to come back and make the design of this site
responsive at a later stage. 

The other resource I found useful when attempting to come up with a site design that didn't make me physically
ill was this [Interactive Guide to Blog Typography](http://kaikkonendesign.fi/typography/section/1).

### End Result

I was really suprised you could hang all this together:

* pretty much for free (ex domain & domain redirection cost if you want your own domain)
* without using a more heavy weight blog engine like Worpdress

Heres the directory layout of my resulting Jekyll site:

![Site Folder Layout](/assets/posts/img/20130414/folder-layout.png)


