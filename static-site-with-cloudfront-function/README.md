# Create a static site with cloudfront that uses CloudFront Functions
First template is the template-cloudfront-function.yml. This creates a CloudFront function that adds security headers to the viewer response. 
You can attach this function to many CloudFront distributions. The second template either takes a bucket you already have or creates a new s3 
bucket and configures a cloudfront distribution and route53 CNAME in front of it.

## Deploy
```
/usr/local/bin/sam deploy --template-file /path/to/template-cloudfront-function.yaml \
  --stack-name cloudfront-functions \
  --s3-bucket your.s3.bucket \
  --capabilities CAPABILITY_IAM CAPABILITY_NAMED_IAM \
  --no-execute-changeset \

/usr/local/bin/sam deploy --template-file /path/to/template-static-site-with-cloudfront.yaml \
  --stack-name cloudfront-function \
  --s3-bucket your.s3.bucket \
  --capabilities CAPABILITY_IAM CAPABILITY_NAMED_IAM \
  --no-execute-changeset \
  --parameter-overrides \"SubDomain\"=\"yoursite\" \"HostedZoneName\"=\"example.com\" \"ExistingS3Bucket\"=\"sample-static-site\" \"CloudFrontStackName\"=\"cloudfront-functions\"
```
