# Linux DotNet Core Setup Guide

## Introduction
This solution is just to demonstrate how to set up a solution within a Linux OS using
a console app project, library project and a test project. 


## Assumptions
* You have a Linux OS installed and know how to convert apt commands to apt-get or yum
or to pacman commands.


## Set Up
1. Please follow the guide to install DotNet on a Linux OS on the
 [dotnet getting started](https://www.microsoft.com/net/learn/get-started/linuxredhat).
2. Get a code editor, personally I use Visual Studio code, but Atom is easier to install on Linux Distributions. Download [VS Code from here](https://code.visualstudio.com/). Run the bellow command.
```
cd /fullPathToDownloadLocation/
sudo dpkg -i code-[VersionNumber]_AMD64.deb
```
3. Install Git, no point working on code without using Version Control. Just incase 
you make mistakes.
```
sudo apt install git
```
4.  Make a folder for the solution
```
cd /PathToParentFolder/
git init
mkdir LinuxDotNetCore
cd LinuxDotNetCore
dotnet new sln
dotnet new nugetconfig
```
5. Make a folder for your Console
```
mkdir CoreConsole
cd CoreConsole
dotnet new console
cd ..
dotnet sln add ./CoreConsole/CoreConsole.csproj
```
6. Make a folder for your Library
```
mkdir CoreLibrary
cd CoreLibrary
dotnet new library
cd ..
dotnet sln add ./CoreLibrary/CoreLibrary.csproj
```
7. Make a Folder for your Unit Tests
```
mkdir CoreTests
cd CoreTests
dotnet new mstest
cd ..
dotnet sln add ./CoreTests/CoreTests.csproj
```
8. Make a reference from your Console project to your Library project to allow execution.
```
cd CoreConsole
dotnet add reference ../CoreLibrary/CoreLibrary.csproj
cd ..
``` 
9. Add a reference from your Tests project to your Libary project to allow testing.
```
cd CoreTests
dotnet add reference ../CoreLibrary/CoreLibrary.csproj
cd ..
```
10. Make sure everything is working.
```
dotnet restore
dotnet build
dotnet test
dotnet publish
dotnet run --project ./CoreConsole/CoreConsole.csproj
dotnet ./CoreConsole/bin/Debug/netcoreapp2.0/CoreConsole.dll
```

_NB: You might encounter an issue with the tests, there seemes to be a problem with the 
Microsoft dotnet core 2.0 packages not being made public for nuget. If you look at my
[nuget.config file](./nuget.config), you will notice 3 additional keys which are the latest 
repos for the MS nuget packages for dotnet core not dotnet core 2.0_ 

### That is a full set up for a Console App in dotnet core, but applies to most applications.

#### Now just to save.
```
git status
git add ./**
git status
git commit -m "Basic set up of dotnet core app."
```