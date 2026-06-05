**Serverless Contact Form with AWS Lambda and DynamoDB**

This project demonstrates a serverless web application built using AWS Lambda, API Gateway, DynamoDB, and S3.
It serves an HTML contact form (contactus.html) and stores submitted form data into a DynamoDB table. After submission, users are redirected to a success page (success.html).
you can acess it here https://b4uipnm17d.execute-api.us-east-2.amazonaws.com/Dev

**🚀 Architecture**

Frontend:

contactus.html: Collects user details (first name, last name, email, phone number, etc.)

success.html: Displays a thank-you message after successful submission

Backend:

lambda_function.py: AWS Lambda function that serves HTML pages (via API Gateway) and writes form data into DynamoDB

Database:

Amazon DynamoDB: Stores form submissions with a unique primary key
⚙️ How it Works

A GET request to API Gateway (backed by Lambda) returns contactus.html.

User fills in details and clicks Submit.

A POST request is made with form data.

Lambda parses the form body and inserts the data into DynamoDB using PartiQL.

On success, Lambda returns success.html.

4. Configure API Gateway

Create a REST API in API Gateway.

Link GET and POST methods to the Lambda function.

Enable CORS for browser access.

5. Test

Open the API Gateway endpoint in your browser.

Fill in the form and click Submit.

Check DynamoDB to confirm that the record is saved.

**📷 Demo Screenshot**
<img width="700" height="900" alt="image" src="https://github.com/user-attachments/assets/359fc325-5f9e-4ac8-b32f-9eec866ad0e1" />
<img width="900" height="1000" alt="image" src="https://github.com/user-attachments/assets/8078c5f8-c286-48fa-9f87-2eaa3e96d437" />

**📧 Auto-Reply via DynamoDB Streams + SES**

We enabled DynamoDB Streams (New Image) on TejaswiniTable.

A second Lambda (ContactFormEmailAcker) is triggered on INSERT events.

It sends an acknowledgement email using Amazon SES (sender and region set via env vars).

SES in Sandbox requires verifying both sender/recipient emails; request production access to lift this.

Trigger uses event filter to process INSERTs only.

Logs & errors are visible in CloudWatch Logs. Optional SQS DLQ is configured for resilience.
