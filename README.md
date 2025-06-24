# Module 2B Lambda SQS Processor

## Topics Covered in Module 2

  - Benefits of EC2
  - Instance Types
  - EC2 Pricing
  - Scaling EC2
  - Elastic Load Balancing
  - Messaging and Queing
  - Additional Compute Services

## Project Description
The first lab of this module utilizes EC2. With this second lab I wanted to go over one of the serverless computing options (lambda). I will write a simple function that will trigger from an SQS message. The lambda function will then log the message to a cloudwatch log group.

## Steps
1. I first created a Standard SQS queue and left all of the options standard. Standard queues will be used most of the time over FIFO (first-in-first-out).

![image](https://github.com/user-attachments/assets/a79ad608-d017-462f-9d23-cfcb951125c9)

2. Then I created my lambda function. I set the name as SQSProcessor and set the runtime to python. I left the rest of the options to default.
   
![image](https://github.com/user-attachments/assets/241e7db0-3daf-462c-8e23-753775a3fc88)

3. Before adding the SQS queue as a trigger, I have to adjust the permissions for the IAM role of the lambda function. I added fullaccess to both SQS and CloudWatch. Without adding these permissions, the trigger would not set and you would get a permission denied error.

![image](https://github.com/user-attachments/assets/f50d3177-8843-4fff-9b8d-73030543b8b7)

4. It can now be seen that the SQS queue is a trigger for the function.
   
![image](https://github.com/user-attachments/assets/a3f3bfd9-0209-4b68-a07b-62ab23541d9b)

5. Now its time to adjust the code to carry out the intended functionality. This code is a basic AWS Lambda function designed to handle messages from an SQS queue. When triggered, it loops through each message in the incoming event (which contains one or more records), extracts the message body from each one, and prints it to the logs (which you can view in CloudWatch). After processing all messages, it returns a simple HTTP-style response confirming success.

![image](https://github.com/user-attachments/assets/4efc6311-3f0e-4878-ba41-3e2ef41301b8)

6. After clicking deploy, it's time for testing. I went back to the SQS queue and selected send/recieve messages and sent the message below to the queue.
   
![image](https://github.com/user-attachments/assets/1550d82d-a124-4b7a-b85f-821c1b993471)

7. To see if this worked, I went to the cloudwatch logs group for the SQSProcessor. As seen below, the message can be found in the logs as intended.
   
![image](https://github.com/user-attachments/assets/44ee35d7-3d27-429a-a5ed-6666144096b9)
