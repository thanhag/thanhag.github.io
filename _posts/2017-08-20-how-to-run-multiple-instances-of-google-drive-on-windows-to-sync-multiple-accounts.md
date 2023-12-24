---
published: False
title: "How to Run Multiple Instances of Google Drive on Windows to Sync Multiple Accounts"
date: "2017-08-20"
categories: 
  - "thu-thuat-chung"
---

Working on multiple [Google Drive accounts](http://www.guidingtech.com/11069/introduction-google-drive-things-you-can-do-with-it/ "An Introduction to Google Drive and Things You Can Do With it") on the browser is very simple. Once can simply use the Google account switcher and [work on multiple accounts in parallel](http://www.guidingtech.com/14812/manage-dropbox-skydrive-windows-8-online-backup/ "Manage Multiple Online Backup Accounts (Dropbox, SkyDrive) in Windows 8 Modern UI"). Unfortunately, when using the Windows application for the same, there is no such feature.

**IMPORTANT UPDATE:** This is an old post and many people recently started reporting in the comments that this method no longer works because the Google Drive app was updated to exclude this feature. Hence we’ve written another post that uses a different method. Here it is -> [How to Use and Sync More Than One Google Drive Account on Windows](http://www.guidingtech.com/27321/run-sync-more-than-one-google-drive/ "http://www.guidingtech.com/27321/run-sync-more-than-one-google-drive/").

![multiple Google drive](/assets/images/multiple-Google-drive.png "multiple Google drive")

According to [Google Support](http://support.google.com/drive/bin/answer.py?hl=en&answer=2375023 "Switch between multiple Google Drive accounts "), once must use application preferences and sign out from the first Google account before using another. But that’s not a solution if you want to sync more than one account and use them in parallel.

Fret not, like always, we’ve got your back. Here’s a method to get it done and run multiple Google Drive instances on the same machine.

## Multiple Google Drive Instances

**Step 1:** Close all instances of Google Drive running on your computer and then download and [install this application](http://v2.nonxt6.c.pack.google.com/edgedl/drive/1.0.2891.6813/gsync.msi "Gsync MSI"). After the application is installed, add C:\\Program Files (x86)\\Google\\Drive to your Windows Environment Variable. You can refer to [this article](http://www.guidingtech.com/16728/what-is-environment-system-variable-edit-windows/ "GT Explains: What is Environment System Variable and How to Edit it in Windows") to see how it’s done.

**Step 2:** Having done that, open Notepad and copy paste the following line. Don’t forget to replace username@ domain.com with your Google username.

> @ECHO OFF SET USERNAME=username@ domain.com SET USERPROFILE=%~dp0%USERNAME% SET USERPROFILE=%~dp0%USERNAME% MD “%USERPROFILE%\\AppData\\Roaming”>nul MD “%USERPROFILE%\\AppData\\Local\\Application Data”>nul MD “%USERPROFILE%\\Application Data”>nul MD “%USERPROFILE%\\Local Settings\\Application Data”>nul MD “%USERPROFILE%\\My Documents”>nul MD “%USERPROFILE%\\Documents”>nul START googledrivesync

![batch file](/assets/images/batch-file.png "batch file")

Save the file as Account 1.bat to your desktop or another folder where you would like to sync the files. Don’t forget to select _All Files_ as type in Notepad while saving the batch file.

**Step 3:** Now run the batch file and wait for another instance of Google Drive to Start. The second instance of the application will ask you to sign in to a new account. Proceed normally, just remember to change the sync folder to the new folder that’s created using the batch files in the advanced option.

![sign in](/assets/images/sign-in.png "sign in")

![advanced settings](/assets/images/advanced-settings.png "advanced settings")

**Note:** Sometimes you might encounter some difficulty while changing the folder. In such a case, copy the exact path of the folder to select the directory.

![browse for folders](/assets/images/browse-for-folders.png "browse for folders")

That’s all, you will now see two instances of Google Drive syncing side by side. Amazing, right? The next time you want to sync files on the secondary account, run the batch file of that particular account. To add every subsequent account, just make a new batch file, run it and configure the application.

## Conclusion

As we are not using any third-party application for the trick, this is the best method to sync multiple Google Drive accounts in Windows according to me. However, I think this is one of the very basic feature that should be provided as a built-in feature by Google. What do you think?
