# CrowdStrikeFDR-AWS
Cloudformation template for an AWS Lambda function as a CrowdStrike FDR consumer. 

CrowdStrike's Falcon Data Replicator (FDR) is a service provided by CrowdStrike which allows downloading of log files for archival or log analytics.  They provide a sample consumer based on (as of this writing) python 2.7 intended to run on an instance or virtual machine.  CrowdStrike also provide FDR customers an SQS queue url, key, and secret for access.

I used CrowdStrike's sample as the launch point to create a python 3.7 (also tested with 3.8) lambda function which performs the same actions.  The queue url, key, and secret are stored in AWS Secrets Manager, and retrieved by the lambda function.  Events are pulled and parsed from the queue, and then the compressed logs are downloaded from CrowdStrike's S3 bucket to a local bucket.  In our use case, this is then further ingested by our upstream log analytics platform. The lambda function is scheduled to run every minute by a cloudwatch event.

# Instructions
1. Create a secrets manager secret in the same region as you want your lambda function and will run CloudFormation.  It should contain three entries (key, secret, and queue).  Enter the details provided by CrowdStrike.
2. Run the cloudformation template.
3. Validate the components were all created as expected and you have data flowing into your bucket.

# NOTE: This template was not provided or supported by CrowdStrike.  
