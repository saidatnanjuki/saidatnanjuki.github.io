---
layout: post
title: Outreachy With Ceph - The last Mile
comments: true
---

This is the last week of outreachy :( and well I am doing the last mile which as my mentor says has the most work.I will give a few updates on what has transpired from week 8 given that that is when I last gave any updates.

## AWS4 Tests

I was told by the mentors of the project to priotize testing AWS4 because there were a couple of reported bugs especially on multipart uploads. I implemented about 50 tests testing objects creation with all possible headers and all possible multipart upload scenarios using both High level API and low level API for the Java SDK.

## Finished Java Suite

Well I have put a stop to adding more tests to the java suite for now and ensuring the existing ones are running perfectly well. I have implemented about 150 tests in this suite. 

I got feedback where my the ceph RGW developers had errors running these tests which I have rectified now and we will review today at a confortable time in their time zone.

#### How I solved Challlenges on this suite

Well most of the challenges in exectuting these tests stemed from the teardown method which I was oiginally calling after every method. This caused the ceph logs to over build up and complain of insufficient memory. When I decided to run the tear down after every class, this was solved. This also solved problems where some tests required to be broken down to another separate class to run well. The Go suite works well with teardown method being called after every test method though.

## Refactoring

Well this took most of the time. I did alot of refactoring for both the Go suite and Java suite. The refactors 
affected mostly tests regarding Server Side encryption and a couple of documentation for the tests.

#### Server Side encryption

To run any tests regarding SSE using the java and Go SDKs, you have to be using a secure endpoint (https) however there  may be times when one tries to run them in a non secure environment. I originally would skip these test methods which is a good idea but after thinking through I decided to catch the errors regarding the need for a secure endpoint because it is also important to  assert what happens when using http instead of https.

#### Documentation

To self document the tests in the Java suite, I used the **description** parameter available in the @Test annotation in TestNG with a brief description the goal of each test.

#### Renaming method names and classes

Well I also did some renaming of stuff but still did not do much work in ensuring very short names because I did 
not want to compromise on readability. You know this is hrdest thing in computer science but I tried.

## Still in the brewery

I am now writing tests for all the utility methods that the tests depend on because I noticed that there were cases where there were errors in the utility methods and the tests would fail in which case my head thought it was RGW failing.

To put things straight, all tests for utility methods shall be implemented before end of tommorrow.

## What Next

I will write two more blogs documenting each tests suite. Keep a good eye for these before end of week.
