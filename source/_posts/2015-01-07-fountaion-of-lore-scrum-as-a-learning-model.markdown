---
layout: post
title: "Fountain of Lore: Scrum as a learning model"
date: 2015-01-07 14:34:59 +0200
comments: false
categories: ["learning", "scrum"]
keywords: "learning, scrum, programming, developer"
description: "Using Scrum as a model for continuous learning" 
---

To be successful in learning, one must have a plan. What do you want to learn and what materials are relevant? How do you order them? Do you study them in parallel or one at a time? How do you keep track of the progress you've made? Should you keep a history of what you've studied? 

<h3>Enter Continuous Learning, the fountain of lore!</h3>

I use Git and <a href="http://www.visualstudio.com/en-us/products/what-is-visual-studio-online-vs">Visual Studio Online</a> to help me throughout the learning process. I choose Git because I use it everyday and I can use it on both Windows and OS X (Unlike TFVC). As you probably know Microsoft provides a free VS Online option that is more than enough for personal use. As a Scrum tool I use VS Online. 

{% imgcap /images/posts/saruman_learning_csharp.png Saruman indexing his ebook collection of fire magic. %}
<!-- more -->


Let's get to the action. I create a project with Scrum model to contain all study materials or subjects. Let's call it "Learning Pro", a learning path for our software development profession. I generally read books so I create a Feature (Epic in Scrum) for every book I own or every online course I'm enrolled in. Feature is a higher level notion that can't be handled or estimated right away without chopping it into smaller parts, so it is a good match for a book or other kinds of learning materials. You can easily check back the materials that you've completed later in Features section.


{% img left /images/posts/features.png %}


Take C# In Depth as an example, a great book by Jon Skeet. There are 16 chapters and so we need to create a Backlog Item for each chapter. A typical chapter can be studied in 1-2 hours so you can divide them easily into Tasks. Before going into Tasks, let me show you the Backlog Items under the Feature C# In Depth.

{% img center /images/posts/features_to_pbi.png %}


Studying a chapter is often not enough to internalize it for me. I like to run an eye over it a day after and do some exercises or write some code about it. There are typically 3 tasks Study, Summary, and Exercise. Studying is studying, nothing unclear about it. I love to write a summary of a chapter the day after and push it to VS Online using Git. Most of the time there are also exercises that involve writing code, they get pushed too.

Now it's time to estimate all tasks and create a Sprint that is a week long. In that sprint determine the Capacity, the amount of hours you can spare that week. Then handle each task in order and try to have them finished in time. Burndown Chart shines again (ignore the fact that I'm behind the schedule this sprint). 

{% img center /images/posts/burndown_chart.png %}

<h3>Collect The Loot</h3>

Using Scrum on cloud provides: 

- You are able to access the materials and save the progress you've made everywhere and easily.
- You can determine a path to follow by using hierarchical structure (Feature-Backlog Item-Task) and by ordering materials.
- You can plan and estimate better by examining your now quantifiable records. You will have a better idea what you will be able to learn in a year for example.
- Motivation is probably the most important gain. Burndown Chart reflects your performance and motivates you if you fall behind.
- Another benefit is keeping a history of your effort. You can come back and see the summaries or the code you've written. 
- Although I've never done before, you can share the output(summaries, notes, code, links etc) of yours with others. Reading your summaries or inspecting the code you've written can be beneficial for your friends or colleagues. 
