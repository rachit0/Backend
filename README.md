# Backend
Backend Assignment
# Django Chat Application

This is a simple chat application built using Django. It allows users to send and receive messages in real-time, using Django's model-view-template architecture along with WebSockets for live message updates.

## Features

- Real-time messaging using WebSockets
- User authentication (login/logout/signup)
- Private and group chat functionality
- Message history storage in the database
- User-friendly interface built with HTML, CSS, and JavaScript
- Notifications for new messages

## Prerequisites

Before running the project, make sure you have the following installed:

- Python 3.x
- Django
- Channels (for WebSocket support)
- Redis (for WebSocket message handling)

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/django-chat-app.git
https://github.com/rachit0/Backend.git

```
use chat.html page which was in chat application and run it on server with /chat.html to see the running application
``` AWS Lambda function
1. AWS function to add two numbers and return result
import json

def lambda_handler(event, context):
    # Extract numbers from event
    num1 = event.get('num1', 0)
    num2 = event.get('num2', 0)
    
    # Add the numbers
    result = num1 + num2
    
    # Return the result as a response
    return {
        'statusCode': 200,
        'body': json.dumps({
            'result': result
        })
    }
```
2. AWS function to store document or pdf in s3 bucket

import json
import boto3
import base64
from botocore.exceptions import NoCredentialsError

s3_client = boto3.client('s3')

def lambda_handler(event, context):
    # Extract base64 encoded file content and metadata
    file_content_base64 = event['fileContent']  # This should be a base64 string of the file
    file_name = event['fileName']
    bucket_name = event['bucketName']
    
    try:
        # Decode the base64 content
        file_content = base64.b64decode(file_content_base64)
        
        # Upload the file to S3
        s3_client.put_object(
            Bucket=bucket_name,
            Key=file_name,
            Body=file_content,
            ContentType='application/pdf'  # Set the content type based on the file type
        )
        
        return {
            'statusCode': 200,
            'body': json.dumps({
                'message': f'File {file_name} uploaded successfully to {bucket_name}'
            })
        }
    
    except NoCredentialsError:
        return {
            'statusCode': 403,
            'body': json.dumps({'message': 'No valid AWS credentials found'})
        }
    except Exception as e:
        return {
            'statusCode': 500,
            'body': json.dumps({'message': str(e)})
        }



```



