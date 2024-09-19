CloudFormation Template Description
This CloudFormation template automates the deployment of a basic AWS infrastructure setup. The components created by this template include:

VPC (Virtual Private Cloud):

Creates a new VPC with a CIDR block of 10.1.0.0/16.
Enables DNS support and DNS hostnames within the VPC.
Internet Gateway:

Creates an Internet Gateway (IGW) and attaches it to the VPC to allow internet access.
Public Subnets:

Creates two public subnets in different Availability Zones (AZs):
PublicSubnetAZ1 in us-east-1a with a CIDR block of 10.1.1.0/24.
PublicSubnetAZ2 in us-east-1b with a CIDR block of 10.1.2.0/24.
Configures these subnets to automatically assign public IP addresses to instances launched within them.
Route Table:

Creates a route table for the VPC.
Adds a route to direct traffic destined for the internet (0.0.0.0/0) to the Internet Gateway.
Associates this route table with both public subnets to ensure they can communicate with the internet.
Security Groups:

EC2 Security Group: Allows inbound SSH (port 22) and HTTP (port 80) traffic from any IP address. This security group is associated with EC2 instances.
Load Balancer Security Group: Allows inbound HTTP (port 80) traffic from any IP address. This security group is associated with the load balancer.
EC2 Instances:

Instance 1: Launches an EC2 instance in us-east-1a with the latest Ubuntu AMI. The instance is configured to run Apache HTTP Server (apache2) on startup, displaying a simple HTML message.
Instance 2: Launches an EC2 instance in us-east-1b with the latest Ubuntu AMI. This instance is also configured to run Apache HTTP Server, with a different HTML message.
Load Balancer:

Creates an Application Load Balancer (ALB) that distributes incoming HTTP traffic across the two EC2 instances.
The ALB is associated with the public subnets to ensure it can receive traffic from the internet.
Target Group:

Creates a target group for the ALB, which includes the two EC2 instances.
Configures health checks to ensure only healthy instances receive traffic.
Listener:

Creates an HTTP listener for the ALB that forwards incoming traffic to the target group.
Outputs:

Provides the DNS name of the Load Balancer, allowing you to access the deployed application via the internet.
