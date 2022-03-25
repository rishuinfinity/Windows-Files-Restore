# Windows-Files-Restore
Restore temporary cache files upon next login, preferably for use at IITD CSC systems

There are situations in public systems{ CSC systems in my case}, where you lose all temporary data like browser history and login data or even apps which you might have installed with user privileges upon logout.

One solution for browser history which everyone uses is that they sign in to their browser account and sync afterwards.

My solution is to create a backup of said temporary files into someplace in your allocated space and restore ir everytime you login.

Pros of this method: You dont need to sign in to browser everytime and your passwords remain saved. Your dont need to install your temporary apps again and again.

Cons: You might have to use some extra space as you are just duplicating the files of those apps. Also, restoring the files depends on the number of files available and can take about 1-2 minutes.

## How to do it
* As present in the examples present in this readme, I recommend creating two files namely "Update.cmd" and "Setup.cmd"
* Update.cmd : Updates the backup data stored in your backup folder (preferably run before logging out)
* Setup.cmd  : Restores the backup data (run just after logging out)
* Now as of the contents of those files check the folders you want to backup and where you want to backup them to:
  Let's say the folder we want to backup has the path "pathA"
  And the place we want to backup it  to has the path "pathB"
  
  Update.cmd
  ```
  :: This line is a comment
  ROBOCOPY "{{pathA}}" "{{pathB}}" /MIR  /W:0 /E /R:1
  ```
  Setup.cmd
  ```
  :: Make sure to restore the files to exactly the same location where they were before
  ROBOCOPY "{{pathB}}" "{{pathA}}" /W:0 /E /R:1
  ```
  
### Here let's have an example (Microsoft edge)
  Microsoft edge allows installation as a user. Upon speculation I found that Edge stores its files in three separate folders{Edge, EdgeCore and EdgeUpdate}. So, here are my configurations.
  
  Update.cmd
  ```
  :: This line moves Microsoft Edge folder
  ROBOCOPY "C:\Users\mt618xxxx\AppData\Local\Microsoft\Edge " "Y:\Windows\My Applications\Microsoft\Edge " /MIR  /W:0 /E /R:1

  ROBOCOPY "C:\Users\mt618xxxx\AppData\Local\Microsoft\EdgeCore " "Y:\Windows\My Applications\Microsoft\EdgeCore " /MIR /W:0 /E /R:1

  ROBOCOPY "C:\Users\mt618xxxx\AppData\Local\Microsoft\EdgeUpdate " "Y:\Windows\My Applications\Microsoft\EdgeUpdate " /MIR /W:0 /E /R:1
  ```

  Setup.cmd
  ```
  :: This line moves Microsoft Edge folder
  ROBOCOPY "Y:\Windows\My Applications\Microsoft\ " "C:\Users\mt618xxxx\AppData\Local\Microsoft\ " /W:0 /E /R:1
  ```

### Let's have another example (Whatsapp)
  The Whatsapp app (i.e. Whatsapp.exe) also allows installation as a user.
  
  Update.cmd
  ```
  :: This line moves Whatsapp folder
  ROBOCOPY "C:\Users\mt618xxxx\AppData\Local\Whatsapp " "Y:\Windows\My Applications\Whatsapp " /MIR /W:0 /E /R:1
  ```

  Setup.cmd
  ```
  :: This line moves Whatsapp Edge folder
  ROBOCOPY "Y:\Windows\My Applications\Whatsapp " "C:\Users\mt618xxxx\AppData\Local\Whatsapp " /W:0 /E /R:1
  ```

Other apps that work (that I know of) : Firefox
