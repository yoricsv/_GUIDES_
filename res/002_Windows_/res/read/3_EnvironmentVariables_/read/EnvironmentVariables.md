## [_GUIDES_][1] > [Windows][3]  > 3. SYS. SOFTWARE > **Environment Variables**

## <p align=center>[Git & GitHub][2] | [Windows][3] | [Linux][4] | [Networks][5] <br/> [Programming][6] | [Databases][7] | [Docker & Kubernetes][8] | [Embedded systems][9] </p>

<!--
* [_GUIDES_][1]
* [Git & GitHub][2]
* [Windows][3]
* [Linux][4]
* [Networks][5]
* [Programming][6]
* [Databases][7]
* [Docker & Kubernetes][8]
* [Embedded systems][9]
-->

[1]: ../../../../../../README.md
[2]: ../../../../../001_Git_and_GitHub_/Git_And_GitHub.md
[3]: ../../../../Windows.md
[4]: ../../../../../003_Linux_(Unix)_/Linux_(Unix).md
[5]: ../../../../../004_Networks_/Networks.md
[6]: ../../../../../005_Programming_languages_/Programming.md
[7]: ../../../../../006_Databases_/Databases.md
[8]: ../../../../../007_Docker_and_Kubernetes_/Docker_and_Kubernates.md
[9]: ../../../../../008_Embedded_systems_/Embedded_systems.md

--- 
<br/>
<!-- ---------------------------------- * Navigation * ---------------------------------- -->

# <p align=center>System & User Environment Variables in Windows 10 explained</p>

## CONTENTS:
* Environment Variables
* System and User Environment Variables
* Add and modify Environment Variables *(GUI)*
   * Using the Path variable
   * Dynamic Environment Variables
* List of all Environment Variables
* Create a User Environment Variable in:
   * [Command Prompt (cmd)][10]
   * [PowerShell][11]


**Environment Variables** has always been a complex topic of discussion for day-to-day **Windows OS** users. Environment Variable is formed up by two separate words, **'Environment'** and **'Variable'**. The'variable' can store a value and vary from computer to computer. Windows provide an *'Environment'* for applications to execute and perform operations and that is what makes the first word. Combining both, Environment Variables are those dynamic objects that store the values provided by the environment. Now environment provides values that help other programs in obtaining some crucial information about the system. Like there is an environment variable called *'windir'* that corresponds to the directory where Windows is installed. To see this in action, open up an explorer window and type in **'%windir%'** in the address bar. The Windows installation folder will open up.

Very similarly, you can make reference to the Windows directory using *'windir'* variable in other programs and scripts. There are numerous other variables that can be accessed:
* *'TEMP'* or *'TMP'* is the variable that points to the directory where all temporary files are stored. 
* The *'Path'* variable is the one that points to the directories containing executable files. So that you can run a program from the Command Prompt in any other directory. 
These variables come in handy when you are developing something or using the shell a lot.

## System & User Environment Variables
Very similar to how the Registry works on Windows, we have System and User Environment Variables.
* The **system variables** are system-wide accepted and don't vary from user to user.
* **User Environments** are configured differently from user to user. You can add your variables under the user so that other users aren't affected by them.

**System Variables** are evaluated before **User Variables**. So if there are some user variables with the same name as system variables then user variables will be considered.
The Path variable is generated in a different way. The effective Path will be the User Path variable appended to the System Path variable.

## Add and modify Environment Variables
A small warning before we go deeper. Create a system restore point, and try not to tamper with the existing settings configured for your system. Until unless you are very sure about your actions. To open the *'Environment Variables'* Window, follow these steps:

1. Right-click *'This PC'* icon and select *'Properties'*.
2. In this window select *'Advanced System Settings'* from the left part.
3. Hit the last button saying *'Environment Variables'* to open our destined window.

![System Properties][12]

Once you've opened this up, you will be able to view User and System variables separately. The variable name is in the first column and its value in the second. The corresponding buttons below the table let you *'Add'*, *'Edit'* and *'Delete'* these variables.

### Using the Path variable
Path is the most used environment variable. It points to directories that contain executable files. Once you've correctly setup your Path variable, you can use these executables from anywhere in the system.<br/>
Open up the environment variables window and look for *'Path'* in system variables.

![System variables path][13]

Now to run your application, open up Command Prompt and type in the name of the executable file that was in the folder. You can provide additional arguments if the program supports it. The program will run from the command prompt without actually being in the directory from where you executed the command. That is the beauty of the **Path variable**.

### Dynamic Environment Variables
Unlike, conventional variables, dynamic environment variables are provided by the CMD and not by the system. You cannot change the values of these variables and they expand to various discrete values whenever queried. We usually use these variables for batch processing and these aren't stored in the environment. Even the *'SET'* command will not reveal these variables. Some of the dynamic environment variables are listed below.

## List of all Environment Variables
Open command prompt and type **'SET'** and hit Enter. The entire list of variables with their current values will be displayed and you can refer to it for making changes to your computer.

To get a list of the all variables might save it into the file .txt.
1. Run the CommandPrompt `[Win]+[R]` -> Type: *`cmd`* -> `[Shift]+[Ctrl]+[Enter]` (to get admin rights)
2. Use next command to save a list of variables into the file envar.txt on desctop:

```bash
set > %homepath%\desktop\envar.txt
```

Variable Name | Value
---: | :---
**%APPDATA%** | `C:\Users\<username>\AppData\Roaming`
**%ALLUSERSPROFILE%** | `C:\ProgramData`
**%CD%** | *Typing in this command will give you the current directory you are working in.*
**%COMMONPROGRAMFILES%** | `C:\Program Files\Common Files`
**%COMMONPROGRAMFILES(x86)%** |  `C:\Program Files (x86)\Common Files`
**%COMMONPRGRAMW6432%** | `C:\Program Files\Common Files`
**%CMDEXTVERSION%** | *This variable expands to the version of the command-line extensions.*
**%COMSPEC%** | `C:\Windows\System32\cmd.exe`
**%DATE%:** | *This variable will give you the current date according to date format preferences.*
**%ERRORLEVEL%** | *Determines the error level set by last executing command.*
**%HOMEDRIVE%** | `C:\`
**%HOMEPATH%** | `C:\Users\<username>`
**%LOCALAPPDATA%** | `C:\Users\<username>\AppData\Local`
**%LOGONSERVER%** | `\\<domain_logon_server>`
**%PATH%** | `C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem`
**%PATHEXT%** | `.com;.exe;.bat;.cmd;.vbs;.vbe;.js;.jse;.wsf;.wsh;.msc`
**%PROGRAMDATA%** | `C:\ProgramData`
**%PROGRAMFILES%** | `C:\Program Files`
**%PROGRAMW6432%** | `C:\Program Files`
**%PROGRAMFILES(X86)%** | `C:\Program Files (x86)`
**%PROMPT%** | `$P$G`
**%SYSTEMDRIVE%** | `C:`
**%SYSTEMROOT%** | `C:\Windows`
**%TIME%** | *Similarly, it gives you current time according to the time format preferences.*
**%TMP%** | `C:\Users\<username>\AppData\Local\Temp`
**%TEMP%** | `C:\Users\<username>\AppData\Local\Temp`
**%USERNAME%** | <username>
**%USERPROFILE%** | `C:\Users\<username>`
**%USERDOMAIN%** | *Userdomain associated with current user.*
**%USERDOMAIN_ROAMINGPROFILE%** | *Userdomain associated with roaming profile.*
**%WINDIR%** | `C:\Windows`
**%PUBLIC%** | `C:\Users\Public`
**%PSMODULEPATH%** | `%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules\`
**%ONEDRIVE%** | `C:\Users\<username>\OneDrive`
**%DRVERDATA%** | `C:\Windows\System32\Drivers\DriverData`
**%CMDCMDLINE%** | *Outputs command line used to launch the current Command Prompt session. (Command Prompt.)*
**%COMPUTERNAME%** | *Outputs the system name.*
**%PROCESSOR_REVISION%** | *Outputs processor revision.*
**%PROCESSOR_IDENTIFIER%** | *Outputs processor identifier.*
**%PROCESSOR_LEVEL%** | *Outputs processor level.*
**%RANDOM%** | *This variable prints a random number from 0 through 32767*
**%NUMBER_OF_PROCESSORS%** | *Outputs the number of physical and virtual cores.*
**%OS%** | *Windows_NT*

This was pretty much about System and User Environment Variables on Windows. Windows does come with a lot more variables – don't forget to check them using the *'SET'* command.

TIP: [Rapid Environment Editor][14] is a powerful Environment Variables Editor for Windows (Download from official [RapidEE_v.9.2_build_937_win10_x64.zip][15] (2,319Kb): zip archive to use it as a portable application)

## Create a User Environment Variable in:
* [Command Prompt (cmd)][10]
* [PowerShell][11]
<!--
* [Command Prompt (cmd)][10]
* [PowerShell][11]
* ![System Properties][12]
* ![System variables path][13]
* [Rapid Environment Editor][14]
* [RapidEE_v.9.2_build_937_win10_x64.zip][15]
-->

[10]: ../../32_Cmd_PROMPT_/read/CommandPrompt_commands.md
[11]: ../../32_Cmdlet_POWERSHELL_/read/PowerShell.md
[12]: ../img/ZeExG.png
[13]: ../img/path-EnvVariables.png
[14]: https://www.rapidee.com/en/environment-variables
[15]: https://www.rapidee.com/download/RapidEEx64.zip

<!--Done!--> 

---
<br/>
