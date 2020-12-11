# Visual Studio Code

Our code editor of choice in this course is Microsoft's Visual Studio Code.

This is an open source cross-platform code editor built with Javascript.  
Don't confuse this with Microsoft's other product _Visual Studio_ which is designed
to only program for the Windows platform. Visual Studio Code (or VSCode) is a
multi-language editor that can handle almost any programming language for any
platform.

Go to website for [Visual Studio Code][vs-code], then
download and install VS Code.

You'll want to make sure you download the Stable release.

## macOS

Download the DMG (Disk Image) file for VSCode and open it up. This will mount
as virtual 'disk' on your desktop. Drag the VSCode icon to your Applications
folder and then eject the virtual disk on the Desktop by dragging it to the Trash.

In macOS the command line utility `code` isn't instaled by default when you install
VSCode.

Open the VS Code editor, open the Command Palette (`Cmd+Shift+P`) and type
type `shell command` to find the `Shell Command: Install 'code' command in PATH`
command.

This will now allow you to easily open files in VS Code from the terminal using
the `code` command followed by a file or directory.

## Windows

In Windows we will be using VSCode alongside WSL (Windows Subsystem for Linux)

In order to do this, we must make sure we install this VSCode extension:

[Remote: WSL by Microsoft][wsl-extension]

Once you've installed this you can open VSCode and connect to your WSL instance.

Make sure you read this tutorial from Microsoft on how to use WSL and VSCode together:

[Remote Development in WSL](https://code.visualstudio.com/docs/remote/wsl-tutorial)

## Ubuntu

To install VSCode in Ubuntu Linux, download the 64-bit .deb file to your Downloads
folder, the open that folder in your File Manager and double click on it to
install it.

[wsl-extension]:https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl
[vs-code]:https://code.visualstudio.com/