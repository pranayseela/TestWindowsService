# TestWindowsService
Sample Simple Windows Service
What a Windows Service is

Enables you to create long-running executable applications that run in their own windows session.
Can be automatically started when the computer boots, can be paused and restarted without any user interaction.
Easily installable by running the command line utility InstallUtil.exe and passing the path to the service's executable file.
Why a Windows Service?

One of the most common requirements of some businesses is long-running scheduled jobs based on some time interval. For example: sending a newsletter everyday afternoon or send an email alert to the customer for every one hour.

So building a Windows Service could be one of the reliable solutions to do the goal that can do the required job in the behind the scenes without interfering others users on the same computer.

Introduction

This article explains a step-by-step process of developing and installing a Windows Service to do a scheduled job based on a time interval.

Open Visual Studio and from the menus select "File" -> "New" -> "Project...".

A New Project window will open. Choose "Visual C#" >> "Windows" project type and select "Windows Service" from the right hand side and name the project "TestWindowsService" as shown in the following screenshot.

new project window

After you click "OK", the project will be created and you will see the design view of the service as shown in the following screen. Right-click the "Service1.cs" file in Solution Explorer and rename it "to" Scheduler or any other name that you want to give it. Then click “click here to switch to code view”.

code view

In the code view, you can see two methods called OnStart() and OnStop(). The OnStart() triggers when the Windows Service starts and the OnStop() triggers when the service stops.

OnStop triggers 
Right-click the TestWindowService project, add a new class and name it "Library.cs". This class will be useful to create the methods that we require in the project. If your TestWindowService is a big project, you can create a ClassLibrary project and reference it to your TestWindowService.

new class 

Library.cs

Make the class public and declare it as a Static class.

Static class

Create a log method (WriteErrorLog) to log the exceptions.

log method 

Create one more log method (WriteErrorLog) to log the custom messages.

log method to log 

Scheduler.cs

Now return to our Scheduler.cs file and declare a Timer.

Timer

Write the following code in the OnStart() method and timer1_Tick():

timer1_Tick

Write the following code in the OnStop() method:

OnStop method
Scheduler.cs [Design]

Now return to the Scheduler.cs [Design] and right-click on the editor window then click "Add Installer".

Add Installer

Then you can see that there will be a new file called "ProjectInstaller.cs" as shown in the following.

new file called ProjectInstaller

Installer

Right-click on the "serviceInstaller1" and click "Properties".
 
Properties

Change the ServiceName to "Test Windows Service" (or your own name) and StartType to "Manual" (or you can choose "Automatic" if you need this service to be automatic).

Test Windows Service 

Right-click the serviceProcessInstaller1, go to the properties window and change "Account" to "LocalSystem".
 
change Account property

Build the project to see the .exe file at the location where you created the solution.

Build the project 

That's all. Your Windows Service is all ready to install in your machine.

Installing the Windows Service

Go to "Start" >> "All Programs" >> "Microsoft Visual Studio 2012" >> "Visual Studio Tools" then click "Developer Command Prompt for VS2012".

Type the following command:

cd <physical location of your TestWindowService.exe file>

in my case it is :

cd C:\Sandbox\WindowServices\TestWindowService\TestWindowService\bin\Debug
 
Installing the Window Service 
 
Next type the following command:

InstallUtil.exe “TestWindowService.exe”

and press Enter.

TestWindowService
