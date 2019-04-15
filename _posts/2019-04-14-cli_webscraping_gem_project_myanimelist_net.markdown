---
layout: post
title:      "CLI Webscraping Gem Project: MyAnimeList.net "
date:       2019-04-15 03:46:27 +0000
permalink:  cli_webscraping_gem_project_myanimelist_net
---


When I first embarked on this project I had many ideas I wanted to try, but the most important thing was to build something that I would use that I would continue to expand and iterate upon. This brings me to the site I selected which was myanimelist.net. The site is used to see reviews, rating and add them to your list to track if you are watching, completed, or intend to watch the show, but one thing the site does not do well is allow you to filter the information that can be overwhelming when you just want to see maybe 4-5 shows you might be interested in.

Once I decided on my site I ran it through a quick check by adding robots.txt after the URL to see if there were any pages that I would be scraping from that would be restricted. Next, I used Nokogiri and Open URI to run a quick test if it would return objects for each show on the site. Finally, I did a quick inspection of the site to see if I would run into any roadblocks with the the data I wanted from the show in the event the site had jQuery for the pieces of information that I wanted to select from the site.

After I verified the site it was time to set up the project. This was by far the most difficult part moving away from the Learn IDE and setting up my local enviornment to start coding. Also ensuring that all of the files were set up correctly. A few things Iearned from the set up was the namespacing that is created if use 'bundle gem" [insert gem name] that creates a gem set up for you. It creates a module for you which allows doesn't seem to do much but creates a module of the name of your gem and then use it in the rest of your lib files. This ensures that if you have a file called scraper.rb for example it does clash with someone else's gem if they also had a scraper.rb. 

The next part was finally writing the code, this part was the most fun as I came to realize how much I had learned in the past two months. I learned quite a bit about program design while I wrote out my program. Creating separate classes and files to hand off data to each other and create the interaction for the end user. If I didn't understanding anything about scraping, I definitely understood it after creating the gem for this project. I also ran into several issues when writing my code as I was trying to figure out to continuosly provide options for the user and handle errors when the user put something in wrong. I iterated over this several times. 

As I iterated over the project, I was also learning how to use git in the terminal for the first time. I figured out how to initialize, create a remote, add my files, commit, and push to Github. I accidently ended up in vim while commiting files to Github. ALWAYS commit with a message. People have mentioned how awful vim is and I realized actually how bad it was when I ended up there super confused. Good thing I had a friend save me and tell me what was happening. 

It feels like such a great accomplishment to have written something that is working from scratch! I would love to continue working on this further to allow to filter anime down by genre with some of the knowledge I have, be able scrape two sites and allow for the infromation from the first scraped site to pull information from the second scraped site, or have some way to store all of the data from MAL into some form of database since the site is quite static so that I am not scraping the site all the time and only scrape when there is no season data.


