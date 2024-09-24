---
title : "View information about registered users through Amplify Auth on the AWS Console"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 4.4 </b> "
---

{{% notice info %}}
You need to access the Amazon Cognito service because Amplify Auth uses Cognito as its backend.
{{% /notice %}}

Here are the steps you can follow:

1. Log in to the AWS Console (console.aws.amazon.com).
2. Find and select the “Cognito” service from the list of services.
3. Select “Manage User Pools”.
4. Find and select the User Pool corresponding to your Amplify application.
![connect](/images/4.AddAuth/image5.png)

1. In the left menu, select the “User pool name” you created earlier.
2. Here, you will see a list of all registered users.
![connect](/images/4.AddAuth/image6.png)
