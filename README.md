# Let's start with a high-level overview.

In this section I'm going to create the second part of the project which is fetching the news based on sentiment.
I'm going to create the backend lambda function to fetch the sentiment to the end user.
The API gateway would be created on another repository.

This is the 2nd part of the project, links to the other parts of the project:

- [Part 1 Lambda Serverless App ](https://github.com/OscarSLopez09/Lambda-Serverless-App)
- [Part 2 Creating the backend lambda](https://github.com/OscarSLopez09/Lambda-Serverless-App-Part2)
- [Part 3 Creating API Gateway ](https://github.com/OscarSLopez09/Serverless-App-Part2-API-GW)
- [Part 4 Creating CloudWatch event](https://github.com/OscarSLopez09/Serverless-Cloudwatch-Rule)
- [Part 5 Implementing security with API keys ](https://github.com/OscarSLopez09/Lambda-Serverless-App-Security)


   


## Lambda backend Function

* Lets start by going to the aws console and search for Cloud9, then open Cloud9
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Part2/blob/main/Images/backendlambda00.PNG" height="90%" width="800%" alt="Disk Sanitization Steps"/>

* On cloud9 create a directory - mkdir BackendSentiment
* Move into the directory - cd BackendSentiment
* Create a python file with - nano lambda_function.py
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Part2/blob/main/Images/backendlambda01.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>


* Once the editor is open I copy and paste the following Python code
```python

import boto3
from boto3.dynamodb.conditions import Key

def lambda_handler(event, context):
    # TODO implement
    dynamodb = boto3.resource('dynamodb') 
    table = dynamodb.Table('news')
    inputSentiment=event['sentiment']
    try:
        # Querying the table using Primary key
        response = table.query(
            KeyConditionExpression=Key('sentiment').eq(inputSentiment),
            Limit=10, #limits returned news to 10
            ScanIndexForward=False) #descending order of timestamp, most recent news first
        return response
    except:
        raise
```

<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Part2/blob/main/Images/backendlambda02.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>

* Check the file creation with - ls -lthr
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Part2/blob/main/Images/backendlambda03.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>

* Proceed to zip up the files - zip -r lambda.zip *
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Part2/blob/main/Images/backendlambda04.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>

* Uploda the zip file to AWS Lambda by running the following AWS command
```
aws lambda create-function --function-name NewsReaderBacked --runtime python3.11 --handler lambda_function.lambda_handler --role arn:aws:iam::785973594274:role/DynamoDB_Comprehend --zip-file fileb:///home/ec2-user/environment/BackendSentiment/lambda.zip
```
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Part2/blob/main/Images/backendlambda05.PNG" height="120%" width="120%" alt="Disk Sanitization Steps"/>

* Go to AWS Lambda to check if the function has been created
* On Lambda console refresh the screen and the function should appeared
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Part2/blob/main/Images/backendlambda06.PNG" height="100%" width="100%" alt="Disk Sanitization Steps"/>

* Click on the function - NewsReaderBacked
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Part2/blob/main/Images/backendlambda07.PNG" height="100%" width="100%" alt="Disk Sanitization Steps"/>

## Create a test event

* Proceed to create a test event to check the Lambda
* Click on the Test tab
* Select the Create new event
* Event name - Event1
* Template optional select - hello-world
* On Event JSON type the below
```JSON
{
  "sentiment":"NEUTRAL"
}
```
* Save the test event
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Part2/blob/main/Images/backendlambda08.PNG" height="100%" width="100%" alt="Disk Sanitization Steps"/>

* Click on test
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Part2/blob/main/Images/backendlambda09.PNG" height="100%" width="100%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Part2/blob/main/Images/backendlambda10.PNG" height="100%" width="100%" alt="Disk Sanitization Steps"/>

* Go to Amazon Dynambo DB to check if is storing the news with sentiment
* On the AWS search box type Dynamo DB
* Select the table news
* Click the refresh buttom to see the results
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Part2/blob/main/Images/backendlambda11.PNG" height="100%" width="100%" alt="Disk Sanitization Steps"/>
  
## Result successful!!
































