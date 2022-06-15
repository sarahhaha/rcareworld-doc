# RFUniverse Dependency
We use [RFUniverse](https://wenqiangx.github.io/robotflowproject/project/rfuniverse/) to construct Unity side and to communicate with Python side. 
Since RFUnivese has not been made public, please reach out to Cathy (ry273@cornell.edu) to get full Unity code for RFUniverse.

# Install
There are two ways of using RCareWorld. 
## With provided assets
Download Unity exectuable file [Windows] [Ubuntu]

Install pyrfuniverse module. 
```
cd pyrfuniverse
conda create -n rcare python=3.8
conda activate rcare
pip install -r requirements.txt
pip install -e .
```
Use the editor

For Windows, `./Player.exe -edit`. For Ubuntu, `./Player.x86_64 -edit`

## With custom assets
### Install PyRfuniverse
Install pyrfuniverse module. 
```
cd pyrfuniverse
conda create -n rcare python=3.8
conda activate rcare
pip install -r requirements.txt
pip install -e .
```
### Install Unity
RCareWorld currently works with Unity 2022.1.3f1c1. Please install this version of Unity Editor.
There might be errors (for instance, no URDF-Importer), just ignore it and continue.
### Import RCareWorld Project into Unity
The whole project can be downloaded from Google Drive, please contact the development team to have access to the codebase of Unity.
You need to get the paid assets from Unity Asset Store to get Unity side working. We provide an asset list for you to purchase.
### Install URDF Importer
1. Open the Package Manager from Unity Menu. Click `Window -> Package Manager`. A new package manager window will appear.

2. Click on the `+` sign on the top left corner of the package manager window and click on `Add Package from Git URL`. 

3. Enter the git URL for the URDF Importer with the latest version tag (currently v0.5.2) `https://github.com/Unity-Technologies/URDF-Importer.git?path=/com.unity.robotics.urdf-importer#v0.5.2` in the text box and press `Enter`.

4. Click `Import URDF`.
### Install Unity Robotics Hub (Optional)
1. Open `Window` -> `Package Manager`.

1. In the Package Manager window, find and click the `+` button in the upper lefthand corner of the window. Select `Add package from git URL...`.


1. Enter the git URL for the package. Note: you can append a version tag to the end of the git url, like `#v0.4.0` or `#v0.5.0`, to declare a specific package version, or exclude the tag to get the latest from the package's `main` branch.
   1. For the [ROS-TCP-Connector](https://github.com/Unity-Technologies/ROS-TCP-Connector), enter `https://github.com/Unity-Technologies/ROS-TCP-Connector.git?path=/com.unity.robotics.ros-tcp-connector`.

1. Click `Add`.

To install from a local clone of the repository, see [installing a local package](https://docs.unity3d.com/Manual/upm-ui-local.html) in the Unity manual.


