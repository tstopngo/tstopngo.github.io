---
layout: post
title:      "Can Rake, rake my lawn? "
date:       2019-06-14 04:48:11 +0000
permalink:  can_rake_rake_my_lawn
---



When I first started learning about Rake, I was very confused as to what it was doing. I know that it was "automating" tasks for me, but what exactly was it automating?  Is it going to rake my lawn for me?

I would write the tasks in the FlatIron lab because understand the syntax and how to use it in the terminal but it didn't quite click for me until I ran into another lab where I had to manually right click to create the db folder and create a migration file and label it 01_create_users.rb. 

Imagine having to right click to create the DB folder, then under the db folder right click and create Migrate folder, and THEN under that adding the file 01_create_users.rb every single time that you needed to set up the database. It's fun the first few times when you're first learning to code, but not so fun when you have a few more labs to do and need to set up a database thens when I REALLY undestood the benefits of Rake.

What if...you could in theory automatically create the folder for **db** and **migrate** and the file with a timestamp? That's where the beauty of Rake comes in. The Rake Gem comes with automatic tasks for you. For example, did this in my terminal:

```
rake db:create_migration NAME = 'create_users'
```

It would automatically create both folders for you with **migrate** nested under **db** AND create a file for you with the timestamp. When I saw the folder magically appear in my atom with the folders and files this is when I truly understood the beuty of the the Rake Gem and what it was capable of "automating".

I think that without having gone through the pain point of manually creating the folder and seeing it done for me with the db:create_migration  for me I wouldn't have really understood it.


Another thing I learned from testing was the importance of the rakefile if you tried to run the comman above without a rakefile it does not work. Ruby will look for the rakefile otherwise it will automatically abort. So what is this rakefile?

Upon messing around in my terminal I noticed that if you have an empty rakefile to satisfy the first error of it aborting, you'll get another error that about path. Well rakefile is needed so that when you run your rake commands it looks at your files and executes the code in those files. So if you had set up table it will execute that file and create that table for you. 

What's nice about the rakefile is if you wanted to write your own tasks specific to your application. For example, maybe you want to run some test to delete all the files under a folder or clean up the naming in your files you can do that with rake! 

In summary, while rake might not rake your lawn, it will rake your code and take care of some things for you, which is also nice. 


