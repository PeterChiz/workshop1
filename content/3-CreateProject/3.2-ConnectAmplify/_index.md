---
title : "Connect to AWS Amplify"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3.2 </b> "
---

**Step 1:** Navigate to the root directory of your application and provision the Amplify backend for the application by running the command below in your terminal. 

```
amplify init
```

**Step 2:** Enter a name for the Amplify project or accept the suggested name and press ***Enter*.**

```
? Enter a name for the project memorymatchgame
The following configuration will be applied:
Project information
| Name: memorymatchgame
| Environment: dev
| Default editor: Visual Studio Code
| App type: flutter
| Configuration file location: ./lib/
? Initialize the project with the above configuration? (Y/n)
```

For android studio user:
![connect](/images/3.CreateProject/image2.png)
**Step 3:** Press **Enter** again to accept the default settings and choose the AWS Authentication method. In this example, I am using the AWS configuration. The Amplify CLI will initialize the backend and connect the project to the cloud.
- For Visual Studio Code users:
![connect](/images/3.CreateProject/image3.png)
- The Amplify CLI will add a new folder named `amplify` to the root directory of your application, containing the Amplify project and backend details. It will also add a new dart file (amplifyconfiguration.dart) to the lib/ directory. The application will use this file to know how to access your provisioned backend resources when running.
![connect](/images/3.CreateProject/image4.png)
