---
layout: post
title: Adding AWS if-none-match headers on UploadInput(Golang)
comments: true
---

**[Outreachy.Started](https://github.com/nanjekyejoannah/Outreachy-RGW-testing)**

After six hours of looking for a way of adding if-none-match headers on UploadInput and MultiPartUpload Input, I had to record this here for my own reference but also to save someone else time in the future.I read the whole AWS Go SDK developer guide in vain in these hours.

Now there is an [AWS Go SDK](https://github.com/aws/aws-sdk-go) that we use to interface  the Amazon web services. I was working with the s3 interface and needed to perform an UploadInput Input.

After rigorous and persistent search (with rumblings ofcorse) on the internet I got to find out that actually the AWS Go SDK S3 team needs to add this feature to their public API. It is a [feature request](https://www.bountysource.com/issues/45142786-feature-request-ifnonematch) that was reported like three weeks when i tried to access it. However below is a work around that saved my day.

	func WithIfNoneMatch(conditions ...string) request.Option {
	    return func(r *request.Request) {
	       for _, v := range conditions {
	            r.HTTPRequest.Header.Add("If-None-Match", v)
	       }
	    }
	}
	svc := s3.New(sess)

	svc.PutObjectwithContext(ctx, &s3.PutObjectInput{
	    Bucket: aws.String(myBucket),
	    Key:      aws.String(myKey),
	    Body:    reader,
	    // Other parameters...
	}, WithIfNoneMatch("etag")


Happy hacking, I am now on to connecting my tests to RGW on my summer outreachy project. 

**The world is against me today !!!** 

Nevertheless very positive.
