## [_GUIDES_][guides] > [_CMake_][CMake] > **Step 8: Adding Support for a Testing Dashboard**

## <p align=center>[Step 1][stp1] | [Step 2][stp2] | [Step 3][stp3] | [Step 4][stp4] | [Step 5][stp5] | [Step 6][stp6] <br/> [Step 7][stp7] | [Step 8][stp8] | [Step 9][stp9] | [Step 10][stp10] | [Step 11][stp11] | [Step 12][stp12]  </p>

<!--
* [_GUIDES_][guides]
* [_CMAKE_][CMake]
* [Step 1][stp1]
* [Step 2][stp2]
* [Step 3][stp3]
* [Step 4][stp4]
* [Step 5][stp5]
* [Step 6][stp6]
* [Step 7][stp7]
* [Step 8][stp8]
* [Step 9][stp9]
* [Step 10][stp10]
* [Step 11][stp11]
* [Step 12][stp12]

_GUIDES_/res/009_CMake_/res/001_Tutorial_/read
_GUIDES_/../../../../..
-->

[guides]: ../../../../../README.md
[CMake]:  ../../../CMake_Tutorial.md
[stp1]:   Step_1_BasicStartingPoint.md
[stp2]:   Step_2_AddingLibrary.md
[stp3]:   Step_3_AddingUsageRequirementsforLibrary.md
[stp4]:   Step_4_InstallingAndTesting.md
[stp5]:   Step_5_AddingSystemIntrospection.md
[stp6]:   Step_6_AddingCustomCommandAndGeneratedFile.md
[stp7]:   Step_7_PackagingAndInstaller.md
[stp8]:   Step_8_AddingSupportForTestingDashboard.md
[stp9]:   Step_9_SelectingStaticOrSharedLibraries.md
[stp10]:  Step_10_AddingGeneratorExpressions.md
[stp11]:  Step_11_AddingExportConfiguration.md
[stp12]:  Step_12_PackagingDebugAndRelease.md

---

<!-- ---------------------------------- * Navigation * ---------------------------------- -->

# <p align = center><b>002_8_Dashboard<b></p>

Adding support for submitting our test results to a dashboard is simple. We already defined a number of tests for our project in **Testing Support**. Now we just have to run those tests and submit them to a dashboard. To include support for dashboards we include the CTest module in our *top-level* ***CMakeLists.txt***.

Replace:

### CMakeLists.txt
```cmake
# enable testing
enable_testing()
```

With:

### CMakeLists.txt
```cmake
# enable dashboard scripting
include(CTest)
```

The CTest module will automatically call `enable_testing()`, so we can remove it from our CMake files.

We will also need to acquire a ***CTestConfig.cmake*** file to be placed in the top-level directory where we can specify information to CTest about the project. It contains:

* The project name
* The project "Nightly" start time
  * The time when a 24 hour "day" starts for this project.
* The URL of the CDash instance where the submission's generated documents will be sent

One has been provided for you in this directory. It would normally be downloaded from the **Settings** page of the project on the CDash instance that will host and display the test results. Once downloaded from CDash, the file should not be modified locally.

### CTestConfig.cmake
```cmake
   set(CTEST_PROJECT_NAME
         "CMakeTutorial"
   )
   set(CTEST_NIGHTLY_START_TIME
         "00:00:00 EST"
   )

   set(CTEST_DROP_METHOD
         "http"
   )
   set(CTEST_DROP_SITE
         "my.cdash.org"
   )
   set(CTEST_DROP_LOCATION
         "/submit.php?project=CMakeTutorial"
   )
   set(CTEST_DROP_SITE_CDASH
         TRUE
   )
```

The **ctest** executable will read in this file when it runs. To create a simple dashboard you can run the **cmake** executable or the **cmake-gui** to configure the project, but do not build it yet. Instead, change directory to the binary tree, and then run:

```bash
ctest [-VV] -D Experimental
```

Remember, for multi-config generators (e.g. Visual Studio), the configuration type must be specified:

```bash
ctest [-VV] -C Debug -D Experimental
```

Or, from an IDE, build the *Experimental* target.

The **ctest** executable will build and test the project and submit the results to Kitware's public dashboard: https://my.cdash.org/index.php?project=CMakeTutorial.

---