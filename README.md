#Process of the Project#
Here's a step-by-step breakdown of the processes described for setting up a CloudFormation stack, configuring an S3 bucket for static website hosting, setting up API Gateway, and deploying client-side code.

CloudFormation Stack
Go to the AWS Management Console and navigate to the CloudFormation service.
Click on Create stack.
Select Upload a template file, then click Choose file to upload a CloudFormation template in YAML format from your local drive.
Optionally, click View in Designer if you wish to visualize the AWS stack in the AWS CloudFormation Designer.
Click Next, fill out the stack details, and then continue following the prompts.
On the Review page, acknowledge any capabilities or IAM resource creations if prompted, then click Create stack.
The stack creation will begin, and you can monitor progress in the CloudFormation dashboard. Wait until the status changes to CREATE_COMPLETE.
S3 Bucket for Static Website Hosting
Navigate to the S3 service in the AWS Management Console.
Click Create bucket.
Name the bucket item-frontend-static-hosting and select an appropriate region. Make sure to uncheck Block all public access settings and acknowledge the warning that the bucket will be publicly accessible.
Enable Static website hosting in the bucket properties. Set index.html as the Index document.
Edit Bucket Policy: Insert the provided JSON policy code, making sure to replace items-frontend-static-hosting with your actual bucket name if different.
Edit CORS configuration: Insert the provided CORS configuration code to allow cross-origin requests.
API Gateway Configuration
Navigate to the API Gateway service in the AWS Management Console.
Find the API named items-api created as part of the CloudFormation stack.
Copy the Invoke URL; you'll need this for the frontend configuration.
Create a new Stage named prod.
Go to Integrations, create a new integration with the AWS Lambda function created as part of the CloudFormation stack.
Create 6 routes as specified (/items and /items/{id} with OPTIONS, GET, PUT, DELETE methods).
Attach the new integration to each of the 6 routes.
Configure CORS for all routes using the S3 bucket URL.
Deploy the API selecting prod as the stage.
Client-side Code
Ensure Node.js version 12.x is installed on your local machine.
Configure the Invoke URL's apiId in the frontend configuration file located at client/src/config.ts.
Open a command prompt, navigate to the client folder, and run npm install to install dependencies.
Run npm run build to create a production build.
Upload the build subfolder's content to the S3 bucket, maintaining the structure for static/css, static/js, and static/media.
After uploading, access the index.html in the S3 bucket's root to view the frontend application.
This process covers the setup from the backend infrastructure with CloudFormation and S3, through API Gateway configuration, to deploying the frontend application. Ensure each step is carefully followed and configurations are correctly applied, especially where public access and CORS settings are involved.
