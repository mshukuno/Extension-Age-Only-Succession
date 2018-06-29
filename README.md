# Extension-Age-Only-Succession

Changes to this extension are governed by the [**Repository Rules**](https://sites.google.com/site/landismodel/developers) from the Technical Advisory Committee.

Robert Scheller is the Custodian of this repository.

 <br><br>


# About

**Project:** LANDIS-II Landscape Change Model <br>
**Project Component:** Extension-Age-Only-Succession <br>
**Component Deposition:**	<https://github.com/LANDIS-II-Foundation/Extension-Age-Only-Succession> <br>
**Author:**			LANDIS-II Foundation <br>
**Origin Date:** 28 June 2018 <br>
**Final Date:**	28 June 2018 <br>


Welcome to the source code repository for Extension-Age-Only-Succession, a LANDIS-II succession extension.

Extension-Age-Only-Succession defines cohort succession as a function of cohort reproduction, cohort ageing, and cohort mortality. The onset of cohort reproduction requires three prior events:  
1.  a propagule must exist, either through seeding, resprouting, or planting; 
2. there must be adequate light; and  
3. the probability of species establishment must exceed a random number. Disturbance, seed dispersal, and amount of shade all affect cohort reproduction. Extension-Age-Only-Succession uses the seed dispersal algorithm described in the white paper provided on the LANDIS-II web site (www.landis-ii.org/documentation) by Ward et al. (2005).

<br><br>

# The Science and the Model


The science powering the LANDIS-II model ultimately resides in .cs files, written in 
the C# programming language. The collection of .cs files associated with the LANDIS-II 
Core Model or with any LANDIS-II extension is the so-called source code. Using the 
source code and the .NET Framework, the actual libraries (.dll files) and executables 
(.exe files) of the LANDIS-II model are constructed. The LANDIS-II model then uses 
various sets of libraries and executables to produce process-based output.

The .NET Framework provides the runtime environment needed for executing C# source code.
Executing C# source code means that the source code is compiled to produce an assembly, either 
a library (.dll file) or an executable (.exe file). The C# code in .cs files cannot be 
independently executed; the use of the .NET Framework is required because the C# programming 
language is so-called 'managed code'.

Integrated development environments (IDEs) are used to assist in compiling .cs files into 
assemblies. Visual Studio and MonoDevelop are two useful IDEs for the C# programming language.
To help with tracking the set of .cs files that are to be compiled, Visual Studio 
creates 'container' files called 'projects' and 'solutions'. A 'project' is the collection of 
source code files that the C# compiler will combine to produce a single output (an assembly). 
A Visual Studio project file is designated with a .csproj extension. A 'solution' is a set of 
one or more .csproj files.  A Visual Studio solution file is designated with a .sln extension.


The process of building 'the science' into 'the model' is done via a LANDIS-II extension.
The process looks like this:

* a set of .cs files is created or modified that translates process-based science into algorithms, and from the algorithms, into C# source code (script)
* a .csproj file is created that links the various .cs files together within an IDE
* the IDE takes the set of .cs files plus the .NET Framework and 'builds' the requisite assemblies: libraries (.dll files) and executables (.exe files). LANDIS-II extensions consist ONLY of libraries.
* the newly-built assemblies constitute 'the extension' and are packaged into a Windows-based installer (a Wizard)
* LANDIS-II users run the Wizard which installs the extension (a set of assemblies into the following directory: **_C:\Program Files\LANDIS-II-v7\extensions_**

<br><br>
# Preliminary notes for building a new or modified extension from source code


* It is recommended that you use Git for version control and change tracking. This means cloning the Extension-Base-Harvest repository to your local machine. Help with Git functionality can be found in the ProGit Manual (freely available) as a .pdf (https://git-scm.com/book/). A very straighforward Windows/Git interface is "git BASH" (available at https://git-for-windows.github.io/)

* Should you want the LANDiS-II Foundation to consider your changes for inclusion in the LANDIS-II Foundation's main GitHub repository https://github.com/LANDIS-II-Foundation/) you will need to submit a Pull request.

* Visual Studio (VS) may mark references to some libraries as "unavailable" until the solution is actually (re)built. During the build process, VS will automatically retrieve any requisite libraries (assmeblies) from the Support-Library-Dlls repository, located at https://github.com/LANDIS-II-Foundation/Support-Library-Dlls-v7.  Retrieval of requisite libraries is done by running the script, ~~"install-libs.cmd" as a pre-build event.~~ 

* ~~Libraries such as "System" and "System.Core" are assemblies that should be available on your machine as part of the .Net Framework. For example, examining "System" and "System.Core" in References (Solution Explorer ==> References) yields the following output in an Object Browser window in VS,~~

  * ~~Assembly System
    C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll~~

  * ~~Assembly System.Core
    C:\Program Files (x86) \ReferenceAssemblies\Microsoft\Framework\v3.5\System.Core.dll~~

<br><br>

# Step-by-step instructions for building a new or modified extension from source code


The following steps use both a Git command-line interface (GitBASH for Windows; see above) and the menu-driven options available in Visual Studio (VS). 

The example given below is a specific one and uses the extension,"Extension-Base-Harvest". The repo for this extension is available at  https://github.com/LANDIS-II-Foundation/Extension-Base-Harvest.


Substitute, as appropriate, for your extension of interest.

===== STEP1. Clone and .git track a local version of an extension repository ================

	a. Clone the extension repository (repo) of interest to your machine.
	a1. The COPY of the extension repo on your machine is the LOCAL repo;
	    the SOURCE of the cloned repo is the REMOTE repo

$ git clone https://github.com/LANDIS-II-Foundation/Extension-Base-Harvest.git
Cloning into 'Extension-Base-Harvest'...
remote: Counting objects: 429, done.
remote: Compressing objects: 100% (17/17), done.
remote: Total 429 (delta 6), reused 0 (delta 0), pack-reused 410
Receiving objects: 100% (429/429), 2.54 MiB | 1.09 MiB/s, done.
Resolving deltas: 100% (263/263), done.

$ git remote -v
origin  https://github.com/LANDIS-II-Foundation/Extension-Base-Harvest.git (fetch)
origin  https://github.com/LANDIS-II-Foundation/Extension-Base-Harvest.git (push)


==== STEP2. Setup Visual Studio (VS)  ==================================================

	a. Open VS and load the "base-harvest.csproj" file
Project ==> Open ==> Project/Solution



	b. Select the 'Solution Explorer' tab to see .cs files, References 
Solution 'base harvest' (1 project)
  C# base-harvest
    Prperties
    References
    EventsLog.cs
    InputParametersParser.cs
    MetadataHandler.cs
    packages.config
    PlugIn.cs
    SummaryLog.cs



	c. VS has added three (3) directories to your LOCAL repo:


...src\.vs\
...src\bin\		
...src\obj\


===== STEP3. (Re)build the project ==========================================================

	a. Under the "Build" tab, select "Build base-harvest"

	b. If the VS build is successful, two new files will have been created:

Landis.Extension.BaseHarvest-3.0.dll	#the functional extension to be used by the LANDIS-II
					Core-Model

Landis.Extension.BaseHarvest-3.0.pdb	#a program database(.pdb) file for storing debugging 
					information about the .dll; created from source files 
					during compilation and not needed by LANDIS-II


	b1. Note that "... \Extension-Base-Harvest\src\obj\Debug" has a text file listing the 
files created by the (re)build (see <name>.csproj.FileListAbsolute.txt)


	b2.  Note that "... \Extension-Base-Harvest\src\bin\Debug" is now populated with various 
reference libraries required for the (re)build. A copy of the newly built, 
"Landis.Extension.BaseHarvest-3.0.dll" library is also found here.



<br><br>
# Testing the (re)built extension (ie, "Landis.Extension.BaseHarvest-3.0.dll")


==== STEP1. remove the currently installed BaseHarvest extension and re-install =============================================== 

	a. Use the Windows 'Control Panel' to uninstall the current version of LANDIS-II Base Harvest
 
	b. Open 'Base Harvest v3.0.iss' in Inno Script Studio (https://www.kymoto.org/products/inno-script-studio)

	c. Compile (CTRL-F9) 'Base Harvest v3.0.iss' to produce an installer, 'LANDIS-II Base Harvest 3.0-setup.exe'

	d. Run the new installer 


===== STEP2. Perform a test run ===========================================================

	a. With LANDIS-II already installed, run LANDIS-II with the Base Harvest example provided with 
	   Extension-Base-Harvest (found in the folder, \Extension-Base-Harvest\deploy\examples OR 
	   after installation, found in the folder, \Program Files\LANDIS-II\v6\examples\Base Harvest)

	b. Open a command prompt (as administrator) and enter the following command at the command line, 
call landis-ii scenario_s1e1.txt

	c. The following console (screen) output, somewhat truncated from the actual output,
	   is expected:

C:\Program Files\LANDIS-II\v6\examples\Base Harvest>call landis-ii scenario_s1e1.txt
LANDIS-II 6.1 (official release)

<br><br>

# Getting started on Windows 10
<br>

## Prerequisites for LANDIS-II-v7 Extension development
 
* Visual Studio 2017 with installation of
  * .NET Core cross-platform development
  * NuGet Package Project for Visual Studio 2017
  * GitHub Extension for Visual Studio (optional)
  * PowerShell Tools for Visual Studio 2017 (optional)
* Inno Setup - required for creating a Windows installer
  * Install latest version from http://jrsoftware.org/isdl.php
<br><br>

## Setting up developing environment
#### Downloading the project <br> 
   ```git clone <download url> ``` <br>

#### Importing LANDIS-II dependencies <br> 
1. Open Windows PowerShell
2. ```cd <LANDIS-II Extensin folder>\src\lib``` <br>
3. Then type `su` and press `Tab` key. It will find **_support_libs_download.ps1_** file. <br>
4. Hit `Enter`

Notes:
  * LANDIS-II Core libralies are on [MyGet **_landis-ii-v7_** feed](https://www.myget.org/feed/Packages/landis-ii-v7)
  * LANDIS-II Support libraries are on [GitHub LANDIS-II-Foundation repository](https://github.com/LANDIS-II-Foundation/Support-Library-Dlls-v7)

<br>

## Creating an installer

1. Change `Configuration` from `Debug` to `Release` in Visual Studio and `Build` the extension application.  DLLs are created in **_src\bin\Release\netstandard2.0_** folder.
2. Go to  **_.\deploy_** folder.
3. Edit text file name and information.
4. Open `.iss` file.
4. Edit extension information and compile.









