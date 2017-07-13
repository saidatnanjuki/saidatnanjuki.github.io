---
layout: post
title: Outreachy With Ceph - Go TestSuite up for feedback, On to Java Suite
comments: true
---

I have implemented a good number of tests about 150 and planning on Sending a status email to the ceph community for 
an update but most importantly feedback. I will quickly move to implementing the next  test suite in the coming weeks. 
Let me share a couple of high lights.

## Major High Lights

I had alot of discussion with the project mentors regarding Teuthology and SSL support since certain operations in the AWS go SDK 
require SSL to be enabled. I therefore decided that the tests that require SSL will be skipped in environments where SSL is not
enabled.

I also took alot of time setting up an SSL environment to run the tests. Thanks for Marcus' help as I implemented more tests on 
bucket ACl, AWSV4, bucket lifecycle configuration and object/bucket headers.I will quickly share a summary of what has been implemend 
so far.

## What has been implemented so far
               
### AWSV4
+ Sign requests and handlers
+ Presign requests and handlers              
### Basic Bucket     Operations
+ Create, Read, Update and Delete of buckets. 
+ Bucket Creation with all possible headers 
### Bucket ACL
### Bucket Lifecycle configuration        
### Basic Object     Operations          
+ Create, Read, Update and Delete of objects        
+ Writing/Reading objects with all possible headers.    
+ Getting and setting metadata.    
+ Getting objects with delimiters, maxkeys, prefix, markers                  
### Multipart Uploads 
### Encryption                  
+ Reading and writing objects with server side encryption (SSE) and SSEKMSKeyId.        
+ Reading andwriting objects with SSECustomerAlgorithm, SSECustomerKey and SSECustomerKeyMD5.              
### Host style

There is a [checklist](https://docs.google.com/document/d/1jbziCPfk2nSs5kycT_RJ64hcqWo6kupfWPQwGAGpYU0/edit) of these tests also 
prepared to give a summary.

This does not mean I am totally done with this suite. I have just decided to give an update but also asking for feedback.I am 
inviting for the community to open issues where possible.

## Tasks for the next Period

As stated earlier, am not yet done with this test suite and with that said I will priotise whatever issues will be opened and 
will work on them according to priority till end of summer.

Like Jay-Z says,Onto the next one. I will move on to starting work on Java test Suite. I will first communicate afew decisions 
regarding the stack I will use for feedback and then get in to motion with the rest of the work.



