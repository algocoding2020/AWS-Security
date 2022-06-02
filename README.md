# AWS-Security
Remove security group created to allow access from CIDR 0.0.0.0/0:
On the left we have a user. The user creates a security group, that fires off a CloudTrail event in AWS CloudTrail, so if you would open AWS CloudTrail, you would be able to see
that the user has created the security group. AWS CloudTrail can be configured that the CloudTrail events got to an S3 bucket.
So, we can have CloudTrail logs where all those events are being logged, and AWS CloudTrail can also be configured that it sends a notification to SNS.
SNS is a pub/sub service that we can then use to launch Lambda.
So what AWS CloudTrail is going to do, it is going to send an event with a bucket name and a key to our SNS topic, and then our SNS topic is going to send this data to a Lambda function.
Our AWS Lambda function will then retrieve from the S3 bucket the CloudTrail event, which is an S3 object.
It will then process this S3 object and then if it sees, if it finds the security group then we can have a certain analysis on it.
For example, if we do not want to allow the range 0.0.0.0/0 then we can check for that, and then we can have a possible deletion of the security group rule if it breaches our policies.
So, then the Lambda function can then remove the security group rule if it is in breach.

![image](https://user-images.githubusercontent.com/69389020/171694728-958417b4-81a1-4982-88e0-9c487eabdeb2.png)
