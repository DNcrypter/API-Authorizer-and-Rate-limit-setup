# API Rate Limiting and Authorization with AWS Lambda and API key

This project is an extension of our previous AWS Serverless API application. It focuses on authorizing API requests, implementing rate limiting, and creating API keys to secure your database from unauthorized access and attacks.

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)
        [![LinkedIn](https://img.shields.io/badge/LinkedIn-Profile-blue)](https://www.linkedin.com/in/nikhil--chaudhari/)
        [![Medium](https://img.shields.io/badge/Medium-Writeups-black)](https://medium.com/@nikhil-c)

[![Watch the video](https://github.com/DNcrypter/API-Authorizer-and-Rate-limit-setup/blob/main/images/image2.png)](https://www.youtube.com/watch?v=L9zknaA6lD4)


## 🍁 Introduction

In this project, we aim to enhance the security and performance of our serverless API application by adding an authorizer, implementing rate limiting, and creating API keys. These measures will help prevent attackers from deleting or updating the content of the database and ensure that the API is used efficiently and securely.

## ✍ Architecture
![image1](https://github.com/DNcrypter/API-Authorizer-and-Rate-limit-setup/blob/main/images/image1.png)

The architecture for this project includes the following components:
- AWS Lambda functions for authorizing API requests
- Amazon API Gateway for handling API requests and responses
- Amazon DynamoDB for storing API keys and rate limit data
- AWS CloudWatch for monitoring and logging

## ☑️Setup

### Prerequisites

- AWS account
- Postman api testing tool

### Installation

1. Clone the repository:
   ```
   git clone https://github.com/your-username/api-authorization-and-rate-limiting.git
   cd api-authorization-and-rate-limiting

   ```

### 🍁 Implementation
* As we already setup API application as micro service. you can refer my last project:
[![Static Badge](https://img.shields.io/badge/Github-Project-blue)](https://github.com/DNcrypter/AWS-serverless-API-application)

#### Lambda Authorizer
* create lambda function using lambda aws service.
* click on create function.
* insert function name as "**lambdaAuth**"
* insert code inside lambda source code editor. code of lambda function is given in downloaded repo with name "**lambda_authoriser.py**" file.
* copy it, insert it and press deploy button.

#### API Gateway Auth integration
* click on stage_tab **>** Get **>** Method_request, edit the method_request and give value to authorization:"lambdaAuth". Also right tick "API_key_required".
* provide value in token tab as "**Authorization**"

Now your lambda Authorizer is setup for Get request do this for all given requested methods in our api.

#### Setup Rate limit
* click on usage plan that is in left down side. name the plan "api-usage-plan". provide rate and burst value as("per second") :
* rate:1 , burst:2
* provide number of request per day as "30" to restrict my api to not cross free tier limit. This is optional. I have setup because, this link will be publically available for demo purpose.

#### API Key 
* create api key to restrict other user and only allow those who have api key.
* I have attached this api key to only **delete** method but you can do for **post** and **put** method. Because these methods are link with data adding and updating.



### API Testing
#### Lambda Authorizer
* open Postman tool add url and select get method and click on send.
* it show 403 forbidden.
* Now enter header :
* Authorization : "Value"
* "Value" is (password_value is provide in **lambdaAuth** Function.)
* 200 ok status, shown all data inside Dynamodb database.


#### API key Defense Mechanism
* enter url {https://opxfw4472e.execute-api.ap-south-1.amazonaws.com/dev/books/6} and select delete method and click send.
* showing status 403 forbidden.
* Now provide header x-api-key : value
* value is api key that is available in your aws api key section.
* click send, showing 204 status.
* check, value is now deleted.


### Conclusion
In this project, we successfully enhanced our serverless API application with secure authorization, rate limiting, and API keys. These improvements safeguard our database and ensure efficient API usage. This solution leverages AWS Lambda and API Gateway to maintain robust security and performance.
