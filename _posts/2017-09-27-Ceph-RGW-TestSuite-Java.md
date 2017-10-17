---
layout: post
title: Ceph - RGW Java TestSuite
comments: true
---

This blog documents the Java suite that I worked on during my outreachy internship with Ceph for anyone interested in building on to the work.

The test suite tests Ceph's Rados Gate Way S3 interface.

## Stack

The tests are written in Java programming language and make use of the AWS Java SDK to perform the s3 operations.

The TestNG test framework is used for implementing the tests and gradle to automate running of the tests to suite CLI environments.

The test configuration data is kept in the  properties file.

## Implemented Tests

About 150 tests are currently implemented in this suite. I will share the details on the specifics.

### Bucket Operations

Most of the bucket operations like Create, update, read and delete for most scenarios are tested with all possible headers:

+ General CRUD of buckets.        
+ Bucket Lifecycle configuration       
+ Bucket Creation with all possible headers.

### Object operations

Most of the cases for object operations were tested including;

+ General Create, Read, Update, Delete scenarios     
+ Writing/Reading objects with all possible headers.   
+ Getting and setting metadata.   
+ Getting objects with delimiters, maxkeys, prefix, markers 
+ Reading and writing objects with server side encryption (SSE) and SSEKMSKeyId.    + Reading andwriting objects with SSECustomerAlgorithm, SSECustomerKey and SSECustomerKeyMD5.
+ Multipart uploads and transfer.

### AWS4

RGW has shown some inconsistencies when performing AWS4 operations before so tests are implemented for these unique cases and include:

+ Multipart Uploads of varying sizes from small to big files for both LLAPI and HLAPI.
+ Multipart Copy of varying sizes from small to big files for both LLAPI and HLAPI.
+ File and directory uploads of small to big files for both LLAPI and HLAPI.
+ Object Read and Create with all possible headers for both LLAPI and HLAPI.


## What is Pending

There are still more scenarios that arent yet tested some specific to the AWS GO SDK but some are critical cases especially experienced on RGW. The oustanding tests pending are:

+ Host style as elaborate in this [issue](https://github.com/nanjekyejoannah/go_s3tests/issues).
+ Versioning
+ Multipart Uploads/Copy/Transfer with SSE and KMS

## Possible Changes

I will make a couple of refactors to make style guide consistencies and remove obvious duplication of methods and other clean ups. I willl also add docmentation that I had overlooked.

The branch shall be merged to master after we have done rigorous testing with [Ali Maredia](https://github.com/alimaredia) the mentor of the project.

I am also revisiting testing utility methods on second thought.

## Going forth

I will keep commiting to this project may not be daily because I have to concetrate on school now . I will keep in touch with the mentors Ali Maredia and Marcus Watts on any changes I will have made or need to make.
