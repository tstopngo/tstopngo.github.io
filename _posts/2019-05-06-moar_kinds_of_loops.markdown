---
layout: post
title:      "Moar Kinds of Loops"
date:       2019-05-06 20:21:11 +0000
permalink:  moar_kinds_of_loops
---


While researching on the internet I found that there are many other ways for you to write loops with Ruby. I'll discuss three examples here that I found on the internet from this site: https://www.thegeekstuff.com/2018/05/ruby-loop-examples/

In the FlatIron cirriculum I remeber learning while, until, for x in ..., loop do..., x.times and etc, but there are some other things you can do with loops that I was not aware of and found particularly useful.

## Skip One Particular Loop with Next

```
count = 1
loop do
  if count == 6
    count = count + 1
    next
  end
  puts "#{count}" " Bork Bork Bork"
  count = count + 1
  if count == 10
    break
  end
end
```

Here we can see that if the count is equal to 6 we will skip that specfic part of the loop and continue to 7 and continue to "bork" until the counter hits 10. This is done by adding logic that checks the count and putting "next" at the end of the if statement.

## Adding While at the end

```
count = 1
begin
  puts "#{count}" "Mrow Mrow Mrow"
  count = count + 1
end while count <= 10
```

This one there is still a counter but you are telling it go ahead and "begin" and execute the loop at least 1 time and then continue to loop if "while" the condition is true.  Unlike the while at the beginning, if the condition is not true, the loop won't execute at all. 

## Upto(x) Loop

```
5.upto(10) do |i|
  puts "#{i} Bork Mrow Bork"
end
```

Unlike the .times loop that we learned in Flatiron this one you can specify WHERE the loops should start, which is really cool. It will start at "5 Bork Mrow Bork" instead of 1 and continue to loop until it reaches 10 and stop.


