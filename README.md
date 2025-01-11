![image](https://github.com/user-attachments/assets/ed335950-1a8e-4935-adea-f3fd4ed46328)Amazon Virtual Private Cloud (Amazon VPC) enables you to launch AWS resources into a virtual network that you’ve defined. This virtual network closely resembles a traditional network that you’d operate in your own data center, with the benefits of using the scalable infrastructure of AWS.

Amazon VPC enables you to build a virtual network in the AWS cloud — no VPNs, hardware, or physical data centers required. You can define your own network space, and control how your network and the Amazon EC2 resources inside your network are exposed to the Internet.

What is the importance of having private and public subnets?

The instances in the public subnet can send outbound traffic directly to the internet, whereas the instances in the private subnet can’t. Instead, the instances in the private subnet can access the internet by using a network address translation (NAT) gateway that resides in the public subnet.



Create VPC from VPC Dashboard from AWS Console.

![image](https://github.com/user-attachments/assets/52ee1736-289d-40e9-a1bb-71e344c9d968)


Click on Create button which will create a VPC
2. Create subnets now, we’ll start with creating a public subnet now.

![image](https://github.com/user-attachments/assets/9dbe183e-bc73-4b49-8d83-0281560b5fe7)

![image](https://github.com/user-attachments/assets/1bf917f4-c1cd-4d8c-903a-071e96b59d9c)

3. Let’s create a private subnet now. This can be created using Subnets options from left hand side list in VPC Dashboard. Same process as the public subnet, except we are using a different IPv4 CIDR block.

![image](https://github.com/user-attachments/assets/baf7e457-b2ce-4c3c-aaae-fd4ae832340b)


Click on create subnet button.


What is an AWS CIDR block?

When you create a VPC, you must specify a range of IPv4 addresses for the VPC in the form of a Classless Inter-Domain Routing (CIDR) block; for example, 10.0. 0.0/16 . This is the primary CIDR block for your VPC.


 Modify Auto assign IP by right clicking on public subnet.

![image](https://github.com/user-attachments/assets/09c7ae92-7490-4c5f-8307-ef378709b8c4)

5. Create an Internet Gateway to use with our Public Subnet.

![image](https://github.com/user-attachments/assets/c575a1ac-c7ea-427c-acef-208c8533608b)
![image](https://github.com/user-attachments/assets/c3289683-92df-4bbc-b996-b61df618f6ec)


6. Attach Internet Gateway to VPC.

When you right click on internet gateway, it will show you Attach to VPC option as below.
Select the VPC you created and click on attach.
![image](https://github.com/user-attachments/assets/ef86fe84-93de-4921-b3da-a0b1c5640ac8)


7. Create NAT Gateway.

You can use a network address translation (NAT) gateway to enable instances in a private subnet to connect to the internet or other AWS services, but prevent the internet from initiating a connection with those instances.
Important: In order to access internet to your private subnet, NAT Gateway must be added to Public Subnet only.

![image](https://github.com/user-attachments/assets/0a748747-98b1-4b30-81ac-93a4cf7cc816)
![image](https://github.com/user-attachments/assets/fc91d33b-1ccd-442a-b723-b1bdbaee9a45)


8. Create Route Tables.

A route table contains a set of rules, called routes, that are used to determine where network traffic from your subnet or gateway is directed. To put it simply, a route table tells network packets which way they need to go to get to their destination.

![image](https://github.com/user-attachments/assets/c051299f-b471-4b26-835c-5093df0f8c89)


Add Internet Gateway to Public Route Table. Click ADD routes and attach.
![image](https://github.com/user-attachments/assets/1ff1c378-3c0e-49d5-80d3-6d4abedf5e26)


Add NAT gateway to Private Route Table. Click ADD routes and attach.

![image](https://github.com/user-attachments/assets/ca8f1cbb-c9f5-4771-b5b5-94045241d7e5)

Since we added NAT Gateway to public subnet, it will also have access to the internet.


9. Edit Subnet Association

Repeat steps for both your public and private Route Tables.
Click Edit Subnet Association button.




10. Create public and private EC2 instances.

Follow process for both public and private instances.
Pay attention to steps for what is particular to a certain instance.
First step, choose an AMI.


11. Testing the EC2 Instances.

Public Instance:

right click on box next to name of instance and click connect

![image](https://github.com/user-attachments/assets/9bb6a40f-897b-4dae-9a0e-8a848f9d3925)

![image](https://github.com/user-attachments/assets/d391d707-98be-47ca-800b-04327778be14)

![image](https://github.com/user-attachments/assets/538947a3-eaab-40d5-8801-dcac97f9d1f0)


Private Instance:

We’ll now connect to our private instance through our public instance.
Inside you public instance create a file for your keypair.
create a file for your keypair.


yum install vim
vim keypair.pem
:wq


Copy and paste contents of keypair inside your newly created keypair.pem file, your keypair file will look like the following below


chmod 600 keypair.pem
ssh -i keypair.pem ec2-user@private-ip-addres

![Uploading image.png…]()

12. Conclusion.

In conclusion, the machines on a private subnet can access the Internet because the default route on a private subnet is not the VPC “Internet Gateway” object — it is an EC2 instance configured as a NAT instance. A NAT instance is an instance on a public subnet with a public IP, and specific configuration





