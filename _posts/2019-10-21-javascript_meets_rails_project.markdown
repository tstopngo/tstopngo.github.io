---
layout: post
title:      "Javascript Meets Rails Project"
date:       2019-10-22 01:48:06 +0000
permalink:  javascript_meets_rails_project
---


This is the next installment of the portfolio projects at FlatIron. For this project I took my pre-existing Rails project and added on a layer of of Javascript to make the application more Dyanmic. 


There were two features that found in my project that made for a good use case to implment Javascript and meet the requirements of the project. The first feature was to allow users who visit the index of workout logs by all users to be able to see the log details without being redirected to the log. The second feature was to load all the logs for a specific user on their profile page using ajax so the user could view all their own logs. Additionally I loaded in a partial form so a user could submit a new log and it would appear on the same page without directing them to the new log.


In order to complete these two features it actually required a bit of set up. First I installed the active_model_serializer gems. This allowed me to create serializers for my models and in the controller have a json or html render depending on the request made to the endpoint.

After I added in my serializers I started to write up some JS where I wanted the functionality. For the first feature I first created elements where the log details would go so when I made a get request to the endpoint for the specific Log it would display in that element. Following that I wrote Javascript add a feature to make the get request and append the page with the following:

```
  $(function(){
    $(".js-show").on("click", function(event){
      event.preventDefault();
      var logID = $(this).data("id")
      $.get(`/logs/${logID}.json`, function(data){
        var log = data

        var descriptionText =
        '<p>'+ 'Calories: ' + log["calories"] +'</p>' +
        '<p>'+ 'Workout Time: ' + log["workout_time"] +'</p>';
        $("#log-" + logID + "-details").html(descriptionText);
          workoutList= "";
          var workouts = log["workouts"]
          workouts.forEach(function(workout){
            workoutList += '<p>'+ 'Workout: ' + workout.name +'</p>';
          });
          $("#log-"+logID+"-workouts").html(workoutList)
      });
    });
  });
```
	

The feature was under the views of the user where they could see all their logs and create a new log. This was going to be much tougher. Rendering the view of each of the logs was simialr to the code above for the index, but creating a new log from the same view was the hard part. First I had to write function that would disable the New Log button from routing to the page for new logs and render a partial instead. Then have another function wait for the user to submit to serialize then pass the response to a constructor function that I made for new Logs: 

```
$(".newLog").on("click", function(event){
      event.preventDefault();
      $('#form').append("<h2>Add New Log<h2>")
      $('#form').append("<%= escape_javascript render(:partial => 'logs/form',
      :locals => { :l => @log }) %>");

      $("#new_log").on("submit", function(e){
        e.preventDefault();
        $.ajax({
          type: "POST",
          url: this.action,
          data: $(this).serialize(),
          success: function(response){
            let log = new Log(response)
            let html = log.renderLi()
            $("#form").html(html);
          }
        });
      });
    });
```

One thing that I had to do was nest the function under for submitting a new log underneath the when the partial was render because the new_log element did not exists on the page until the first event ocurred and it caused a few bugs where my entire page would not render.


The last problem I had when working on the project was once I got this up and running. When I hit create log it would hang on the page. Then when I refreshed it would appear which meant my post action was working but my success never hit. I found that I was missing one spectacular line of code in my controller under the create

```
render json: @log, status: 201 
```

I had forgotten about this which was required because when the post is succesfful the was no repsonse for it to render the post to the page. By adding this response I got the data that was serialized in a JSON format to use and render it on the same page. This took a few hours of debugging and all I was missing was this code. 

This project helped me have a better grasp on AJAX and adding Javascript alongside with Ruby code. While I wouldn't say I am confidenent with this I definitely feel like I have a better handle with Javascript and these concepts from the project and learned a lot along the way.

