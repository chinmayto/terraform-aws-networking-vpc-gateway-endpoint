# Deploying a VPC Gateway Endpoint to connect to S3
Deploying a VPC Gateway Endpoint to connect to S3

A VPC endpoint enables customers to privately connect to supported AWS services and VPC endpoint services powered by AWS PrivateLink. Amazon VPC instances do not require public IP addresses to communicate with resources of the service. Traffic between an Amazon VPC and a service does not leave the Amazon network.

There are two types of VPC endpoints:
1. interface endpoints
2. gateway endpoints

### Gateway endpoints

A gateway endpoint targets specific IP routes in an Amazon VPC route table, in the form of a prefix-list, used for traffic destined to Amazon DynamoDB or Amazon Simple Storage Service (Amazon S3). Gateway endpoints do not enable AWS PrivateLink. Instances in an Amazon VPC do not require public IP addresses to communicate with VPC endpoints, as interface endpoints use local IP addresses within the consumer Amazon VPC. Gateway endpoints are destinations that are reachable from within an Amazon VPC through prefix-lists within the Amazon VPC’s route table. There is no additional charge for using gateway endpoints.

### Architecture Diagram:

![alt text](/images/diagram.png)

Step 1: Create a VPC

Step 2: Create IAM role with policy and instance profile for s3 access

Step 3: Create Bastion and Private host with instance profile.

Step 4: Create S3 bucket

Step 5: Create VPC Gateway Endpoint connected to private route table 

Terraform Apply Output:
```
Apply complete! Resources: 18 added, 0 changed, 0 destroyed.

Outputs:

s3_bucket_name = "s3-test-bucket-ct"
vpc_a_bastion_host_IP = "54.173.10.180"
```

### Testing:
VPC Gateway Endpoint:

![alt text](/images/gateway_endpoint.png)

Prefix list association added to private route table:

![alt text](/images/prefix_list.png)

S3 Bucket:
![alt text](/images/s3bucket.png)

Accessing S3 bucket from private host via gateway endpoint:

![alt text](/images/s3access1.png)

![alt text](/images/s3access2.png)

Terraform Destroy Output:
```
Destroy complete! Resources: 18 destroyed.
```