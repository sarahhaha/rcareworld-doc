# Install  
## System requirement
The simulation environment has been tested on Windows and Ubuntu, while MacOS is not supported. We recommend using a desktop satisfying the requirements [here](https://docs.unity3d.com/Manual/system-requirements.html).

If you are using Ubuntu version 22.04 you will need to create a symlink 

You can check your unity version with the following command
```
lsb_release -a
```

If the version is 22.04, then you will need to create a symlink from libdl.so.2 to libdl.so.
You can search the path of libdl.so.2 and create a symlink like so
```
whereis libdl.so.2
libdl.so.2: [PATH of libdl.so.2]
sudo ln -s [PATH of libdl.so.2] [PATH of libdl.so]
```

## File structures
Organize the folder as  
```
RCareWorld 
- rcare_py
- rcare_unity
```

You might use the following commands
```
mkdir rcareworld_workspace
cd rcareworld_workspace
mkdir rcare_py
mkdir rcare_unity
```
## Install Python module
Follow the following steps to install the python module. If you would like to perform reinforcement learning, you need to also install rl-baselines3-zoo.
```
# Create conda environment
conda create -n rcare python=3.8
conda activate rcare

# Install pyrfuniverse
git clone https://github.com/mvig-robotflow/pyrfuniverse.git
cd pyrfuniverse
pip install -r requirements.txt
pip install -e .
cd ..
```

```
# Install pyrcareworld
cd rcare_py
git clone https://github.com/empriselab/pyrcareworld_internal.git
cd pyrcareworld
pip install -r requirements.txt
pip install -e .
cd ..
```

The file structure should look like
```
RCareWorld 
- rcare_py
    - pyrcareworld
    - pyrfuniverse
    - rl-baseline3-zoo-1.1.0 (optional)
- rcare_unity
```
## With prebuilt environments
Download Unity executable files [Windows] [Ubuntu].
## With builtin assets
Download Unity exectuable files [Windows] [Ubuntu].
Use the editor
For Windows, `./Player.exe -edit`. For Ubuntu, `./Player.x86_64 -edit`

## With custom assets
### Install Unity
RCareWorld currently works with Unity 2022.1.3+. Please install this version of Unity Editor. Before that, you might need to install Unity-Hub. See [this](https://unity.com/download) for reference.
### Import RCareWorld Project into Unity
The whole project can be downloaded from Google Drive, please contact the development team to have access to the codebase of Unity.
You need to get the paid assets from Unity Asset Store to get Unity side working. We provide an asset list for you to purchase. After downloading, you need to import the project into Unity. Ignore the errors and continue.
### Fix the Errors by Installing Packages
Users will need to purchase certain packages to use the simulation environment.
#### Obi 
- `Softbody` for soft-tissue on human body https://assetstore.unity.com/packages/tools/physics/obi-softbody-130029
- `Fluid` (optional) https://assetstore.unity.com/packages/tools/physics/obi-fluid-63067
- `Cloth` for tasks involving garments (optional) https://assetstore.unity.com/packages/tools/physics/obi-cloth-81333
- `Rope` (optional) https://assetstore.unity.com/packages/tools/physics/obi-rope-55579

*KNOWN ISSUE*: 
![Issue like this](https://user-images.githubusercontent.com/16759982/217441647-120a9204-8db3-4dce-851b-6b49fa5ce34b.png)
Follow this link to fix it.
http://obi.virtualmethodstudio.com/forum/thread-3703-post-13679.html?highlight=GraphColoring#pid13679
#### BioIK
To replace the pybullet IK for articulated agents like human and robots. https://assetstore.unity.com/publishers/22741
#### DOTWeen (Free asset)
https://assetstore.unity.com/packages/tools/animation/dotween-hotween-v2-27676


### Install URDF Importer
1. Open the Package Manager from Unity Menu. Click `Window -> Package Manager`. A new package manager window will appear.

2. Click on the `+` sign on the top left corner of the package manager window and click on `Add Package from Git URL`. 

3. Enter the git URL for the URDF Importer with the latest version tag (currently v0.5.2) `https://github.com/Unity-Technologies/URDF-Importer.git?path=/com.unity.robotics.urdf-importer#v0.5.2` in the text box and press `Enter`.

4. Click `Import URDF`.
### Install Unity Robotics Hub (Optional for ROS interface)
1. Open `Window` -> `Package Manager`.

1. In the Package Manager window, find and click the `+` button in the upper lefthand corner of the window. Select `Add package from git URL...`.

1. Enter the git URL for the package. Note: you can append a version tag to the end of the git url, like `#v0.4.0` or `#v0.5.0`, to declare a specific package version, or exclude the tag to get the latest from the package's `main` branch.
   1. For the [ROS-TCP-Connector](https://github.com/Unity-Technologies/ROS-TCP-Connector), enter `https://github.com/Unity-Technologies/ROS-TCP-Connector.git?path=/com.unity.robotics.ros-tcp-connector`.

1. Click `Add`.

To install from a local clone of the repository, see [installing a local package](https://docs.unity3d.com/Manual/upm-ui-local.html) in the Unity manual.


