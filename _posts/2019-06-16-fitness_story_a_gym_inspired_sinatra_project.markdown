---
layout: post
title:      "Fitness Story, a gym inspired Sinatra Project"
date:       2019-06-17 01:33:04 +0000
permalink:  fitness_story_a_gym_inspired_sinatra_project
---


Ok so, when I first started thinking about what project I wanted to do for Sinatra and wrote down a number of ideas, but none of them did I actually love. The most important for me when deciding on what to do is not just getting the project done, but doing something useful for me that is practical and learning experience that I would be passionate about. While I was at the gym and entering my food logs I realized how I would have wanted a much better app that was more gamified and had more functionality.

This project is definitely something that I want to continue to work on and grow out the functionality as I progress through my learning on Flatiron, which will become a significant part of my portfolio.

The first part of the process was determining what mapping out what the user should be able to do, which was sort of outline by the project, but what types of data would I want to capture and how I would display the pages to the user. I wanted the bare minimum of entering workout calories, food calories, and what they ate that day.

After I created the login for the user I wanted from their profile page to be to add a new log and see all of their logs, access recently posted logs from other users. This is where I ran into trouble with the project.

The New Log button was giving me trouble because it was showing on all user profiles! Which I definitely did not want my users to experience. I was able to rememdy this with writing a single line of code that would display the button only under the condition that the user that was currently logged into the session could see it on their pofile page.

The other part of the proble was showing entries specific to each profile. At first I tried doing this on the view similar to the new log button and realized, oops... it showed specific entries to the user but on all profiles. Haha. Odd. I realized this was something I need to do in the controller and then pass to the user so that each user's profile would show their instances of entries.

One thing that I did learn while writing my routes was a more efficient way to check if all the fields were emtpy by grabbing all the values from the params hash and iterating through to see if any of them included empty spaces to ensure no bad data was entered into the system or an account was created. This took a bit testing and playing around in irb to discover and felt much more efficient than what we learned in the Group Project Fwitter.

All in all I had so much programming this project and I will be continuing work on this on the side and fiddling more with the CSS and handling the entries and views a bit more. Some functionality I would like to add this is documenting what was exactly done during the workout and instead of a manually entering their workout calories and food, I would want to use an API from popular exisitng apps to push into the fields to understand how that would work.






