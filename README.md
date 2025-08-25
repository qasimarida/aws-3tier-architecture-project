Project 2: Serverless Task Manager 🚀
This is a full-stack, serverless web application that allows users to create tasks. The project serves as a comprehensive demonstration of core AWS services and a practical example of a modern, cloud-native architecture.

🎯 Project Goal
The primary objective of this project is to create a secure, scalable, and highly available task management application without using any traditional servers. It showcases the ability to build a complete application using the AWS serverless ecosystem, from user authentication to data storage.

🛠️ Technologies Used
Frontend
HTML & CSS: The foundational structure and styling of the web page.

Tailwind CSS: A utility-first CSS framework for rapid and responsive UI development.

JavaScript: The logic for handling user authentication, form submissions, and API calls.

Amazon S3: Used for static website hosting, serving the index.html file to users.

Amazon CloudFront: A Content Delivery Network (CDN) used to securely deliver the website and improve performance.

Backend (Serverless)
Amazon Cognito: Manages user authentication, providing a secure hosted UI for user sign-in and a robust identity token to secure API access.

Amazon API Gateway: Acts as the "front door" to the backend, routing authenticated requests from the frontend to the appropriate Lambda function.

AWS Lambda: A serverless compute service that runs the backend logic for creating new tasks. It is invoked by API Gateway.

Amazon DynamoDB: A NoSQL database used to store the task data in a scalable and highly available manner.

🏗️ Architecture
The user's journey begins by accessing the static index.html file, which is hosted on Amazon S3 and delivered via CloudFront.

If the user is not authenticated, the JavaScript redirects them to the secure Cognito Hosted UI for sign-in.

Upon successful sign-in, Cognito redirects the user back to the application with a temporary authorization code. The JavaScript exchanges this code for an ID token.

The sign-in screen is then replaced with the Task Manager form.

When a user submits a new task, the JavaScript makes a secure POST request to the API Gateway endpoint.

API Gateway validates the request using the user's id_token and then invokes the Lambda function.

The Lambda function receives the task data and securely stores it in a DynamoDB table.

A success or failure message is returned to the webpage, providing real-time feedback to the user.

🏃 Getting Started
This project assumes you have an AWS account with the following services already configured:

S3 Bucket for static website hosting.

CloudFront Distribution pointing to your S3 bucket.

Cognito User Pool and an App Client.

API Gateway REST API with a POST method.

Lambda Function to handle API requests and write to a DynamoDB table.

DynamoDB Table to store the tasks.

To get the application up and running:

Clone this repository.

Open the index.html file and update the domain, clientId, and loginPageRedirect variables with your specific AWS resource details.

Upload the index.html file to your S3 bucket.

Access the website via your CloudFront URL to begin using the application!
