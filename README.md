# An Event-Driven Architecture for enforcing a project policy that restricts the use of EBS volumes to 'gp3', utilizing Lambda functions, EventBridge, and IAM

![ebs_volumes_conversion-diagram-ezgif com-effects](https://github.com/user-attachments/assets/e9e6fb77-97b6-4e41-a215-a2eacfcf2b17)




# Objective
Trigger a Lambda function when an Amazon Elastic Block Store (EBS) volume is created of type GP2 and convert them to type GP3.

# Overview:
we will demonstrate how to capture EC2 volume events using **Amazon EventBridge**, log them using **Lambda functions**, and automate the conversion of **ebs volumes** of type **gp2 to type gp3**. This setup enhances operational efficiency and provides real-time monitoring and automation for your AWS resources.

# Project Application
Suppose you work in a Project which only works with the **gp3 ebs** but by mistake someone created the EBS with **gp2** in that scenario it will convert the **gp2 to gp3 automatically**.

##########################################################################################################################

# AWS Lambda Setup:
• Create a Lambda Function and Add code logic to convert EBS Volume type

   ![lambda_function_creation](https://github.com/user-attachments/assets/91aff582-861a-4046-a1bb-c9920abe9ae8)



•	Create the lambda function with the name of your choice and select the Python latest runtime, Leave the rest setting as it is.
•	Replace the following code with your code in the Lambda function.

![lambda_func_code](https://github.com/user-attachments/assets/4a7337db-76e1-4060-9f01-2d7014f6c714)


# EvenBridge Setup:
•	Create an EventBridge event to trigger the Lambda function
•	Open Rule in AWS Event Bridge and go to Rules and then Create Rules to Create Rule.
•	A rule watches for specific types of events. When a matching event occurs, the event is routed to the targets associated with the rule. A rule can be associated with one or more targets.)
•	In Our case, When the EBS volumes get created the EventBridge will listen to that event and route that event to Lambda function.

![rules_creation](https://github.com/user-attachments/assets/e9b2c9e5-0e8f-44da-8e52-c76c6f29ccc0)


•	Add the Name and description as per your choice and leave the default setting.

![image](https://github.com/user-attachments/assets/57c6a923-1a2b-40a5-97b5-945bffb084d4)


•	On the next page leave the default setting and scroll down to the last section Event pattern. \
•	Select EC2 AWS Service, EBS Volume Notification in Event type, Event type specification should be Specific event(s), and select modifyVolume and create volume.

![event-pattern](https://github.com/user-attachments/assets/173f076c-55b7-4318-83f9-fd99e7c25b76)


On the next page in the Target Section select AWS Lambda in AWS Service and select the Lambda function we created.

![target](https://github.com/user-attachments/assets/0c35f8d6-2a5d-4ada-af50-0b1dfe9630a9)


# •	After Creating the Event Rule, try to create the EBS instance of Type GP2 and check whether that works. 
# •	It will throw the following error saying AWS Lambda doesn’t have access to modify EBS Volume. We will need to assign permission to the AWS Lambda Role.

# •	Open the role attached to AWS Lambda and Create an inline policy to modify the EBS Volume type.

# Create a gp2 volume and test the function :

•	Created  a Volume of type gp2:
![gp2](https://github.com/user-attachments/assets/cb7c1cfa-1144-4fd7-9537-7a208da7fcf3)

•	Volume got converted to gp3 automatically:
![gp3](https://github.com/user-attachments/assets/932015fc-4da7-42f5-8819-d8ceec1d9658)

# Congratulations! Your ebs has been converted to gp3
















   


