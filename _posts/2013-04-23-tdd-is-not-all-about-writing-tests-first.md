---
layout: post
title: TDD is not all about writing tests first
date: 2013-04-23 06:33:00.000000000 -07:00
categories:
- software design
- TDD
tags: []
status: publish
type: post
published: true

---
[TDD](http://c2.com/cgi/wiki?TestDrivenDevelopment)'s mantra:

![TDD](http://www.zeroplayer.com/tdd.png)

In words:

* Add a failing test
* Write code to pass the test
* Refactor

If you want to get a firm grip on this awesome methodology, read [this book](http://www.amazon.com/Test-Driven-Development-Kent-Beck/dp/0321146530) by **Kent Beck**.
s
However, TDD is not just about writing your tests first or to increase your code's test coverage. These are just the add-ons that you get for free when you use TDD. The mantra behind using TDD is to improve your design, to think from a consumer point of view who is going to use your components or APIs. These consumers can be anyone, it could be you, your team mates, other teams or general public.

Then, you may ask how can writing tests first allows you to better design your interfaces? Good question. Lets think about it in this way. Why we write software? One possible answer is to create some applications that does few useful things that wouldn't have been possible or too tedious to do manually. Its creates something with some intent that someone can use it. So two things that pop out: intent and use. I think that TDD allows you to get these two things right, the intent and use, while creating software. Again you may ask, still how writing a test helps you to get these two things right? Good question again.

When you are writing a test even without the code itself, the most important thing that comes to your mind is how am I going to use this component in my system or application. This makes you think about the interfaces, the parameters, the exceptions you want this method to throw. And there you design your API.

And then the other most important thing you think about what is the intent or the purpose of the code that you are about to write. What you want this piece of code to do? That is what makes you to write your assert statements.

Yes, it could be very difficult to digest this test-first approach initially if you haven't been practicing such methodology but once you do you will see the results and it value. You will be amazed to see how easy it becomes to design your components if they are easy to test.
I have been using TDD for more than a year now and I can definitely see the difference in the way I think and develop software. Its weird but TDD makes you to not to hate writing unit tests since they are the not burdensome-after-thoughts anymore.

Then, there are so many other good things that come for free when you write your tests first. It makes you confident about refactoring existing code. I am currently working on a system at Amazon that serves million of customers and allow them to play with their apps with almost zero downtime. How can you imagine refactoring such a service where a simple mistake can either lead to doing something unintended that breaks millions' of users Appstore experience or can breaks a functionality (or Appstore client) in its entirety? We want our tests to fail first in such cases. 

Then there is code coverage. You won't believe the results of running a code coverage tool on a codebase that is written using TDD approach. It does not give you a single opportunity to make the coverage better by looking at the results and then 'hack' the tests to increase the coverage since you already get an amazing high code coverage for free!

Give it a try, its worth it.