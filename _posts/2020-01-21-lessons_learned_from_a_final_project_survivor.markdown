---
layout: post
title:      "Lessons Learned from a Final Project Survivor"
date:       2020-01-22 01:09:31 +0000
permalink:  lessons_learned_from_a_final_project_survivor
---


I have finally reached the final project– and survived. While working on the project I jotted some, note to self, please don't do this again to yourself.


There were some traumatic lessons learned from this project:


## 1. USE THE RAILS NEW --api. 

I wish I knew this before starting my project. I spent 2 days debugging my code trying to figure out why I was not able to post to my backend. Why? Because apparently, when you create using rails new, it adds a few Gems that require you to get a authenticity token to pass to the backend. 

While in some cases this might make sense, it didn't make sense to have this feature since I wanted anyone even if they were in another application to be able to post to my database given they had the API. I had to go the Rails controller for my Log and add :

 `:skip_before_action :verify_authenticity_token`
 
 This one single line of code, allowed me to post. Now if I had just created the Rails using the --api tag, it would have removed the unecessary code that caused me not to be able to post correctly. So, if you're out there reading this. You're welcome.
 
 
 ## 2. Start with the Back End?
 
When starting the project I started the Front End because that was most fresh in my mind and I could at least create a state of how I wanted my app to work , or so I thought. This decision ultimately led to me spending a little extra time to refactor the code so that I could dispatch actions and fetch from my backend. I'm not sure how most developers work, but next time I work on an app I would probably start from my back end first so I wouldn't have to do so much of the refactoring. I needed to re-write and move stuff around to ensure it was fetching and posting correctly.

## 3.  Check your Spelling. No, seriously.

The first part I refactor was the fetch action, and while this seemed straight forward enough I mapped the dispatch to the props, made sure that the props was passed down to the correct component, and made sure my reducer included the case for the action. Here's where I messed up, writing the action. In my reducer I had ADD_LOG, which was to add a brand new log. Cool, makes sense. Then I had another one for ADD_LOGS, this one was to add logs to my state when I fetch from the endpoint. When writing my fetch action to render all the logs from the database, when I dispatched my action I noticed that it would get to the promise, give me a response, and then die. 

When in doubt, open up your console, or just use consle.log to print things to know how far your program made it to. I finally went back to my action that I wrote and read through it line by line. I had ADD_LOG instead of ADD_LOGS. I think my heart broke at this point, but I was so glad that it was working.

## 4. 422 unprocessable entity error

The next issue I ran into was related to part 1 which was the skip before action, but also because of my data shape. 

When I first ran into the error I googled it immediately and learned 2 things: there are a lot of errors out there and this one is very close to the 400 error with one key difference that this means the structure was correct, but when I was sending it over it didn't mean anything because it did match with anything in the data base.

Again, I can't express how important it is to console.log your variables if you're unsure what they look like. You need to make sure that you are passing in the correct format in order for it to post. You can either add breakpoints in your console and check out what the variable is at specific time points in your application. From here, you can better understand what the data looks like, how to pass it to your back end so that it gets into your data base correctly. Once I figured out the data structure component thanks to the help of a tech coach, the second part was also to ensure that the method was added to my class.

For example:

```
body: JSON.stringify({log:data}) vs body: JSON.stringfy({data})
```

console.log your data and response to see what it looks like or just add debuggers to see what's happening.

## Conclusion

While these are few lessons I learned along the way, yours may be different, but I hope that if someone out there can be saved from my mistakes then I'll be glad this blogpost was somewhat useful. 

tl;dr, when it doubt console.log or add breakpoints :)








 
