
# Customization: RobotArmHelix Update

You can **skip to [Usage](#usage)** if not interested in details of customization.

The RobotArmHelix project has been updated such that it can be built and run. The C# project file (`.csproj`) was changed to the new SDK-style to make changes easier. The project was upgraded to .NET Framework 4.8, which is supported and can easily be targeted on Windows computers. Source code has not been changed except for the part where robot models are locates. This part was modified to be more robust, and finds models through location of executable (motels are copied to the directory of executable during build process).

Instead of direcly referencing Helix Toolkit's DLLs (which needed to be generated and put to specific location), the project now references source projects from the source repository, which must be cloned at the specified relative location (scripts are provided that take care of this). The project currently works only with very old versions of Helix Toolkit (before 2018), which did not support any currently supported version of .NET or .NET Framework. Therefore, the Helix Toolkit sources are [cloned form a fork](https://github.com/ajgorhoe/helix-toolkit) which contains customization of these old versions on the branch `25_12_03_CustomizingOldCommitForRobotArm_7049fa`. This branch adapts the necessary projects from Helix toolkit such that they can be used by the RobotArmHelix project. Note that there is an issue with how Helix Toolkit projects are organized, because of which Helic Toolkit cannot be cloned in the same directory as the RobotArmHelix. Instead, the RobotArmHelix project must be cloned at one level deeper, in a separate directory, that contains copies of some files from Helix Toolkit.


The following components were used in this customization:

* customization of the [iglibmodules container repository](https://github.com/ajgorhoe/iglibmodules) on the branch `swrepos/GrLib/repoMain`
  * this also inclludes custoization of the [codedoc repository](https://github.com/ajgorhoe/IGLib.workspace.doc.codedoc) on the branch with the same name, which can be used for automatic generation of Doxygen code deocumentation
* a fork of the [Helix Toolkit](https://github.com/helix-toolkit/helix-toolkit), with a branch `00IGLib/25_12_03_CustomizingOldCommitForRobotArm_7049fa` created from an old commit compatible with the [RobotArmHelix]() project and customized such that it ues supported .NET framework and works with RobotArmHelix
* a fork of the RobotArmHelix project with a customization branch `https://github.com/Gabryxx7/RobotArmHelix` for upgrading the project and making it work

## Usage

* Clone the [iglibmodules container repository](https://github.com/ajgorhoe/iglibmodules) and checkout the branch `swrepos/GrLib/repoMain`
* Run the PowerShell script `GrLibUpdateRepoGroup_RobotArmHelix.ps1` that will clone individual components checked out at appropriate references (branches). Alternatively, you can run individual cloning scripts:

  * `GrLibUpdateRepo_HelixToolkitForRobotArm.ps1` - clones the `Helix Toolkit` repository used by RobotArmHelix and checks out the appropriate branch
  * `GrLibUpdateRepo_RobotArmHelix.ps1` - clones the RoboArmHelix project and checks out the appropriate customization branch
* Open the `RobotArmHelx` solution in Visual Studio, build it, and run the application. The solution is located at `RobotArmHelix\RobotArmHelix.sln`

If you want to do cloning **manually**, make sure to clone both repositories in the same directory, side by side:

* Clone the Helix Toolkit [from this fork](https://github.com/ajgorhoe/helix-toolkit) in the `helix-toolkit-forRobotArm` directory and switch to the `00IGLib/25_12_03_CustomizingOldCommitForRobotArm_7049fa` branch
* Clone the RobotArmHelix project [from this fork](https://github.com/ajgorhoe/RobotArmHelix) (or [from the original repo](https://github.com/Gabryxx7/RobotArmHelix), after changes are pulled in) in the `RobotArmHelix` directory and switch to the `swrepos/GrLib/repoMain` branch (or to the `master`branch, after changes are merged).
