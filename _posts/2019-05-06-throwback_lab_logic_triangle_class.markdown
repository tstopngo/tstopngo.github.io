---
layout: post
title:      "Throwback Lab Logic:  Triangle Class"
date:       2019-05-06 17:20:40 +0000
permalink:  throwback_lab_logic_triangle_class
---


A cohort mate pinged me about this lab and we walked through the logic of this particular lab together. The lab request you to return the correct type of triangle or an error message depending on the the numbers that the class is instantiated with. 

For example `triangle = Triangle.new(4,4,4)` would create a instance of a triangle with those numbers stored as instance variables. Next, if we did `triangle.kind` it return that the triangle is an equilateral triangle. The goal of this lab was to identify isoceles, equilateral, and scalene. Additionally, there are some other test that we need to ensure to make the test pass.

Let's start with the first test, we need to make sure that if someone instantiates triangle = Triangle.new(0,0,0) we should get an error message.

`def kind 
   if @num1 == 0 && @num2 == 0 && @num3 == 0 
	 raise TriangleError 
end`

Here we are checking that num1, num2, num3, which is 0,0,0 will simply give us an error message.

Next, test to check is that if the we give a side a negative number this is not allowed and we should also throw an error message here as well, so we will need to another line of logic using elsif knowing that we have a few more test. If this was our last test then we could end it with else.

`def kind 
   if @num1 == 0 && @num2 == 0 && @num3 == 0 
	 raise TriangleError 
	 
	 elsif @num1.abs != @num1 || @num2.abs != @num2 || @num3.abs != @num3
        raise TriangleError 
end`

The .abs will take the absolute value the number and check that it is not equal to the original number, which could be negative, so this means that the absolute value is not equal to the original number and we should send an error to our terminal.


The third error we need check for is to ensure that we a following the "Triangle Inequality rule, which simply states that the length of one side of the triangle cannot be less than the sum of the other two sides of the triangle. Thus we create our next elsif statement to add this logic to our #kind method.

`def kind 
   if @num1 == 0 && @num2 == 0 && @num3 == 0 
	 raise TriangleError 
	 
	 elsif @num1.abs != @num1 || @num2.abs != @num2 || @num3.abs != @num3
        raise TriangleError 
		
		elsif (@num1 + @num2) <= @num3 || (@num2 + @num3) <= @num1 || (@num1 + @num3) <= @num2
        raise TriangleError

end`

In the next line we are checking if any comboination of two sides which we add together is less than the remaining side then we are going to raise an error message. At this point the kind method now accounts for all of the potential errors that we need to address in the tests, so now we can move on to the next three test which is to create the logic to return the type of triangle based on the numbers provided to the instance.

Let's start with the scalene triangle, the definition of a scalene triangle is that no two sides are equal.

`def kind 
   if @num1 == 0 && @num2 == 0 && @num3 == 0 
	 raise TriangleError 
	 
	 elsif @num1.abs != @num1 || @num2.abs != @num2 || @num3.abs != @num3
        raise TriangleError 
		
		elsif (@num1 + @num2) <= @num3 || (@num2 + @num3) <= @num1 || (@num1 + @num3) <= @num2
        raise TriangleError
  
	elsif @num1 != @num2 && @num2 != @num3 && @num1 != @num3
       return :scalene

end`

The next line of logic that you see is that none of the numbers are equal no matter which numbers are compared. We can also see that we are using && between each of the checks because this must be true for all the sides.

Next, we need to check if the triangle is equilateral, which simply means all sides are equal to one another. 

`def kind 
   if @num1 == 0 && @num2 == 0 && @num3 == 0 
	 raise TriangleError 
	 
	 elsif @num1.abs != @num1 || @num2.abs != @num2 || @num3.abs != @num3
        raise TriangleError 
		
		elsif (@num1 + @num2) <= @num3 || (@num2 + @num3) <= @num1 || (@num1 + @num3) <= @num2
        raise TriangleError
  
	elsif @num1 != @num2 && @num2 != @num3 && @num1 != @num3
       return :scalene
			 
	elsif @num1 == @num2 && @num2 == @num3 && @num1 == @num3
       return :equilateral

end`


Similar to the scalene, we are using the same concept where we compare all the sides except this time we just need to make sure that all sides are equal to return equilateral.

Finally since our last test is to check of it is isoceles, we could write out the logic for it, but since we know if none of the above are true then we can write else

`def kind 
   if @num1 == 0 && @num2 == 0 && @num3 == 0 
	 raise TriangleError 
	 
	 elsif @num1.abs != @num1 || @num2.abs != @num2 || @num3.abs != @num3
        raise TriangleError 
		
		elsif (@num1 + @num2) <= @num3 || (@num2 + @num3) <= @num1 || (@num1 + @num3) <= @num2
        raise TriangleError
  
	elsif @num1 != @num2 && @num2 != @num3 && @num1 != @num3
       return :scalene
			 
	elsif @num1 == @num2 && @num2 == @num3 && @num1 == @num3
       return :equilateral
		else
        return :isosceles 
      end
end`

There you have it! The logic for the triangle lab was one of the most complex part of the lab, whereas setting up the class and having a class within it to inherit the Standard rule class was much easier than getting the test to pass for the errors.











