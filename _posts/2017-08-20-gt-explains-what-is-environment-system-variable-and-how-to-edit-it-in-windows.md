---
title: "GT Explains: What is Environment System Variable and How to Edit it in Windows"
date: "2017-08-20"
categories: 
  - "thu-thuat-chung"
---

Whenever I write content related to [Android rooting and ADB access](http://www.guidingtech.com/15008/adb-control-keypress-broken-android-keys/ "How to Use ADB to Control Keypress events on Android"), I often ask readers to add a specific path to **Windows System Environment variable** so that they can execute the command globally. However, most of the users seem to be having trouble understanding what setting up the environment variable path actually means and the way to edit it in Windows to include the path.

Today I am going to show you how you can edit Environment Variable in Windows but before we see that, let’s understand what it really means.

## What Environment Variable Means

Environment Variable is only significant if you are [working on Windows Command prompt](http://www.guidingtech.com/12909/brilliant-command-prompt-cmd-tricks/ "10 Brilliant Command Prompt (CMD) Tricks You Probably Don’t Know About"). Let me state an example for better understanding. Suppose you type in the command _ipconfig_ to find out the [IP configuration of your computer](http://www.guidingtech.com/12170/automate-ip-switching-dns-network-profile-change-windows/ "How to Automate IP Switching, DNS Change and Network Profile Change in Windows"). No matter in which folder you are in the Command Prompt, Windows will recognize the command and automatically run it. However, if you try to execute any executable file in a folder without actually navigating to the folder, Windows will not be able to recognize the command.

![adb not recognised](/assets/images/adb-not-recognised.png "adb not recognised")

It’s not that Windows has a soft corner for the ipconfig command, but the path where the ipconfig command is located in the system, i.e. system32 is configured in Windows Environment Variable by default. So the point is, if you want to run any file on Command Prompt, no matter which folder you are in you will have to set up the Environment Variable Path for it.

So let us now see how we can set up an Environment Variable in Windows to include the path of a folder.

## Setting Windows Environment Folder

**Step 1:** Open Windows Explorer and navigate to _Computer_. Here, click on the _System properties_ button to open your computer System properties.

![system properties](/assets/images/system-properties.png "system properties")

**Step 2:** After the Windows System Properties open up, click on the link _Advanced System Settings_ on the left sidebar.

![adv sys settings](/assets/images/adv-sys-settings.png "adv sys settings")

**Step 3:** In Advanced System Properties click on the button _Environment Variable_ to open Environment Variable.

![edit environment variable](/assets/images/edit-environment-variable.png "edit environment variable")

**Step 4:** Under user variable, double click on _PATH_ to open it. You can now add the path of the folder in the text box. Use a semicolon (;) to merge two or more paths.

![environment variable](/assets/images/environment-variable.png "environment variable")

Finally press the OK Button to save the settings and close all the windows. You can now access the executable files from the configured path globally on Command Prompt.

![adb command now recognised](/assets/images/adb-command-now-recognised.png "adb command now recognised")

## Conclusion

That was how you can edit and include a custom path to Windows Environment Variable in Windows to execute a file throughout the Command Prompt. I have tried my best to put it in as easy way as possible, still if you have questions you would like me to clear, all you need to do is drop a comment.

Nguon: guidingtech.com
