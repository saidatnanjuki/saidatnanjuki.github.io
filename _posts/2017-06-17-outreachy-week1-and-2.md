---
layout: post
title: Outreachy With Ceph - Week 1 and 2
comments: true
---

# Multi Language S3 Testing - Go TestSuite

## About the Project

The project aims at implementing a set of tests to test RGW's S3 interface. RGW features an AWS s3 like interface against which tests are to be run.  Currently there exists a python suite of tests implemented [here](https://github.com/ceph/s3-tests).This test suite uses an SDK from Amazon called Boto, and has 400 some tests in it. The goal for this project is to have other test suites, in other languages specifically (c++ , java and Go), that all test the same subset of the 400 python tests. 

The major deliverables of this project is to implement three test suites in :

+ Golang
+ Java and 
+ C++

If time allows, Then the tests shall also be connected to the Ceph Integration framework called Teuthology.



## Project Execution

I have set up a [project Tracker](https://github.com/nanjekyejoannah/Outreachy-RGW-testing) and [trello board](https://trello.com/b/etwTtnv4/outreachy-rgw-testing) for different people to track progress on the project. The goal is ensure the [Time line](https://docs.google.com/document/d/186YHbdIGi1Ja2X6t24vIufU3pLyBVhKzhskY6Ax_0x4/edit) is followed in order to meet the deliverables. The tracker has a summary of my daily tasks in the [daily log](https://github.com/nanjekyejoannah/Outreachy-RGW-testing/blob/master/Daily%20Logs/logfile.md) and summary of the weekly tasks in the [Week logs](https://github.com/nanjekyejoannah/Outreachy-RGW-testing/tree/master/Coding).

## Project repositories

I started working on the Golang test suite and the source code lives here:

[go_s3tests](https://github.com/nanjekyejoannah/go_s3tests)

## Achievements during this Time

### Set Up

Getting my environment to work conviniently took abit of time. At first I has running the rados gate way on my laptop in a virtual machine and connecting my tests to it. I then realised after a few times, my machine would just hang. I therefore asked my mentor if I could instead setup [Ceph](https://github.com/ceph/ceph) on another machine and connect the tests on my laptop to the rados gate way on another host.

This worked fine with guidance from my mentors.

### Connected Golang test Suite to RGW

After setting up, I developed a skeleton of the project and before I could write any tests I had to do some hackery to connect to RGW(rados gate way ). Fortunately my mentor had a working Go client that connects to RGW (rados gate way )which I gladly reverse engineered to meet the project needs and was able to hook my tests to RGW(rados gate way).

### Written 25 running tests so far

After connecting to RGW for the s3 interface, I started working on the tests. My mentor asked me to implement eight tests annotated with explanations in comments to see if I understand their goal. I did this and got feedback on the same. 

After this task, I was then started implementing the tests on bucket and object operations. I have written 25 tests to date and still getting feedback as I write more tests.

The feedback was about:

+ Ensuring that my codefiles end with newline.
+ Ensuring that my config is consumable by teuthology.
+ Ensuring that the instructions for running the tests actually work.

## Blockers

I do not have blockers on my end however I am facing a challenge where my mentor is not able to run the tests in his environment. We will have a chat this coming week to rectify this when he gives more detail.

## What I have learned

### Amazon Web Services

The major capacity building high light in these first two weeks has been being able to use the AWS Go SDK to perform s3 object storage operations. I have written logic for most operations during implemetation of the test suite. The community supporting this SDk is good and this even makes life simple. I faced one major challenge adding AWS if-none-match headers on UploadInput which had not be implemented but there was a work around for that.

### Working with Go Configuration

I have also learned alot about handling configs with Go. I got to know how to use [viper](https://github.com/spf13/viper) for loading config data. it features simple ways of reading the data as we use the dot notation without need for writing extra structs. Also the fact that it supports all config types really stood out for me as the config type is not tied to the implementation. Therefore a user can decide to use any config type of choice.

I decided to use .toml config. Implementing this was this simple:

config.toml

	[DEFAULT]

	host = "s3.amazonaws.com"
	port = "8080"
	is_secure = "yes"

	[fixtures]

	bucket_prefix = "jnans"

	[s3main]

	access_key = "0555b35654ad1656d804"
	access_secret = "h7GhxuBLTrlhVUyxSPUKUV8r/2EI4ngqJxD7iBdBYLhwluN30JaT3Q=="
	bucket = "bucket1"
	region = "mexico"
	endpoint = "http://localhost:8000/"
	display_name = ""
	email = "someone@gmail.com"

Loading the configuration

	func LoadConfig() error {

		viper.SetConfigName("config")  
	  	viper.AddConfigPath("../")

	  	err := viper.ReadInConfig() 
	  	if err != nil {
	    	fmt.Println("Config file not found...")
	  	}

	  	return err
	}

	var err = LoadConfig()

	var creds = credentials.NewStaticCredentials(viper.GetString("s3main.access_key"), viper.GetString("s3main.access_secret"), "")

	var cfg = aws.NewConfig().WithRegion(viper.GetString("s3main.region")).
		WithEndpoint(viper.GetString("s3main.endpoint")).
		WithDisableSSL(true).
		WithLogLevel(3).
		WithS3ForcePathStyle(true).
		WithCredentials(creds)

### Golang

I have been writing Golang since september 2016 but still confess I am learning new ways of doing things in the language. There have been a few ramblings for the abscence of features I valued so much in other languages like default parameters but I have found a way around. However I feel this is on my wish list for the language.

## Tasks for the Next Period.

### Work on Open issues

There is one [issue](https://github.com/nanjekyejoannah/go_s3tests/issues/1) opened on the project so far and I will discuss with the author this week so that I can close it.

### Ensure I have 60% test implementation

The next two weeks will be focused on ensuring a good number of tests implemented in the python test suite is impelemented according to plan before July.

### Integrating to teuthology

I will also work on integrating the test suite to teuthology before I move on to the next test suite.
