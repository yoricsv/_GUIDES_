## [_GUIDES_][guides] > [Windows][win]  > 3. SYSTEM SOFTWARE > 2. SERVICES > **PowerShell**

### <p align=center>[Git & GitHub][git] | [Windows][win] | [Linux][linux] | [Networks][nets] <br/> [Programming][progLang] | [Databases][db] | [Docker & Kubernetes][docker] | [Embedded systems][embSys] | [CMake][CMake] </p>

<!--
* [_GUIDES_][guides]
* [Git & GitHub][git]
* [Windows][win]
* [Linux][linux] (Unix)
* [Networks][nets]
* [Programming Languages][progLang]
* [Databases][db]
* [Docker & Kubernetes][docker]
* [Embedded systems][embSys]
* [CMake][CMake]
-->

[guides]:   ../../../../../../README.md
[git]:      ../../../../../001_Git_and_GitHub_/Git_And_GitHub.md
[win]:      ../../../../Windows.md
[linux]:    ../../../../../003_Linux_(Unix)_/Linux_(Unix).md
[nets]:     ../../../../../004_Networks_/Networks.md
[progLang]: ../../../../../005_Programming_languages_/Programming.md
[db]:       ../../../../../006_Databases_/Databases.md
[docker]:   ../../../../../007_Docker_and_Kubernetes_/Docker_and_Kubernates.md
[embSys]:   ../../../../../008_Embedded_systems_/Embedded_systems.md
[CMake]:    ../../../../../009_CMake_/CMake_Tutorial.md

---
<!-- ---------------------------------- * Navigation * ---------------------------------- -->

# <p align=center><b>PowerShell</b></p>

### CONTENTS:

* [Environment Variables][EnvVari]
* Comandlets
* Scripts

### Create a System Environment Variable in PowerShell

1. Run the CommandPrompt `[Win]+[R]` -> Type: *`pwsh`* -> `[Shift]+[Ctrl]+[Enter]` (to get admin rights)
2. Type the following command:

```bash
[Environment]::SetEnvironmentVariable("<variable_name>", "<variable_value>" ,"Machine")
```

3. Substitute "`<variable_name>`" with the actual name of the variable you want to create.
4. Substitute "`<variable_value>`" with the value you want to assign to your variable.
The last parameter of the SetEnvironmentVariable call tells it to register the given variable as a system variable.

<!--
* [Environment Variables][EnvVari]
-->

[EnvVari]: ../../3_EnvironmentVariables_/read/EnvironmentVariables.md

---