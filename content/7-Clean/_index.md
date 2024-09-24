---
title : "Clean Up Resources"
date :  "`r Sys.Date()`" 
weight : 7
chapter : false
pre : " <b> 7. </b> "
---

Now that you have completed this tutorial, follow the steps below to delete AWS resources to avoid incurring unexpected costs.
Access the Amplify interface at [console.aws.amazon.com/amplify/apps](http://console.aws.amazon.com/amplify/apps)

**Step 1:**  Navigate to the root directory of your application and run the command below in your terminal.

```
amplify delete
```

**Step 2:** Assuming your application is named amplify4, open AWS Amplify, then select the amplify4 application, and choose View app.
![connect](/images/7.Clean/image1.png)

**Step 3:** Select App settings → General settings → Manage backends.
![connect](/images/7.Clean/image2.png)

**Step 4:** Select Actions at the top → choose delete app, and wait about 1 minute.
![connect](/images/7.Clean/image3.png)

## **Congratulations on successfully deleting the resources**