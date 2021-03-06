---
layout: post
title: Creating a developer blog with Jekyll
---
In this blog post I'm going to show how to quickly start a simple blog with the tool that you as a developer use daily and hopefully are most familiar with, Git.

We will use a popular blog engine called **Jekyll** that uses markdown syntax, which is "compiled" into static blog pages. For hosting we choose **Github Pages**, and we will look at how to set it up with your own custom domain. After getting the blog up we will link the blog to your other social networks, followed by adding **Google Analytics** for, and last we look at **Google Webmaster Tools** to hint Google to crawl and index your site.

Prerequisites: Basic git knowledge.

Overview
---

 1. Playing with Jekyll
 2. Hosting on Github Pages
 3. Adding Social Networks
 4. Insight with Google Analytics
 6. Simple Search Engine Optimization SEO

Playing with Jekyll
---
Jekyll is an open-source project used to build static web sites. It has a build in support and convention for blog post but can support any custom site. 

The Jekyll engine is written in Ruby but don't worry, you need no Ruby skills, or even set-up. In this blog post we will use GitHub as our host/engine. If your interested in running Jekyll locally take a look at my blog post on Docker where I set up a ruby environment on a Windows machine to compile and run Jekyll in (*Upcoming*...). 

#### Content files
The main object in Jekyll is the content files. This is where your text will be. Several formats are supported but I will use markdown. In markdown you us plain text with small markers to describe text formatting. Markdown makes it simple and fast to write rich text documents. The content files can be stored anywhere under the Jekyll folder but convention for blog posts is under the _post folder. 

For a quick markdown kick-start, try out the free online markdown editor [StackEdit](https://stackedith.io). 

At the top of the content file are a few lines of metadata in the format of a key-value list. The most important is the *Layout* property with tells the Jekyll engine which layout to choose.

#### Layout templates
The layout template is a simple .html file with standard HTML and CSS, and has built in support for SASS. There are two important and specific code blocks that can be inserted into the layout. 

The first is {{include 'html file'}} to include html from another file, typically used for header and footer which are the same for all templates. 

The second is  {{ content }} which specify where the text from the content file should be included. 
 
Standard Jekyll includes two layouts, default and post. By convention the layouts are placed in the _layout folder.

#### Config file
All your personal settings are stored in the _config.yaml file. This is a key-value list that we will look more into when we personalize the blog.

#### Templates and forks
There are many different templates for Jekyll that you can choose from. There are also a few forks that not only change the theme and sass files but also add some extra functionallity. I choosen a project called [Jekyll-Now](https://github.com/barryclark/jekyll-now) because it had extra support for Google Analytics, and Disqus. And there is a repository to clone from.

#### Clone start template
Open up git and clone the following

    git clone https://github.com/barryclark/jekyll-now.git

Now you got all the files you need on your computer. Look them through and familiarize yourself to the different building blocks.

#### Hello World blog post
Create a new file in the _post folder. The filename should include the date of the post followed by unique describing title. This title will be the url for the post. An example of a filename is `2015-04-01-Hello_World`. Inside the file there are two sections, a key-value section, and the blogpost content. The key-values informs Jekyll of which layout to choose and which title to set. You can add extra parameters here that can be used inside the layout templates. A full Hello World example blog post would then look something like

	---
	layout: post
	title: Foreign keys - the key to open up the monolith
	---
	**Hello World!**
*Filename:* 2015-04-01-Hello_World.md

Hosting on Github Pages
---
The simplest hosting for your Jekyll pages is directly on Github. There are two different places for your sites, on your personal account or on one of your projects. For a personal account site you need to create a repository called YourUserName.github.io and check in your code in the "master" branch. For a project site the Jekyll code needs to be checked in on the project repository, but in a separate branch called "gh_pages". In this tutorial I will use and create a personal account site.

Log in to github (after createing a new account if you don't already have one) and create a new repository called YourUserName.github.io. We no want to connect the Jekyll-now repository we cloned in Part 1 to our new repository. Rename the folder if you like and then run the following commands from inside the new folder,

	# Point origin to your site (if you use https authentication)
	git remote set-url origin https://github.com/YourUserName/YourUserName.github.io.git
	# or (if you use SSH-key authentication)
	git remote set-url origin git@github.com:YourUserName/YourUserName.github.io.git
	
	# Use simple mode (the new git standard) for push.
	git config --global push.default simple

	# Push your code to Github
	git push

 Start now by browsing your Github repository at `github.com/YourUserName/YourUserName.github.io`. You should see all your files already here. If they are you can go to the specific website `YourUserName.github.io`.
#### Custom domain
Next step is to link a custom domain to your site. Go to your favorite domain name registrar and register a unique domain name. I chosed [Binero.se](http:/www.binero.se) because they have the CNAME alias function on there free account, and I also used them with positive results before. Go to DNS settings and add a CNAME for `www.YourSite.com` pointing to `YourUserName.github.io`. 
The last step is to let Github know about the link. Create a new file called `CNAME` in the root folder of your repository. Give it just a single line 
	
	www.YourSite.com
 
Now it's only to wait for these changes to mirror out to all the DNS servers. The domain name registrar warned that this could take up to 3 hours but for me I reached my Github hosted site via my domain address after only 20 minutes.
 
 Adding Social Networks
---
 One of the reasons for choosing Jekyll-Now over standard Jekyll is the extended out-of-the-box support for social networks. In the `_config.yaml` file we find the following list of key values:

	# Includes an icon in the footer for each username you enter
	footer-links:
		dribbble:
		email:
		facebook:
		flickr:
		github:
		instagram:
		linkedin:
		pinterest:
		rss: # just type anything here for a working RSS icon, make sure you set the "url" above!
		twitter: 
		stackoverflow: # your stackoverflow profile, e.g. "users/50476/bart-kiers"
		youtube: # channel/<your_long_string> or user/<user-name>
 
Now it's just to go to all of the different networks, open an account if you don't already have one, then go back an fill in the username in the right place in the list above. 
####Allowing comments
Now when readers can see who you are it's time to let them discuss and comment on your blog posts. This is what the disqus widget is for. Look further down in the `_config.yaml` file and find the disqus key-value: 
	
	# Enter your Disqus shortname (not your username) to enable commenting on posts	
	# You can find your shortname on the Settings page of your Disqus account
	disqus: 
If you go slow and carefully read the instruction you will notice that it's not the username you should enter. Given the right shortname it works like a charm.

Insight with Google Analytics
---
####Analytics
When writing blog posts it is interesting to know more about your readers. Do you actually have any readers at all? Are the returning? Did they found your site on a search engine or did they follow a link? All these type of questions are answered by Google Analytics.
 
Start by signing on and register to [Google Analytics](http://www.google.com/analytics) with your gmail account. Pick an account name, a website name and give the url to the web page. Click on the "Get tracing-ID" button. You will now be redirected to the admin page where you can see your tracing id. This is a site unique id that is sent to google every time your site is loaded. This Id you have to enter into the Jekyll config file. 

Ohh, I almost forgot to tell you. Once you got Google Analytics up and running you will notice that you get a lot of hits from suspicious users and crawler engines. These are called refferer spam, and just like email spam you should not follow the links. A good article on how to filter your analytics from spam is found here: [What is referrer spam and how to stop it - Guide](http://www.ohow.co/what-is-referrer-spam-how-stop-it-guide/).
####Webmaster Tools
**_If it not on Google it doesn't exist_**, therefore we want to help Google to crawl your page. This is done in the Webmaster tools. 

On the admin site of Google Anayltics go to the property settings for your site. At the very bottom there is a choice for Webmaster Tools settings. Click on the Edit, and you get redirected to [Webmaster Tools](www.google.com/webmasters). Now you can add the site to Webmaster Tools and link it back to your analytics account.

In the webmaster tool you can go to Crawl and "Fetch as Google". First force Google to fetch your site, and then submit the collected info. You can do this a limited times a month, but once Google found your site it will continue to crawl it automatically. If you come back to the webmaster tools after a few days you can find more info about the crawl, if it found any problems, which words it rated the highest, which external sites that are linking to your site, and much more.

Summary
---
That's it. Hopefully you, just like me, now have a running static Jekyll blog hosted on gitpages. 