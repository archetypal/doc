Introduction
============
This documentation has been revised per the 2.6.3 version of [git](https://git-scm.com/).

Windows Installation
====================
When installing on Windows, the following defaults are generally used:

Destination
-----------
Accept the default destination under AppData

Components
----------
Accept defaults (Windows Explorer integration, associations).  If using TortoiseGIT, the
git GUI is unnecessary.

Start Menu
----------
Don't create a Start Menu folder.

Adjusting Path
--------------
Use Git form the Windows Command Prompt.  While all documentation for Archetypal assumes usage of Bash,
Visual Studio Code needs this option.

SSH
---
Use OpenSSH.  All documentation for Archetypal assumes usage of OpenSSH.

Line Endings
------------
Checkout Windows-style, commit Unix-style line endings.

Terminal Emulator
-----------------
Use Windows' default console window

Experimental Performance
------------------------
Currently not using Enable file system caching.


Windows Bash
============
Because bash is used so often, it can be helpful to create a shortcut to load bash.  To do so,
find the git-bash.exe in the %userprofile%\AppDataLocal\Programs\Git.  Right click and select Pin to Start.
Find the shortcut on the start menu and find the shortcut location.  Adjust the properties and

Windows TortoiseGIT
===================
[TortoiseGIT](https://tortoisegit.org/) is a nice windows shell extension.