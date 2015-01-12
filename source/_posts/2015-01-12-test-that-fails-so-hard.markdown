---
layout: post
title: "Test That Fails So Hard"
date: 2015-01-12 23:40:07 +0200
comments: false
categories: testing 
keywords: unit, testing, stack overflow, exception, fatal 
description: Stack overflow exception can kill test environment.
---

I've added a few unit tests today and all the tests stopped running. There was no feedback about the problem, the tests just wouldn't run. I've got suspicious first about VS 2015 and then NUnit test adapters because VS 2015 is in Preview stage and test adapters use Visual Studio SDK(which in turn may not be mature enough). Then I tried running tests using NUnit GUI runner app, no luck, it too got stuck.

It was time to debug the test, and as soon as the debugger entered a property in one of my new classes, I realized that there was a circular call which resulted in running out of stack memory and StackOverflowException was being thrown. 

Of course this is a fatal exception that can't be handled by an app easily (maybe impossible?). So there was no information from the IDE that something was causing infinite loop of method calls. The next time same thing happens, I would suspect my own code instead of Visual Studio even if it is a "Preview" version.
