---
layout: post
title:      "Rails Project: Fitness Story V2"
date:       2019-08-25 23:54:19 +0000
permalink:  rails_project_fitness_story_v2
---


For the Rails project I decided to iterate over my previous application that was done in Sinatra and recreate it in Rails framework. The scrapped some of the features and had different features here where the user should be able to put in an amount for the workout as opposed to just one. 

This was a long journey, while the foundation of getting the views up and running was easy, the tough part was has many, through relationships with the join table. I had so much trouble writing the amount to the join table which was the unique amount that was tied between a log and workout. I spent probably 4-5 days total with a lot of debuggging sessions with tech coach to figure this out. I thought that since this was such a significant part of my application I thought this topic would be a great fit.

Before we get started this is how my models were set up for my application:

The Log

```
class Log < ApplicationRecord
  belongs_to :user

  has_many :log_workouts, dependent: :destroy
  has_many :workouts, through: :log_workouts
end
```

The Workouts

```
class Workout < ApplicationRecord
  has_many :log_workouts, dependent: :destroy
  has_many :logs, through: :log_workouts

  validates :workout_type, inclusion: {in: %w(Aerobic Strength Balance Flexibility)}
  validates :name, uniqueness: true
end
```


Log_Workouts (Join Table) 

```
class LogWorkout < ApplicationRecord
  belongs_to :log
  belongs_to :workout
end
```

This table is where amount would be written to when the user created a new log and added a workout to it where I had the most trouble.



## Challenge 1- The Model & View:

I looked up so many examples from labs but nothing that would actually help me since many of the examples were for different cases because lab examples examples would essentially write a few lines in the view for a hidden field for the other two models on the show page.  For me this was not the case, I was creating a new object, and under that new object creating or re-using workout objects and those workout those the id of these two upon being creating needed to be written to my join table along with an additional attribute.

I knew that the form would have to accept the nested attribute for the workout since we are adding the workout. Then the workout would have to accept an attribute for the amount under it. I had two nested attributes under each. So working on the view I came up with the follwing code under the new log form:

```
<%=f.label "Add your Workout"%>
  <%=f.fields_for :workouts do |workout_fields| %>
    <%=workout_fields.label :name%><br>
    <%=workout_fields.text_field :name%><br>
    <%-workout_fields.label :workout_type%><br>
    <%=workout_fields.select :workout_type, ['Aerobic', 'Strength', 'Flexibility', 'Balance']%><br>
    <br>
    <%=workout_fields.fields_for :log_workouts do |lwf| %>
        <%=lwf.label :amount %><br>
        <%=lwf.number_field :amount%><br>
        <%end%>
```

In my model I also needed to update the Log and Workout Models to include since the Log needed to accept attributes for Workout and under workout you'll notice that Workout accpets attributes for log_workouts where the amount is written:

```
class Log < ApplicationRecord
#previous code above

accepts_nested _attributes_for :workouts
end
```

```
class Workout < ApplicationRecord
#previous code above

accepts_nested _attributes_for :log_workotus
end
```


## Challenge 2: The Controller

After setting up my form correctly I needed to set up my controller correctly to accept the nested attributes from the form. I noticed I kept gettnig an error that my fields were not permitted so I needed to fix this. I updated my params to accept nested attributes. After some research on StackOverflow I realized that it needed to be nested as well and ensure that they were nested properly like they were on the form.

```
def log_params
      params.require(:log).permit(:workout_time,
                                  :calories,
                                  :user_id,
                                  workouts_attributes: [:id, :name, :workout_type,
                                  log_workouts_attributes: [:id, :amount]])
    end
```


## Challenge 3: Back to the Model

After I set up my Controller and View I did some testing and submitted my form, but the issue here was that it was never writing my workout Id and amount to the database. It was just always...empty. I tried unesting it as spearating them and many variations, but it all came down to creating a custom writer method under the Log model. You can see my notes below in the # to see line by line what is happening. 


```
#when creating a new workout from form check to see if it is db first
		def workouts_attributes=(workouts_attributes)
		
      workouts_attributes.values.each do |workout_attribute
      #workous_attributes gives you the values of the hash, which has an array of "workout objects"
			
        workout= Workout.find_or_create_by(name: workout_attribute[:name], workout_type: workout_attribute[:workout_type])
        #find the workout object from the pipes or create a new one with the arguments
				
        self.workouts << workout unless self.workouts.include?(workout)
        #add the workout object to the proxy collection unless it has it already
				
        workout_attribute[:log_workouts_attributes].values.each do |log_workout_attribute|
        #key into the nested information workout attribute and grab the log_workout attributes, which includes amount, wokrout_id, and log_id
        
				if self.log_workouts.any? do |log_workout|
          #check if logs have any log_workouts if true then pass each log_workout through pipes
					
            log_workout.log_id == self.id && log_workout.workout_id == workout.id
            #set the the ids of the log and workout to the log_workout 
          end
          log_workout = self.log_workouts.select do |i|
					#select the log_workout from logs
            i.workout_id == workout.id && i.log_id == self.id
						#select the log_workout from the log_wokrouts where the the Workout ID and Log Id match
          end.first
					
          log_workout.amount = log_workout_attribute[:amount] unless log_workout_attribute.blank?
					#writet the amount to the Join Table
          log_workout.save
					
					
        else
          log_workout = self.log_workouts.select {|i| i.workout_id == workout.id}.first
          log_workout.amount = log_workout_attribute unless log_workout_attribute.blank?
					#if there are no log workouts then then select the workout id that matches and write the amount
          log_workout.save
        end
      end
      end
    end

```

## Conclusion

As you can see this ended up being more complex than it seemed, but I learned a lot about how all the ids and additional attributes get written to to a join table and how the relationships between join models work. I spent 4-5 days and I'll be honest I still feel rattled by it. Definitely takes some time to read up on the Rails guide on the relationship and running experiements in your application. Don't be discouraged. Ask for help when you need it to help step through your application. Use Pry to see what is happening and tweak it along the way.

Onwards to Javascript!




