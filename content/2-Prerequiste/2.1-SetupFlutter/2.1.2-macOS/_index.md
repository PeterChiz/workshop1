---
title : "For mac OS"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 2.1.2 </b> "
---

**Download Flutter SDK**

- Download the zip file from the [Flutter.](https://docs.flutter.dev/get-started/install/macos#get-sdk) *flutter_macOS_<-version-number->.zipflutter_macos_arm64_<-version-number->.zip*
    
Make sure to download the correct Flutter release package for your Mac’s chip. Download the file for Intel-based laptops or the file for Apple Silicon.
    
- Extract the Flutter SDK into a folder named development on your Desktop.
    
{{% notice note %}}
The folder path above is just a recommendation and will be referenced throughout the workshop. You can also move it to any other folder. Just make sure to keep track of where your Flutter folder is extracted.
{{% /notice %}}

**Add Flutter to Path**

- Go to the extracted Flutter folder and copy its path:
    - You can copy it by right-clicking on the Flutter folder and selecting the “Get Info” option. This will open a window with folder information. In the General tab, check the Where information. Select all the text and copy it.
- Open the terminal and write the following command to determine your terminal type:
![connect](/images/2.Prerequiste/image6.png)
![connect](/images/2.Prerequiste/image7.png)

```
 echo $SHELL
```

- If you are using Bash, write:
```
open ~/.bash_profile # or open ~/.bashrc
```

- If you are using Z shell, write:

```
open ~/.zshrc
```

- Paste the following content into the file as a new line:

```
 export PATH="$PATH:[PATH_OF_FLUTTER]/flutter/bin"
```

- Close all terminals and open a new terminal.
- Then open a new Terminal and write the following command to check:

```
flutter doctor
```

