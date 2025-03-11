# Deploying a Serverless Demo with AWS Lambda

## 1. Create an AWS Lambda Service and select Python as the runtime.

## 2. Write the following Python code for the Lambda function:

  ```python
 import json

def lambda_handler(event, context):
    body = json.loads(event['body'])
    cust_name = body['cust_name']
    cust_position = body['cust_position']
    print("Loading")
    
    return {
        'statusCode': 200,
        'body': json.dumps('Hello {} - {}. Have a good day!'.format(cust_name, cust_position))
    }
  ```

## 3. Use Postman to send a request to the API endpoint with the following JSON payload:

  ```
  {
    "cust_name": "Pham Chi Vy",
    "cust_position": "Student"
  }
  ```

![](assets/Apache.png)

## 4. Check the logs in AWS CloudWatch to verify the request processing and execution results. 🚀

![](assets/Apache.png)

