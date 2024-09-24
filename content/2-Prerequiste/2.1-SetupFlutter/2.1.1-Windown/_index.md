---
title : "For Windows"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 2.1.1 </b> "
---

**Dowloading Flutter SDK**

- Download the zip file from the [Trang web Flutter.](https://docs.flutter.dev/get-started/install/windows#get-the-flutter-sdk)
- Extract the Flutter SDK to a folder named *development* on your Desktop.
{{% notice note %}}
The folder path above is just a recommendation, and this reference will be used throughout the workshop. You can also move it to any other folder. Just make sure to keep track of where your Flutter folder is extracted.
{{% /notice %}}

> 

**Add Flutter to Path**

- Go to the extracted Flutter folder and copy its path.
- You can copy it by right-clicking on the folder and selecting the “Copy as Path” option or by clicking on the navigation bar at the top of the window and copying the path text from there.
![connect](/images/2.Prerequiste/image1.png)

- Click on the Windows icon in the bottom left corner and search for **Environment Variables**. Select **Edit Environment variables for your account.**
![connect](/images/2.Prerequiste/image2.png)

- This will open a window with the **Advanced** tab selected in **System Properties**. Click the **Environment Variables**… button.
![connect](/images/2.Prerequiste/image3.png)

- In the window that opens, under **System variables**, find **Path** and double-click on it.
![connect](/images/2.Prerequiste/image4.png)

- Add a new entry by clicking the **New** button on the right and pasting the path you copied earlier.
![connect](/images/2.Prerequiste/image5.png)

- Save and close all windows.
- Close any Command Prompt windows.
- Then open a new Command Prompt and write the following command to check:
flutter doctor
```