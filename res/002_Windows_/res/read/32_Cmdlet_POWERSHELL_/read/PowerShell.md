## [_GUIDES_][1] > [Windows][3] > 3. SYSTEM SOFTWARE > 2. SERVICES > **PowerShell**

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

# <p align=center><b>PowerShell</b></p>

## CONTENTS:
* [Environment Variables][10]
* Comandlets
* Scripts

## Create a System Environment Variable in PowerShell
1. Run the CommandPrompt `[Win]+[R]` -> Type: *`pwsh`* -> `[Shift]+[Ctrl]+[Enter]` (to get admin rights)
2. Type the following command:

```bash
[Environment]::SetEnvironmentVariable("<variable_name>", "<variable_value>" ,"Machine")
```
3. Substitute "`<variable_name>`" with the actual name of the variable you want to create.
4. Substitute "`<variable_value>`" with the value you want to assign to your variable.
The last parameter of the SetEnvironmentVariable call tells it to register the given variable as a system variable.

<!--
* [Environment Variables][10]
-->

[10]: ../../3_EnvironmentVariables_/read/EnvironmentVariables.md


<!--Done!--> 

---
<br/>