# Justification about the selected EC2 Instance Type:
<p align="center">
    <img src="https://user-images.githubusercontent.com/98076289/231658842-6b3d3b3a-b5a7-4fdf-add9-59fff6c06cd8.png">
</p> 
According to the above note deplayed on DLAMI instances in ec2 G3,P3,P3de, G5, G4dn instance tpes are supported for the Deep Learning AMI GPU PyTorch 2.0.0 (Amazon Linux 2) 20230406Deep Learning AMI GPU PyTorch 2.0.0 (Amazon Linux 2) 20230406. Therefore G3 instance type has been chosen to provide the optimal level of requirement for the AMI and On demand instance has been chosen due to spot instance are not defaulting supported for G3 the service quota for the G3 instance should be increased to achieve this.

# The EC2 Code Compared to the SageMaker Code:
<p align="center">
    <img src="https://user-images.githubusercontent.com/98076289/231662055-14f3c1ed-1629-4312-ad10-d97bba454714.png">
</p> 

Both Sagemaker and EC2 code for train the model are similar instead the followings;
- In Sagemaker we first do the hyperparameter tuning for and select the best parameter values for the model training but in ec2 instance training job we didn't do such kind of hyper parameter tuning..
- Also in Sagemaker we have to store data in S3 bucket, and have to import them into sagemaker using sagemaker method to train the models. But in EC2 instance it is more similar to train the model inside an own machine.

# Step3 - The Lambda Function  
<p align="center">
    <img src="https://user-images.githubusercontent.com/98076289/231739837-21ac41f9-c023-4411-9a59-d93bf0740a62.png">
</p>  

- The lambda function has been deployed with the provided code by updating the endpoint name as above.  
<p align="center">
    <img src="https://user-images.githubusercontent.com/98076289/231737447-d834e509-9f49-4cc0-8dbc-91d6585408e7.png">
</p>  

- Intial function didn't have the necessary permission to access to the Sagemaker. Therefore, Sagemaker full access permission has been attached to the endpoint-invocation-role-27an2d7i role.  
<p align="center">
    <img src="https://user-images.githubusercontent.com/98076289/231738553-00a7e088-941d-4047-ba89-b4ba66a6545b.png">
</p>  

<p align="center">
    <img src="https://user-images.githubusercontent.com/98076289/231738110-4e2a640d-9845-44e9-a86f-42143fecaa7b.png">
</p>  

- After attaching the role the endpoint invokation was successfully done with the "url": "https://s3.amazonaws.com/cdn-origin-etr.akc.org/wp-content/uploads/2017/11/20113314/Carolina-Dog-standing-outdoors.jpg".
