---
layout: post
title: Test driven approach to build MVP
date: 2014-01-12 23:15:00.000000000 -08:00
categories:
- MVP
- software design
- TDD
tags: []
status: publish
type: post
published: true

---
I have talked a little bit about [Test Driven Development ](http://c2.com/cgi/wiki?TestDrivenDevelopment)in [my earlier post](http://hakimhanif.com/2013/04/tdd-is-not-all-about-writing-tests-first) though it was more towards while working on a component level. But I have been thinking about how can we apply the same approach on a bigger scale, how about while defining how to add features and build a good enough product.

Let me give you some context first before diving deep into this.  I got an opportunity recently to work on a very interesting project within AWS called [Amazon WorkSpaces](http://aws.amazon.com/workspaces/), which is Amazon way of doing Desktop As a Service. I won't go into details of how awesome this project is (though you should definitely try it out to see some of the awesomeness), but I will focus on the approach that we took to deliver the most critical piece of the project in a couple of months.

As usual the timelines are tight as well the [competition](https://www.google.com/search?q=aws+workspaces+competition&ie=utf-8&oe=utf-8&aq=t&rls=org.mozilla:en-US:official&client=firefox-a&channel=fflb), but we still have to deliver a good product or what we call the [Minimum Viable Product](http://practicetrumpstheory.com/minimum-viable-product/) (yeah, we run lean at AWS). Anyways, I was set to work on the piece that act as a gateway for handling the streaming of workspace (the windows EC2 machine) to [the WorkSpaces client](https://itunes.apple.com/us/app/amazon-workspaces/id727778113?mt=8). This part below is my learning while working on this project.

Now when you think about working on a project, there are various ways to approach it; once you are done with initial design and have a good idea of how it should work overall as a system. 

__Approach A__ is to have a detailed (implementation) design document with all the details about APIs, their structure, how will they fit into the entire system and you then hand it over to your engineers and say: go built it guys! Make sure you follow this document as we have spent good three weeks writing it. And as usual, things change, requirements change and no one ever care to take a look at what is written in that document. The system is built, integration tests are added (when? depends on the design document) but then we realize that things are little different that what we though while writing the document. Believe me, one of my previous team followed the above pattern and as obvious, we were late delivering that project.

Okay, so that is one extreme. 

__Approach B__ is, jump into the implementation assuming we are agile and change as we go, come up with an implementation, do some form of testing and come up with an end to end approach quickly, see it all work with some manual testing. And then we say, lets not worried about the end to end tests or what they call "integration tests" for now, we will add them later but lets add more functionality based on our learning and 'TODO' list from our last progress. The project progresses that way, and then we think about adding all our integration tests, load tests and making the system 'ready for operations'. But then its time to launch and we are sweating as we are done with our functionality but may be we are not ready for the prime time. Why? Well, we have the MVP product in terms of functionality but may be we are not sure if its good enough.

Now coming to the __Approach C__, the __TDD__ approach at a project level, while building a MVP, why not first write your tests (most importantly your integration tests) first that defines the scope of your product. I know you might think of this as an extreme case of TDD (write the tests first, meh!), but I mean why not think these tests are your technical definition of MVP and as building blocks of your MVP.
Lets pause for a moment, and look back at what a MVP definition is. This [blog from Ash Maurya](http://practicetrumpstheory.com/2009/10/how-i-built-my-minimum-viable-product/) says "The basic idea is to maximize validated learning for the least amount of effort".  And then he adds a great example:

_For Timothy Ferris, his MVP for testing new products that don’t yet exist (micro-testing) comprises of a landing page, signup page, and Google Adwords to drive traffic. However, this approach presupposes that:_

* _You can create a good landing page_
* _You can write good adwords copy_
* _Adwords is a viable distribution channel for your product_

Now if I understand correctly, it means build a small set of features but these should be "good enough" to maximize your learning from customer feedback. Hmm, interesting! Specially the "good enough" part.
So, how to define something as "good enough"? And most importantly, how to validate that you maintain that "good enough" trait as you go on adding features to build your MVP? And when you feel you are done with your MVP, you have maintained and made a "good enough" product to launch in public.
I think this is where Test driven approach is so valuable. Using TDD, this is how one should go about developing these good enough features:

1. Write a failing test (start with unit tests and then add integration tests) that defines the features you want in your MVP.
2. Implement the feature without caring much about good refactored code. Just make it work and such that the tests are green.
3. Integrate other components using that feature and make it work end to end.
4. Then refactor the code and make it production ready. The tests are still green.

Add a small good enough feature, but validate with tests (unit tests at small component level, and integration tests for end-to-end feature) and mark it as "good enough" before proceeding towards a new one. Keep the bar as "A feature is marked done, only if its good enough to ship to your customers". By working this way, you maintain that confidence all the time in your product, that if your tests are green for a feature its good to go. Its also setting up an awesome, solid operations platform to make sure that any new changes or features added to the system is not breaking your previous release of your MVP.

It all sounds simple and obvious, right? And you might think: "So is that the approach that your team is taking right now?" The answer is "No, not exactly". But we are close, at least we are not taking the Approach A but unfortunately we didn't follow a TDD approach either. We do have a good setup of tests that validates our entire system every minute though were setup a little late in the project but we now understand the importance of these tests. Seeing a green light every minute is the best motivation you can ever get.

I tried some form of TDD approach while working on the WorkSpaces project, but I think I failed to make sure that we had tests (specially integration tests) for every feature we added. But I am still working on it, and there is still a long way to go so I will get another chance to make sure I do it the 'good enough' way!