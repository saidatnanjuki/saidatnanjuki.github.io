---
layout: post
title: Ceph - RGW GO TestSuite
comments: true
---

This blog documents the Go suite that I worked on during my outreachy internship with Ceph for anyone interested in building on to the work.

The test suite tests Ceph's Rados Gate Way S3 interface.

## Stack

The tests are written in Go programming language and make use of the AWS Go SDK to perform the s3 operations.

We use the builtin go testing package for the tests but we also make use of testify for assertions and creating suites.

The test configuration data is kept in a toml file and viper used to load and read the configuration data. Viper is used due to its flexibility in the configuration types used. We load the configuration data by reading the config file by name without its extension. This accomodates any configuration type i.e yaml , toml etc. Other than this, viper avails us a less complex way using the dot notation rather than using structs when reading config data.

## Implemented Tests

About 150 tests are currently implemented in this suite. I will share the details on the specifics.

### Bucket Operations

Most of the bucket operations for most scenarios are tested and include:

+ General CRUD of buckets.        
+ Bucket ACL
+ Bucket Lifecycle configuration       
+ Bucket Creation with all possible headers    


### Object operations

Most of the cases for object operations were tested including;

+ General Create, Read, Update, Delete scenarios     
+ Writing/Reading objects with all possible headers.   
+ Getting and setting metadata.   
+ Getting objects with delimiters, maxkeys, prefix, markers 
+ Reading and writing objects with server side encryption (SSE) and SSEKMSKeyId.    + Reading andwriting objects with SSECustomerAlgorithm, SSECustomerKey and SSECustomerKeyMD5.
+ Multipart uploads and transfer.

## What is Pending

There are still more scenarios that arent yet tested some specific to the AWS GO SDK but some are critical cases especially experienced on RGW. The oustanding tests pending are:

+ Host style as elaborate in this [issue](https://github.com/nanjekyejoannah/go_s3tests/issues).
+ Versioning
+ Multipart Uploads with SSE and KMS
+ AWS4

## Possible Changes

I have been working on and intend to push commits on a new branch for now. The branch shall contain mainly refactors and change in dependency management.

The refactors shall affect mostly some utility methods to use  interfaces and reduce some duplication of methods and other clean ups. I will also make foldering changes adding a few more documentation files.

To manage dependecies, I will change to using **dep**.

I am also revisiting testing utility methods though I had flagged this off earlier as not making sense but later noticed tests need to depend on reliable utility methods.

The branch shall be merged to master after we have done rigorous testing with [Ali Maredia](https://github.com/alimaredia) the mentor of the project.

## Conclusion

I will keep commiting to this project though it may not be daily because I have to concetrate on school now . I will keep in touch with the mentors Ali Maredia and Marcus Watts on any changes I will have made or need to make.
