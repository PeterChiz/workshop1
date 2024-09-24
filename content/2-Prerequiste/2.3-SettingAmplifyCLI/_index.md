---
title : "Creating an IAM user"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

**Installing Amplify CLI**
- Install cURL if you haven’t from the official website.
- Run the following commands to install the Amplify CLI
- Mac and Linux:

```
curl -sL https://aws-amplify.github.io/amplify-cli/install | bash && $SHELL
```

  - Windows:
```
curl -sL https://aws-amplify.github.io/amplify-cli/install-win -o install.cmd && install.cmd
```

**Configure Amplify**
- The Amplify CLI requires an IAM user with appropriate policy permissions to interact with your AWS account. This command will guide you through creating a new user in your AWS account and storing the user profile credentials in your local environment. Future commands run with the CLI will use these credentials to perform actions that require amplify configure.

```
amplify configure
```
- *amplify configure* will prompt you to log in to the AWS Console.

- After logging in, the Amplify CLI will prompt you to create an IAM user. Choose your desired region and follow the instructions.

```
Specify the AWS Region
? region:  # Your preferred region
Follow the instructions at
https://docs.amplify.aws/cli/start/install/#configure-the-amplify-cli

to complete the user creation in the AWS console
https://console.aws.amazon.com/iamv2/home#/users/create
```

**Create an IAM User**

- Navigate to the [ IAM User Creation Page ](https://console.aws.amazon.com/iamv2/home#/users/create) if it is not already open.

- Enter a username and select **Next**. You can name the user anything, but I will call it `amplify-dev`.
![connect](/images/2.Prerequiste/image8.png)

- Select **Attach policies directly** and choose **AdministratorAccess-Amplify** as the Permissions policy. Select **Next**.
![connect](/images/2.Prerequiste/image9.png)

- On the **Review**, page, check that everything looks good and select **Create user**.
![connect](/images/2.Prerequiste/image10.png)

- This will redirect to the user list page. Select the user you just created.
![connect](/images/2.Prerequiste/image11.png)

- On the user details page, navigate to the **Security credentials** tab, scroll down to **Access keys** and select **Create access keys**.
![connect](/images/2.Prerequiste/image12.png)

- On the next page, select **Command Line Interface**, acknowledge the warning, and select **Next**.
![connect](/images/2.Prerequiste/image13.png)

- On the next page, select **Create access key**.
![connect](/images/2.Prerequiste/image14.png)

- You will then see a page with the access keys for the user. Use the copy icon to copy these values to your clipboard, select the **Done**,  button, and then return to the Amplify CLI.
![connect](/images/2.Prerequiste/image15.png)


## **Enter Access Key and Secret Access Key**

- Enter the values you just copied into the corresponding CLI prompts. Use  `AmplifyWorkshop` as the profile name.

```
Enter the access key of the newly created user:
? accessKeyId:  # YOUR_ACCESS_KEY_ID
? secretAccessKey:  # YOUR_SECRET_ACCESS_KEY
This would update/create the AWS Profile in your local machine
? Profile Name:  # (default)

Successfully set up the new user.
```


  
