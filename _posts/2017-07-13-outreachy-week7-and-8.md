---
layout: post
title: Outreachy With Ceph - Java Test Suite building up
comments: true
---

From my last blog post, the [java suite](https://github.com/nanjekyejoannah/java_s3tests) is already up with more than 100 tests
implemented. Let me get to some details on what has and needs to be implemented.

## What has been implemented

This is a summary of the implemented tests a [commit](https://github.com/nanjekyejoannah/java_s3tests/commits/master) summary would sound 
more elaborate.

+ Tests on Basic object and bucket CRUD.
+ Tests on SSE and KMS.
+ Tests on object put and get with delimeters, prefixes, maxkeys, metadata and markers.
+ Tests on bucket and object put with with the different headers.

## What Next

I will have to ensure I have a CLI environment to run the tests as currently I run them in eclipse. I need to make us of Ant
to automate the test automation. This has been a battle but hoping to nail it down completely soonest.

I will be implementing tests on AWS auth4. I will get advise and feedback on this on especially what should be tested
but will first share my test plan with my mentors.
