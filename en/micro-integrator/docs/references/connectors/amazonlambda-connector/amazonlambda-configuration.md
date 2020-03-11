# Amazon Lambda Configuration

The AmazonLambda Connector allows you to access the REST API of [Amazon Web Service Lambda (AWS Lambda)](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html), which lets you run code without provisioning or managing servers. With Lambda, you can run code for virtually any type of application or backend service - all with zero administration. Just upload your code in one of the languages that AWS Lambda supports (currently Node.js, Java, C#, Go, and Python) and Lambda takes care of everything required to run and scale your code with high availability. You can set up your code to automatically trigger from other AWS services or call it directly from any web or mobile app. You pay only for the compute time you consume - there is no charge when your code is not running.

To use the AmazonLambda service, you must have an AWS account. If you don't already have an account, you are prompted to create one when you sign up. You're not charged for any AWS services that you sign up for unless you use them.

## Signing Up for AWS

* **To sign up for AWS:**

    1. Navigate to [Amazon AWS website](https://aws.amazon.com/), and then select **Create an AWS Account**.

        > **Note**: If you previously signed in to the AWS Management Console using AWS account root user credentials, select **Sign in to a different account**. If you previously signed in to the console using IAM credentials, choose Sign-in using root account credentials. Then select **Create a new AWS account**.

    2. Follow the online instructions.

Part of the sign-up procedure involves receiving a phone call and entering a verification code using the phone keypad. AWS will notify you by email when your account is active and available for you to use.

## Obtaining user credentials

You can access the Amazon Lambda service using the root user credentials but these credentials allow full access to all resources in the account as you cannot restrict permission for root user credentials. If you want to restrict certain resources and allow controlled access to AWS services then you can create IAM (Identity and Access Management) users in your AWS account for that scenario.
* **Follow the steps below to get an AWS Access Key for your AWS root account:**

  1. Go to the AWS Management Console.
     
     <img src="/assets/img/connectors/aws-management-console.png" title="AWS Management Console" width="800" alt="AWS Management Console"/>
  
  2. Hover over your company name in the right top menu and click "My Security Credentials".

     <img src="/assets/img/connectors/my-security-credentials.png" title="My security credentials" width="800" alt="My security credentials"/>
  
  3. Scroll to the "Access Keys" section.
  
     <img src="/assets/img/connectors/create-accesskey-using-root-account.png" title="Create accesskey using root account" width="800" alt="Create accesskey using root account"/>
  
  4. Click on "Create New Access Key".
  5. Copy both the Access Key ID (YOUR_AMAZON_LAMBDA_KEY) and Secret Access Key (YOUR_AMAZON_LAMBDA_SECRET).

* **Follow the steps below to get an AWS Access Key for an IAM user account:**

  1. Sign in to the AWS Management Console and open the IAM console.

     <img src="/assets/img/connectors/iam.png" title="IAM" width="800" alt="IAM"/>
  
  2. In the navigation pane, choose Users.

     <img src="/assets/img/connectors/iam-users.png" title="IAM users" width="800" alt="IAM users"/>
     
  3. Add a checkmark next to the name of the desired user, and then choose User Actions from the top.
  4. Click on Manage Access Keys.
  
     <img src="/assets/img/connectors/security-credentials.png" title="Security credentials" width="800" alt="Security credentials"/>
  
  5. Click on Create Access Key.
        
     <img src="/assets/img/connectors/create-access-key-using-iam.png" title="Create access key using IAM" width="800" alt="Create access key using IAM"/>
     
  6. Click on Show User Security Credentials. Copy and paste the Access Key ID and Secret Access Key values, or click on Download Credentials to download the credentials in a CSV (file).
     
     <img src="/assets/img/connectors/download-access-key.png" title="Download access key" width="800" alt="Download access key"/>
  
## Create Amazon S3 Bucket

  1. Navigate to the created **AWS** account.
  2. Click **Services** tab on left top of the tab.
  
     <img src="/assets/img/connectors/amazon-services.png" title="Select amazon services" width="800" alt="Select amazon services"/>
  
  3. Select **Storage** section and click **S3**.
  
     <img src="/assets/img/connectors/amazon-s3-create-bucket-sample-1.png" title="Select S3 services" width="800" alt="Select S3 services"/>

  4. Create a bucket.
  
     <img src="/assets/img/connectors/amazon-s3-create-bucket-sample-2.png" title="Create S3 bucket" width="800" alt="Create S3 bucket"/>
       
## Create Deployment Package

  Your function's code consists of scripts or compiled programs and their dependencies. When you author functions in the Lambda console or a toolkit, the client creates a ZIP archive of your code called a [ deployment package ](https://docs.aws.amazon.com/lambda/latest/dg/deployment-package-v2.html). 
  
  This sample explains how to create a sample python program as deployment package.
   
  1. Create sample Python function (e.g., lambda_function.py) file. (On Linux and macOS, use your preferred shell and package manager. On Windows 10, you can [install the Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) to get a Windows-integrated version of Ubuntu and Bash).
  2. Create a ZIP archive.
     ```
     ~/my-function$ zip function.zip lambda_function.py
       
     adding: lambda_function.py (deflated 17%)
     ```
  3. Upload the ZIP archive you created into the S3 bucket that you created.
   
     <img src="/assets/img/connectors/upload-deployement-file.png" title="Upload deployment package" width="800" alt="Upload deployment package"/>
   
## Create Execution Role
    
You can use AWS Identity and Access Management (IAM) to manage access to the Lambda API and resources like functions and layers. For users and applications in your account that use Lambda, you manage permissions in a permissions policy that you can apply to IAM users, groups, or roles. To grant permissions to other accounts or AWS services that use your Lambda resources, you use a policy that applies to the resource itself.
   
Creating an [Execution Role](https://docs.aws.amazon.com/lambda/latest/dg/lambda-permissions.html#lambda-intro-execution-role) in the IAM Console.

   1. Open the [roles page](https://console.aws.amazon.com/iam/home#/roles) in the IAM console.
      
      <img src="/assets/img/connectors/create-iam-roles.png" title="Create IAM roles" width="800" alt="Create IAM roles"/>
      
   2. Choose Create role.
   3. Under Common use cases, choose Lambda.
   4. Choose Next: Permissions.
   5. Under Attach permissions policies, choose the AWSLambdaBasicExecutionRole and AWSXrayWriteOnlyAccess managed policies.
   6. Choose Next: Tags.
   7. Choose Next: Review.
   8. For Role name, enter lambda-role.(Please copy and save the created role and role name to configure the connector) 
   7. Choose Create role.