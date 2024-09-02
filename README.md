# Deploy-an-application-in-a-VPC-with-private-subnets-
![image](https://github.com/user-attachments/assets/5bae6fae-4a03-4e79-8414-edf4a0dfbd6e)

The VPC has public subnets and private subnets in each of the two Availability Zones. Each public subnet contains a NAT gateway and a load balancer node. The servers run in the private subnets, are launched and terminated by using an Auto Scaling group and receive traffic from the load balancer. The servers can connect to the internet by using the NAT gateway.

Log in to your AWS Management Console using your credentials. Navigate to VPC Dashboard by searching for “VPC” in the AWS services search bar or directly accessing it from the services menu.

# Create a VPC:
Go to the VPC dashboard in the AWS Management Console.
Click on “Create VPC”.
Provide a name for your VPC, select the CIDR block, and enable DNS support.
Create two public subnets and two private subnets, each in a different availability zone of the Mumbai region (1a and 1b). I have selected Mumbai region. You can select anything as you need.
Make sure to associate a route table with each subnet and configure the public subnets to have access to the internet through an Internet Gateway (IGW)
![Screenshot 2024-09-02 115149](https://github.com/user-attachments/assets/c6c876ca-d0e9-4c88-877b-faa956d982b0)
# Creation of an Auto Scaling Group:
Go to the EC2 dashboard and navigate to the “Auto Scaling Groups” section.
Click on “Create Auto Scaling Group”.
Choose the launch template option and create a launch template with the desired configuration (minimum 1 instance, maximum 4 instances, desired capacity 2 instances). Launch Templates allow you to create a saved instance configuration that can be reused, shared and launched at a later time. Templates can have multiple versions.
Specify the AMI, instance type, security groups (allowing necessary traffic), key pair, etc.
Configure scaling policies if needed.
Associate the auto scaling group with the private subnets in the Network tab as shown in the image below.
![Screenshot 2024-09-02 115610](https://github.com/user-attachments/assets/2a243d19-8dcc-4f1d-9c8c-1a9a4f2699de)

# Creation of a Bastion Host:
Launch a new EC2 instance in one of the public subnets (public subnet in Mumbai 1a or 1b).
Ensure that the security group allows SSH access from your IP address.
Assign an Elastic IP to the instance for persistent public IP.
Connect to the bastion host using SSH.
![Screenshot 2024-09-02 115435](https://github.com/user-attachments/assets/5db392f6-a7d8-4bdf-ae80-9197169c11e8)

# Deployment of Sample Application on Primary Web Server:
Copy the PEM file to the bastion host which is needed to connect to EC2 instances that are in the private subnet.
SSH into the primary web server (one of the instances in the private subnet).
Deploy your sample application and run a Python HTTP server.
Test the application locally on the primary web server to ensure it’s running correctly.


# Creation of Load Balancer and Target Group:
Go to the EC2 dashboard and navigate to the “Load Balancers” section.
Click on “Create Load Balancer” and choose the type (e.g., Application Load Balancer).
Configure listeners and select the availability zones.
Create a target group and add the primary and secondary web servers as targets.
Configure health checks and routing settings as needed.
![Screenshot 2024-09-02 115518](https://github.com/user-attachments/assets/5fa7e8a5-86aa-4715-b3fe-931600d1c283)
and Target group
![Screenshot 2024-09-02 115652](https://github.com/user-attachments/assets/3c9d5645-9857-43d8-81fd-47a5be5c3497)

# Ec2 instances connect pdf as a link :
https://drive.google.com/file/d/15Omr_W8kcFVJnPQuc1HkvKZwhjz75aiN/view?usp=drivesdk
# result link :
http://project1-432817283.us-east-1.elb.amazonaws.com/
# Result Images
![Screenshot 2024-09-02 123139](https://github.com/user-attachments/assets/e0d374e1-78af-4b00-b9bd-e4a69b6ab1c5)
![Screenshot 2024-09-02 123209](https://github.com/user-attachments/assets/cc5c7eec-f05b-4c53-991c-1c402599edd5)
