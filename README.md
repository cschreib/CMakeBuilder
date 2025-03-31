# CMakeBuilder

Configure, build and test a CMake project right from within Sublime Text 3.

## Installation

Run the command

    Package Control: Install Package

and look for CMakeBuilder.

Version 1.0.1 and lower do not have server functionality. What follows is the
documentation for version 1.0.1 and lower.

## TL;DR

1. Open a `.sublime-project`.

2. Add this to the project file in your `"settings"`:

   ```javascript
   "CMakeBuilder":
   {
      "build_folder": "$folder/build"
   }
   ```

3. Run the command "CMakeBuilder: Configure" from the command palette.

4. Check out your new build system in your `.sublime-project`.

5. Press <kbd>CTRL</kbd> + <kbd>B</kbd> or <kbd>⌘</kbd> + <kbd>B</kbd>.

6. Hit <kbd>F4</kbd> to jump to errors and/or warnings.

See the example project below for more options.

## Settings

Please see the description of all settings in `CMakeBuilder.sublime-settings`.

Any of these settings can be changed in your project file, by adding an entry in

````json
{
    "settings":
    {
        "CMakeBuilder":
        {
        }
    }
}

Furthermore, any setting may be overridden by a platform-specific override.
The platform keys are one of `"linux"`, `"osx"` or `"windows"`. For an example
on how this works, see below.


## Example Project File

Here is an example Sublime project to get you started.

```json
{
    "folders":
    [
        {
            "path": "."
        }
    ],
    "settings":
    {
        "CMakeBuilder":
        {
            "build_folder": "$folder/build",
            "command_line_overrides":
            {
                "BUILD_SHARED_LIBS": true,
                "CMAKE_BUILD_TYPE": "Debug",
                "CMAKE_EXPORT_COMPILE_COMMANDS": true
            },
            "generator": "Unix Makefiles",
            "windows":
            {
                "generator": "Visual Studio 15 2017",
                "platform": "x64",
                "toolset": { "host": "x64" }
            }
        }
    }
}

````

### Available Scripting Commands

- `cmake_clear_cache`, arguments: `{ with_confirmation : bool }`.
- `cmake_configure`, arguments: `None`.
- `cmake_diagnose`, arguments: `None`.
- `cmake_open_build_folder`, arguments: `None`.

### Available Commands in the Command Palette

- `CMakeBuilder: Clear Cache`
- `CMakeBuilder: Configure`
- `CMakeBuilder: Diagnose`
- `CMakeBuilder: Browse Build Folder...`

All commands are accessible via both the command palette as well as the tools
menu at the top of the window.

### Clearing the cache

To force CMake files re-generation run

    CMakeBuilder: Clear Cache

and then run

    CMakeBuilder: Configure

### Diagnostics/Help

If you get stuck and don't know what to do, try running

    CMakeBuilder: Diagnose

### Tools Menu

All commands are also visible in the Tools menu under "CMakeBuilder".

![11][11] <!-- Screenshot #11 -->

### Running unit tests with CTest

If you have unit tests configured with the [add_test][2] function of CMake, then
you can run those with the "ctest" build variant.

### Using multiple cores with `make`

This package invokes `cmake --build` to build your targets. If you are using the
"Unix Makefiles" generator (`make`), and you want to use multiple cores, then
you have a few options:

- Don't use `make`, instead use `ninja`.
- Put `"env": {"CMAKE_BUILD_PARALLEL_LEVEL": 8}` as an environment variable in
  the `"cmake"` configuration.
- Export a `MAKEFLAGS` variable in your .bashrc.

### Syntax highlighting for various generators

There is syntax highlighting when building a target, and a suitable line regex
is set up for each generator so that you can press F4 to go to an error.

![9][9] <!-- Screenshot #9  -->
![10][10] <!-- Screenshot #10 -->
![12][12] <!-- Screenshot #12 -->

### List of Valid Variable Substitutions

This is a reference list for the valid variable substitutions for your
`.sublime-project` file.

- packages
- platform
- file
- file_path
- file_name
- file_base_name
- file_extension
- folder
- project
- project_path
- project_name
- project_base_name
- project_extension

[2]: https://cmake.org/cmake/help/latest/command/add_test.html
[9]: https://raw.githubusercontent.com/rwols/CMakeBuilder/screenshots/screenshots/9.png
[10]: https://raw.githubusercontent.com/rwols/CMakeBuilder/screenshots/screenshots/10.png
[11]: https://raw.githubusercontent.com/rwols/CMakeBuilder/screenshots/screenshots/11.png
[12]: https://raw.githubusercontent.com/rwols/CMakeBuilder/screenshots/screenshots/12.png
