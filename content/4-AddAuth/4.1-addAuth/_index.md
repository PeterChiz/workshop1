---
title : "Add the Amplify authentication category to the application"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 4.1 </b> "
---

**Step 1:** Navigate to the root directory of your application and run the command below in your terminal.

```
amplify add auth
```

**Step 2:** Select the **Default configuration** option and then choose **Email** as the login method. Then select the **No, I am done** option.

```
Using service: Cognito, provided by: awscloudformation
 The current configured provider is Amazon Cognito. 
 Do you want to use the default authentication and security configuration? Default configuration
 Warning: you will not be able to edit these selections. 
 How do you want users to be able to sign in? Email
 Do you want to configure advanced settings? No, I am done.
✅ Successfully added auth resource memorymatchgame28e6d925 locally

✅ Some next steps:
"amplify push" will build all your local backend resources and provision it in the cloud
"amplify publish" will build all your local backend and frontend resources (if you have hosting category added) and provision it in the cloud
```

**Step 3:** Now the Amplify Auth category is ready. Run the `amplify push` command to create the resources in the cloud.
![connect](/images/3.CreateProject/image5.png)

**Step 4:** Press Enter. The Amplify CLI will deploy the authentication resources and display a confirmation, as shown in the screenshot.
![connect](/images/3.CreateProject/image6.png)
