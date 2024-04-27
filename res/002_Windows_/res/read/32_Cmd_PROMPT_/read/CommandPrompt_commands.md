# [GUIDES](../../../../../../README.md) > [Windows](../../../../Windows.md)  > 3. SYS. SOFTWARE > 2. SERVICES > __Command Prompt (*CMD*)__

<!-- ### <p align=center>[Git & GitHub][git] | [Windows][win] | [Linux][linux] | [Networks][nets] <br/> [Programming][progLang] | [Databases][db] | [Docker & Kubernetes][docker] | [Embedded systems][embSys] | [CMake][CMake] </p> -->

## __List of Guides__

| Guide Name                    |   |  Guide Name                   |   | Guide Name                    |
|-------------------------------|---|-------------------------------|---|-------------------------------|
| [Windows][navWin]             | * | [Linux][navNix]               | * | [Networks][navNet]            |
| [Databases][navDBs]           | * | [Programming][navPLn]         | * | [Git & GitHub][navGit]        |
| [CMake][navCMk]               | * | [Docker & Kubernetes][navDkr] | * | [Embedded systems][navEmS]    |

[navGit]:   ./../../../../../001_Git_and_GitHub_/Git_And_GitHub.md
[navWin]:   ./../../../../Windows.md
[navNix]:   ./../../../../../003_Linux_(Unix)_/Linux_(Unix).md
[navNet]:   ./../../../../../004_Networks_/Networks.md
[navPLn]:   ./../../../../../005_Programming_languages_/Programming.md
[navDBs]:   ./../../../../../006_Databases_/Databases.md
[navDkr]:   ./../../../../../007_Docker_and_Kubernetes_/Docker_and_Kubernates.md
[navEmS]:   ./../../../../../008_Embedded_systems_/Embedded_systems.md
[navCMk]:   ./../../../../../009_CMake_/CMake_Tutorial.md

---
<!-- ---------------------------------- * Navigation * ---------------------------------- -->

<!-- # <p align=center><b>Command Prompt (CMD) Commands</b> <i>(Chaet sheet)</i></p> -->

### CONTENTS

- [Environment Variables][EnvVari]
- Comandlets
- Scripts

## __Create a User Environment Variable in Command Prompt (cmd)__

1. Run the CommandPrompt `[Win]+[R]` -> Type: *`cmd`* -> `[Shift]+[Ctrl]+[Enter]` (to get admin rights)
2. Type the following command:

   ```bash
   setx /M <variable_name> "<variable_value>"
   ```

3. Substitute "`<variable_name>`" with the actual name of the variable you want to create.
4. Substitute "`<variable_value>`" with the value you want to assign to your variable.

The `/M` switch makes the setx command create a system variable.

[EnvVari]: ../../3_EnvironmentVariables_/read/EnvironmentVariables.md
