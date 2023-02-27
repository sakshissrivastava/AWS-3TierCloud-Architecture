# AWS-3TierCloud-Architecture
This repository contains the capstone project of AWS Cloud Technical Essential

Scenario: 
You have a web application that accepts requests from the internet. Clients can send requests to query for data. When a request comes in, the web application queries a MySQL database and returns the data to the client.

Instructions: 
Design a three-tier architecture that follows AWS best practices by using services such as Amazon Virtual Private Cloud (Amazon VPC), Amazon Elastic Compute Cloud (Amazon EC2), Amazon Relational Database Service (Amazon RDS) with high availability, and Elastic Load Balancing (ELB). Create an architecture diagram that lays out the design, including the networking layer, compute layer, database layer, and anything else that’s needed to accurately depict the architecture and describe how traffic flows through the different AWS components—from the client to the backend database, and back to the client. 

Here's my take on the Capstone Project

Description:
The AWS region contains 2 Availability Zones for higher availability of the Web applications to the consumers. Each of these AZ contains Public and Private Subnet with EC2 instance in Public and RDS (MySQL) instance in Private subnet. The internet connection is established between the client and the VPC (Virtual Private Cloud) by the Internet Gateway. 

The clients sends the HTTP request to query the data. This request reaches the VPC through internet gateway and makes its way to the load balancer. Here Application Load Balancer is used since the request is sent through web application that deals with HTTP server. The load balancer distributes the traffic to the EC2 instances hosted on both the AZ on the round robin basis.

Auto Scaling groups attached with EC2 instance manages scaling based on the traffic coming form the internet. These EC2 instances is guarded by the security group which accepts the traffic only from internet gateway. 

The EC2 instances in turn communicates with the RDS instance hosted on different Availability Zones and fetches the data from the database and shares the response back to the client through the same channel. RDS instances are guarded by the security group which only accepts traffic from EC2 instance. The Auto Scaling Groups attached to the database manages the scaling based on the rise and fall of EC2 traffic. 

Hence this way we have taken care of both Availability and Scalability of the resources.

