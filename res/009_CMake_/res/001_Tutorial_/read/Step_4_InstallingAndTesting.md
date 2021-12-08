## [_CMAKE_][CMake] > **Step 4: Installing and Testing**

## <p align=center>[Step 1][stp1] | [Step 2][stp2] | [Step 3][stp3] | [Step 4][stp4] | [Step 5][stp5] | [Step 6][stp6] <br/> [Step 7][stp7] | [Step 8][stp8] | [Step 9][stp9] | [Step 10][stp10] | [Step 11][stp11] | [Step 12][stp12]  </p>

<!--
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
-->
[CMake]: ../../README.md
[stp1]: https://github.com/yoricsv/002_CppCMake/002_1_BasicStartingPoint.git
[stp2]: https://github.com/yoricsv/002_CppCMake/002_2_AddingLibrary.git
[stp3]: https://github.com/yoricsv/002_CppCMake/002_3_UsageReqForLib.git
[stp4]: https://github.com/yoricsv/002_CppCMake/002_4_InstallAndTest.git
[stp5]: https://github.com/yoricsv/002_CppCMake/002_5_SysIntrospection.git
[stp6]: https://github.com/yoricsv/002_CppCMake/002_6_ComFileGen.git
[stp7]: https://github.com/yoricsv/002_CppCMake/002_7_BuildInstall.git
[stp8]: https://github.com/yoricsv/002_CppCMake/002_8_Dashboard.git
[stp9]: https://github.com/yoricsv/002_CppCMake/002_9_StaticShared.git
[stp10]: https://github.com/yoricsv/002_CppCMake/002_10_GenExpression.git
[stp11]: https://github.com/yoricsv/002_CppCMake/002_11_ExportConfig.git
[stp12]: https://github.com/yoricsv/002_CppCMake/002_12_PackDebRel.git

---
<br/>
<!-- ---------------------------------- * Navigation * ---------------------------------- -->

# <p align = center><b>002_4_InstallAndTest<b></p>

Now we can start adding install rules and testing support to our project.

---
</br>

## Install Rules
The install rules are fairly simple: for **MathFunctions** we want to install the library and header file and for the application we want to install the executable and configured header.

So *to the end* of ***MathFunctions/CMakeLists.txt*** we add:

### MathFunctions/CMakeLists.txt
```cmake
install(
   TARGETS
      MathFunctions
   DESTINATION
      lib
)
install(
   FILES
      MathFunctions.h
   DESTINATION
      include
)
```

*And to the end* of the *top-level* **CMakeLists.txt** we add:

### CMakeLists.txt
```cmake
install(
   TARGETS
      Tutorial
   DESTINATION
      bin
)
install(
   FILES
      "${PROJECT_BINARY_DIR}/TutorialConfig.h"
   DESTINATION
      include
)
```

That is all that is needed to create a basic local install of the tutorial.

Now run the **cmake** executable or the **cmake-gui** to configure the project and then build it with your chosen build tool.

Then run the install step by using the **install** option of the **cmake** command (introduced in 3.15, older versions of CMake must use `make install`) from the command line. For multi-configuration tools, don't forget to use the `--config` argument to specify the configuration. If using an IDE, simply build the `INSTALL` target. This step will install the appropriate header files, libraries, and executables.
*For example*:

```bash
cmake --install .
```

The CMake variable `CMAKE_INSTALL_PREFIX` is used to determine the root of where the files will be installed. If using the `cmake --install` command, the installation prefix can be overridden via the `--prefix` argument.
*For example:*

```bash
cmake --install . --prefix "/home/myuser/installdir"
```

Navigate to the install directory and verify that the installed Tutorial runs.

---
</br>

## Testing Support
Next let's test our application. At the end of the *top-level* ***CMakeLists.txt*** file we can enable testing and then add a number of basic tests to verify that the application is working correctly.

### CMakeLists.txt
```cmake
enable_testing()

# does the application run
add_test(
   NAME
      Runs
   COMMAND
      Tutorial 25
)

# does the usage message work?
add_test(
   NAME
      Usage
   COMMAND
      Tutorial
)
set_tests_properties(
      Usage
   PROPERTIES
      PASS_REGULAR_EXPRESSION
         "Usage:.*number"
)

# define a function to simplify adding tests
function(
   do_test
      target arg
         result
)
   add_test(
      NAME
         Comp${arg}
      COMMAND
         ${target}
         ${arg}
   )
   set_tests_properties(
         Comp${arg}
      PROPERTIES
         PASS_REGULAR_EXPRESSION
            ${result}
   )
endfunction()

# do a bunch of result based tests
do_test(
   Tutorial 4
      "4 is 2"
)
do_test(
   Tutorial 9
      "9 is 3"
)
do_test(
   Tutorial 5
      "5 is 2.236"
)
do_test(
   Tutorial 7
      "7 is 2.645"
)
do_test(
   Tutorial 25
      "25 is 5"
)
do_test(
   Tutorial -25
      "-25 is (-nan|nan|0)"
)
do_test(
   Tutorial 0.0001
      "0.0001 is 0.01"
)
```

The first test simply verifies that the application runs, does not segfault or otherwise crash, and has a zero return value. This is the basic form of a CTest test.

The next test makes use of the `PASS_REGULAR_EXPRESSION` test property to verify that the output of the test contains certain strings. In this case, verifying that the usage message is printed when an incorrect number of arguments are provided.

Lastly, we have a function called **do_test** that runs the application and verifies that the computed square root is correct for given input. For each invocation of **do_test**, another test is added to the project with a name, input, and expected results based on the passed arguments.

Rebuild the application and then cd to the binary directory and run the **ctest** executable: `ctest -N` and `ctest -VV`. For multi-config generators (e.g. Visual Studio), the configuration type must be specified with the `-C <mode>` flag. For example, to run tests in Debug mode use `ctest -C Debug -VV` from the binary directory (not the Debug subdirectory!). Release mode would be executed from the same location but with a `-C Release`. Alternatively, build the `RUN_TESTS` target from the IDE.

---