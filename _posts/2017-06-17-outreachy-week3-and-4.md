---
layout: post
title: Outreachy With Ceph - Week 3 and 4
comments: true
---


# [Multi Language S3 Testing - Go TestSuite]()

# Major refactors and up to 70 tests written

Every one has a plan until they are punched in the face. I had a plan of implementing many many more tests but these weeks turned out to be about alot of refactoring however I also wrote 50 more tests to add to the 25 tests written in the previous period. Let me get to the details quickly.

## Achievements during this Time

### Refactor

After a review of the tests, I was advised to implement cleaner ways of cleaning up created buckets and ensuring that bucket names bear unique and random names.

This made me switch to testify/suite from testify/assert for handling my test workflow. The earlier gives me features of test teardown and setup that the builtin testing package is not so generous with. This was some hell of work but it made my tests neat and cleaner.

I also introduced separation of concerns in the utility methods and the actual tests am implementing. I moved all utility logic to a different folder a way from the tests. My decision was based on the fact that we need the test methods to just do assertions and not clatter them with logic.

Generally speaking working with the Go AWS SDK has been a journey and I have been learning better ways of doing things time and again and this has made me do alot of refactoring. Even testing with Go has been a journey but am becoming a master every day.

### Tests

I implemented 50 more tests on object operations. I implemented most scenarios on setting and listing objects with delimeters, maxkeys, prefixes and markers.

I opened two issues on the [AWS Go SDK](https://github.com/aws/aws-sdk-go/issues/created_by/nanjekyejoannah) for cases where there were failures in the tests I had written. I noticed that I was able to set a negative maxkey and the sdk would process the request which is odd to me. I also noticed one can create a bucket twice and the SDK had no validation for bucket dupliation for this. which we also discussed it [here](https://github.com/aws/aws-sdk-go/issues/1362).The team generously gave me feedback. 

My code snippet of the week is:

	const charset = "abcdefghijklmnopqrstuvwxyz" +  
	  "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"

	var seededRand *rand.Rand = rand.New(  
	  rand.NewSource(time.Now().UnixNano()))

	func StringWithCharset(length int, charset string) string {  
	  b := make([]byte, length)
	  for i := range b {
	    b[i] = charset[seededRand.Intn(len(charset))]
	  }
	  return string(b)
	}

	func String(length int) string {  
	  return StringWithCharset(length, charset)
	}

	var bucket_counter = 1
	var prefix = viper.GetString("fixtures.bucket_prefix")

	func GetPrefix() string {

	  return prefix
	}

	func GetBucketName() string {

	  prefix := GetPrefix()
	  random := String(6) 
	  num := bucket_counter

	  name := fmt.Sprintf("%s-%s-%d", prefix, random, num)

	  return name
	}

Because these methods saved me alot of code duplication of more than 50 lines of code.

## Community Involvement

I have worked and been mentored by a couple of generous people in the ceph community. 

Special thanks to marcus for the insightful feedback on the project thus far and providing good fixes when we are stuck. He is the hero for RGW connection. His help was very beneficial.

A loud shout out to  [Robin Johnson](https://github.com/robbat2) for opening [issue](https://github.com/nanjekyejoannah/go_s3tests/issues/1) and for giving me a long and clear detail on how I should solve it.

And salute to [Ali Maredia](https://github.com/alimaredia), my mentor for patiently answering all dumb questions in a basic and clear way when am super lost. The Docs that he prepares for me are very detailed and helpful. I think I have the best mentor!!

## Tasks for the Next Period

### Tests

1. Implement tests on;

+ SSE
+ Bucket Lifecycles
+ Multipart Uploads and
+ host style

2. I will also prepare an update to the ceph-devel mailing list on the project.

3. I will also work on wrap up for the Go test-suite and will keep resolving issues that shall be opened as I continue working on other suites till end of the internship. The next suite will be the Java Suite.

4. We are also going to discuss teuthology integration for the Go test suite

## Interested in more Details??

Check out the [Project Tracker](https://github.com/nanjekyejoannah/Outreachy-RGW-testing) for more details on this project.

