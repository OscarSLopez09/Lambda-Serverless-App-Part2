# Let's start with a high-level overview.

In this section I'm going to create the second part of the project which is fetching the news based on sentiment.
I'm going to create the backend lambda function to fetch the sentiment to the end user.
The API gateway would be created on another repository.

Lets start by going to the aws console and search for Cloud9, the open Cloud9
On cloud9 create a directory - mkdir BackendSentiment
Move into the directory - cd BackendSentiment
Create a python file with - nano lambda_function.py
Copy and Paste the python code and save it
Check the file creation with - ls -lthr
Proceed to zip up the files - zip -r lambda.zip *
Uploda the zip file to AWS Lambda by running the AWS command

Go to AWS Lambda to check if the function has been created
On Lambda console refresh the screen and the function should appeared
Proceed to create a test event to check the Lambda
Click on the Test tab
Select the Create new event
Event name - Event1
Template optional select -hello-world
On Event JSON - {"sentiment":"NEUTRAL"}
Save the test event
Click on test
Go to Amazon Dynambo DB to check if is storing the news with sentiment
on the search box type Dynamo DB
Select the table news
Click the refresh buttom to see the results
Result successful
































