---
title : "Add Amplify API to the Application"
date :  "`r Sys.Date()`" 
weight : 5
chapter : false
pre : " <b> 5.1 </b> "
---

**Step 1:** Navigate to the root directory of your application and provision the Amplify API resources by running the command below in your terminal.

```
amplify add api
```

**Step 2:** Select the GraphQL option and press **Enter**. Update the suggested settings as below. Scroll to the **Authorization modes** option and change it to **Amazon Cognito User Pool**. Select **No** for the additional authentication type prompt. Choose the **Continue** option. For the GraphQL API, select **Conflict detection: Disabled**, then choose **yes**. For the default resolution strategy, select **Auto Merge**, then choose **Continue**. Select the **Blank Schema** template and press **Enter**. Select **No** to the schema editing prompt. 
![connect](/images/5.AddAmplifyAPI/image1.png)

The Amplify CLI will add a new directory for the API, which contains the `schema.graphql` file where you will define the models for your application.
![connect](/images/5.AddAmplifyAPI/image2.png)

**Step 3:** Open the *schema.graphql* file and replace its contents with the following to define the session model.
```
type Trip @model @auth(rules: [{ allow: owner }]) {
    id: ID!
    tripName: String!
    destination: String!
    startDate: AWSDate!
    endDate: AWSDate!
    tripImageUrl: String
    tripImageKey: String
}
```