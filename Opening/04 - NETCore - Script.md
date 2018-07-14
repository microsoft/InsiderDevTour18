# WinForms on .NET Core 3 Demo 

## Setup

- VS 2017 15.7 with .NET Desktop Development, ASP.NET and Web Development workloads 
- Also requires optional .NET Framework 4.7.1 SDK and .NET Framework 4.7.1 targeting pack in Visual Studio 2017. Plus the .NET Core 2.1 SDK: https://www.microsoft.com/net/download/dotnet-core/sdk-2.1.300
- Sample Code: Grab the sample from Teams [here](TBD)
- Copy solution to c\demos\netcore
- Prep c\source with a lot of folders and lots of files inside. Example, copy program files 86 \microsoft sdk to source\
- Go to \builddemos\build\telerik and ensure all files are 'unlocked'
- Right now the publish is set to “MY DESKTOP”, you will need to right click on PieSample.core, select Publish, select configure and change Target Location to your desktop. 
 
## Demo
1.	Open **buildDemos.sln** 
2.	Show that we have **two versions** of the same application. pieSample the **.NET Framework** version and pieSample.core the **.NET Core** version. 
3.	**Right click on pieSample.core**, Edit **piSample.core.csproj**. Show that the project is **referencing .NET Core 2.1**, show that it references **System.WindowsForms** and show that it references a **pre-existing Telerik control** (we did not have to rebuild this control, existing controls just work out of the box) 
4.	CoreFX the BCL that .NET Core runs on has taken tons of updates from the community and from us that we can’t do in .NET Framework for compatibility reasons. Since .NET Core is side by side we can take these updates in .NET Core. Because of this .NET Core is faster than .NET Framework. 
5.	**Right click on pieSample**, select **Set As Startup Project**, Debug | **Start Without Debugging**. Point this to a **folder** on the disk. Press **run**. See the pie chart and note **how fast it ran in the lower right**. 
6.	**Right click on pieSample.core**, select** Set As Startup Project**, Debug | **Start Without Debugging**. Point this to the same folder on the disk. Press run. See the pie chart and note it runs much faster than the .NET Framework version. 
7.	Click the “?” icon which will show which assemblies the application loaded, you can see it referencing .NET Core here. 
8.	**Right click on pieSample.Core**, Select **Publish**. Note that we can use linkers to take the .NET Core, WinForms and Telerik and link the application into a single .EXE which does not require anything to be installed on the machine. **Click Publish** and it will deploy a simple .EXE onto the desktop.  
9.	**Right click on the .exe**, see it is **66MB**, our linker tech is early and we know we can make it much smaller. For fun you can copy this to a memory stick and it will run on any machine in the audience. 
