# AWS-LOAD-BALANCER

## AIM
To use Elastic Load Balancing (ELB) and Auto Scaling services to load balance and automatically scale an AWS infrastructure.

## PROBLEM STATEMENT
As web applications receive varying levels of traffic, a single EC2 instance cannot reliably handle sudden spikes in demand, nor can it provide fault tolerance if that instance fails. Elastic Load Balancing (ELB) solves this by automatically distributing incoming application traffic across multiple EC2 instances and Availability Zones, ensuring high availability and fault tolerance.

However, load balancing alone does not solve the problem of capacity — if traffic increases beyond what the current instances can handle, more instances are needed; when traffic decreases, running excess instances wastes cost. AWS Auto Scaling addresses this by automatically launching or terminating EC2 instances based on defined conditions (such as CPU utilization), maintaining application performance while minimizing cost.

This experiment demonstrates how to create a reusable Amazon Machine Image (AMI) from a running server, configure an Application Load Balancer to distribute traffic, set up a Launch Template and Auto Scaling group to automatically manage instance capacity, and use CloudWatch alarms to trigger and verify scaling behavior under load.

## ALGORITHM
### Step 1: Create an AMI for Auto Scaling
Open the EC2 console, confirm that Web Server 1 is running (2/2 status checks passed), select the instance, and choose Actions → Image and templates → Create image. Name it "WebServerAMI" and create it. This AMI will be used to launch identical instances later.

### Step 2: Create a Target Group and Load Balancer
Create a Target Group named "LabGroup" (type: Instances, VPC: Lab VPC) without registering targets yet. Then create an Application Load Balancer named "LabELB" under Lab VPC, mapped to Public Subnet 1 and Public Subnet 2, using the Web Security Group, with the HTTP:80 listener forwarding to LabGroup.

### Step 3: Create a Launch Template and Auto Scaling Group
Create a Launch Template named "LabConfig" using the WebServerAMI, instance type t2.micro, key pair "vockey", the Web Security Group, and Detailed CloudWatch monitoring enabled. Using this template, create an Auto Scaling group named "Lab Auto Scaling Group" attached to Private Subnet 1 and Private Subnet 2, linked to the LabGroup target group, with desired/minimum/maximum capacity of 2/2/6 and a target tracking scaling policy set to maintain 60% average CPU utilization.

### Step 4: Verify Load Balancing
Confirm that two new "Lab Instance" EC2 instances were launched by Auto Scaling and that both show a "healthy" status in the LabGroup target group. Copy the Load Balancer's DNS name and open it in a browser to confirm the application is being served correctly through the load balancer.

### Step 5: Test Auto Scaling
Lower the scaling policy's target CPU value to 50% to make scaling trigger sooner, then use the application's "Load Test" feature to generate high CPU load across the instances. Monitor the CloudWatch alarms (AlarmLow/AlarmHigh) until AlarmHigh enters the "In alarm" state, then verify in the EC2 console that additional instances were automatically launched to handle the load.

### Step 6: Terminate the Original Web Server
Select Web Server 1 (the original instance used to create the AMI) and terminate it, since it is no longer needed once the Auto Scaling group is managing instances independently.

## COMMANDS
No CLI commands are used in this experiment, as it is performed entirely through the AWS Management Console (GUI-based setup) using EC2, Elastic Load Balancing, Auto Scaling, and CloudWatch services.

## OUTPUT
### REG NUMBER:
212225040374
### NAME:
SANJAY S

<img width="692" height="349" alt="image" src="https://github.com/user-attachments/assets/ac7d8238-f31e-4f84-9a3e-8f147df8806f" />

<img width="692" height="347" alt="image" src="https://github.com/user-attachments/assets/01064232-74a1-407a-a02e-1ef1c484a753" />

<img width="692" height="348" alt="image" src="https://github.com/user-attachments/assets/5a34ec60-3677-4744-9640-5dbd6577bff1" />

<img width="692" height="350" alt="image" src="https://github.com/user-attachments/assets/575ee207-aa5e-4c12-b684-f39ae8ce8fec" />

<img width="692" height="348" alt="image" src="https://github.com/user-attachments/assets/a0cecdf5-bb12-417e-8720-67e10de12b40" />

<img width="692" height="347" alt="image" src="https://github.com/user-attachments/assets/c00e754e-0012-4afd-b46d-7f50bce9d148" />

<img width="692" height="347" alt="image" src="https://github.com/user-attachments/assets/39310f7d-381b-467e-8433-dc2cc525a138" />

<img width="692" height="348" alt="image" src="https://github.com/user-attachments/assets/b7c84c9d-bae1-43b3-8695-ce01dd2c4941" />

<img width="693" height="350" alt="image" src="https://github.com/user-attachments/assets/380d7f6d-faf3-47b3-aa55-8f5cd359e190" />

<img width="692" height="349" alt="image" src="https://github.com/user-attachments/assets/eb9953e4-78c1-45a8-8154-6629b86e86e1" />

<img width="692" height="347" alt="image" src="https://github.com/user-attachments/assets/a8d6434e-7c9f-4b98-9927-45659c3e8341" />

<img width="692" height="348" alt="image" src="https://github.com/user-attachments/assets/093f5647-5d1b-46f7-8a27-e34462324fd3" />

<img width="692" height="348" alt="image" src="https://github.com/user-attachments/assets/652ca440-dbbe-4c58-9155-da4aca9963cf" />

<img width="692" height="346" alt="image" src="https://github.com/user-attachments/assets/9428e531-58fe-439b-9d17-8b7e9b87032a" />

<img width="692" height="349" alt="image" src="https://github.com/user-attachments/assets/e3a190a4-62db-402f-a055-7d824f4dd9b6" />

<img width="692" height="348" alt="image" src="https://github.com/user-attachments/assets/fda6d721-a362-4e4e-8047-b77f16b848e5" />

<img width="692" height="347" alt="image" src="https://github.com/user-attachments/assets/21afd99a-c230-45fd-a8f7-8aae1a3f5553" />

<img width="692" height="348" alt="image" src="https://github.com/user-attachments/assets/9a4fe52a-0755-4d84-b1be-b34a1ec1a063" />

<img width="692" height="347" alt="image" src="https://github.com/user-attachments/assets/3a30f703-7e2d-4401-a788-f849ffbfb1b2" />

<img width="692" height="347" alt="image" src="https://github.com/user-attachments/assets/8cbab2cd-bf41-40cb-89a6-83cedda51a32" />

<img width="693" height="349" alt="image" src="https://github.com/user-attachments/assets/f1693cf2-818e-4417-95e7-73eb8fa4cc2b" />

<img width="692" height="347" alt="image" src="https://github.com/user-attachments/assets/5892fe82-94f8-49aa-8cd0-3f1975a620e7" />

<img width="693" height="348" alt="image" src="https://github.com/user-attachments/assets/525f9d3a-c28b-40b4-be34-10e5fb975dec" />

<img width="692" height="349" alt="image" src="https://github.com/user-attachments/assets/f40cf124-5905-4e32-ad1c-410d899abdf1" />

<img width="692" height="351" alt="image" src="https://github.com/user-attachments/assets/0f919405-af21-40ed-be3d-c19ead2c65e6" />

<img width="692" height="347" alt="image" src="https://github.com/user-attachments/assets/015bab90-885c-456c-8a21-eb6f7306fd38" />

<img width="692" height="344" alt="image" src="https://github.com/user-attachments/assets/9ba5cdfb-8539-46f9-9a50-163efcbe606e" />

<img width="692" height="348" alt="image" src="https://github.com/user-attachments/assets/70dba6fa-f66f-4705-b160-c3cd8d7a51b1" />

<img width="692" height="351" alt="image" src="https://github.com/user-attachments/assets/f8d3d759-7109-4dd7-95f2-3961d4d6ba53" />

<img width="692" height="349" alt="image" src="https://github.com/user-attachments/assets/1574bd9f-4783-4db1-8005-e0bf1a719d77" />

<img width="692" height="350" alt="image" src="https://github.com/user-attachments/assets/afe82026-c49b-40f8-8644-74c428c7c051" />

<img width="692" height="348" alt="image" src="https://github.com/user-attachments/assets/49e74c23-3b53-4105-ad86-525c4fe0dc64" />

<img width="692" height="349" alt="image" src="https://github.com/user-attachments/assets/2768e4c1-1076-484f-97f3-034d8da12efe" />

<img width="692" height="346" alt="image" src="https://github.com/user-attachments/assets/2e53d1d6-9bac-4551-b068-a08520799cde" />

## RESULT
Thus, an AMI was created from a running EC2 instance, a Load Balancer was configured to distribute traffic across multiple instances, an Auto Scaling group was set up with a target tracking scaling policy, and the infrastructure was verified to automatically scale out under increased load using CloudWatch alarms.
