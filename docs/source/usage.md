# Install
There are two ways of installing RCareWorld. 
## With builtin assets
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
### RFUniverse Dependency
We use [RFUniverse](https://wenqiangx.github.io/robotflowproject/project/rfuniverse/) to construct Unity side and to communicate with Python side. 
Since RFUnivese has not been made public, please reach out to Cathy (ry273@cornell.edu) to get full Unity code for RFUniverse.
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


# Getting Started
RCareWorld is built upon RFUniverse project, which leverages the communication scheme of [ML-agents](https://github.com/Unity-Technologies/ml-agents/blob/main/docs/Getting-Started.md). You may take a look at ML-agent's tutorial to have an overview of how the Python-Unity framework works. In short, Unity and Python communicates with each other with gRPC. Also, please refer to ML-agent's tutorial to have an overview of the Scene concept in Unity.
In this section, we'll first look at an example and then introduce the elements of RCareWorld.
## The First Example
Let's start with an example. Start your Unity Editor before doing the steps in the following. 
First, open the `Man` scene in Unity Editor. There should be something like the following image. Make sure the models are complete.
![Unity Editor](https://user-images.githubusercontent.com/16759982/174258734-b8c9362e-15d6-4664-a19d-f4e54a0f4bb9.png)

Second, run `pyrfuniverse/tests/test_man.py`
```
python test_man.py
pybullet build time: May  6 2022 01:58:07
Side channel id in use:
534c891e-810f-11ea-a9d0-822485860400
d587efc8-9eb7-11ec-802a-18c04d443e7d
2d1916c4-4c96-4dff-a341-426976c91192
63d7c283-f43a-4336-8aef-916ea91b1d9f
09bfcf57-9120-43dc-99f8-abeeec59df0f
```

Next, click on the button to run Unity Scene.

![Run button](https://user-images.githubusercontent.com/16759982/174259121-c2b39dc4-432c-4de5-9694-453168527343.png)

You will see the robot moving and repositioning the human avatar's arm. 

![](https://user-images.githubusercontent.com/16759982/174259400-aa355dc5-5871-465c-88c3-61756c7cb5ff.png)

And in the terminal whre python runs you will see outputs like these:
```
{'gravity_forces': [-0.0002206891222158447, 48.74412155151367, -8.762385368347168, 45.774208068847656, 14.679387092590332, 0.8401356339454651, -0.03461959958076477, -0.7229466438293457, 0.2632662057876587, -0.12076511979103088, -0.718228816986084, 0.274467796087265, -0.13025012612342834], 'coriolis_centrifugal_forces': [1.4526883363723755, -1.005357265472412, 1.6692850589752197, -1.5723116397857666, -0.10112074017524719, 1.1313716173171997, 0.021233953535556793, -0.011885210871696472, -0.015485050156712532, -0.0005606227205134928, 0.04887770116329193, 0.0014246093342080712, 0.007489994168281555], 'drive_forces': [14.636249542236328, -178.42129516601562, 36.54844665527344, -78.24534606933594, -27.06083869934082, -21.341175079345703, 16.785539627075195, 2.2281360626220703, -0.771892786026001, 0.16910383105278015, 1.3702343702316284, -1.7367568016052246, 0.027873782441020012]}
```

Your install will be fine if this demo works correctly.

## Components in a RCareWorld Scene
Let's take a closer look at this scene. Here is a human avatar coverred with soft tissue and a robot arm. The followng section will explain how to setup this scene
and introduce the components in a RCareWorld.
### Agent
Agent is responsible for communicating. An Agent should be placed in the scene to make the Python script work. Agent looks like the following.

![](https://user-images.githubusercontent.com/16759982/174257293-6a467a3f-4854-4f5e-b5e1-a642be449c22.png)

To setup a scene, the first thing is to add an Agent in Unity Editor. Right click in the Hierarchy Window, select `Create Empty`. You will see a new `GameObject` in the editor. Rename it to `Agent`.

Add `BaseAgent` script to this Agent script. Click `Add Component`

![](https://user-images.githubusercontent.com/16759982/174261187-a0390d4e-10c9-472c-93c0-755a359f19fb.png)

Type `Base Agent` and click on the `Base Agent` script. The agent setup is done.

![](https://user-images.githubusercontent.com/16759982/174261326-704dedac-c790-4a76-9273-4ff610e04908.png)

### Attributes

![Game Object Attribute for the Cube](https://user-images.githubusercontent.com/16759982/174290279-93b3f84d-2ff9-4e20-831f-5ef5a1a0b0be.png)

![Controller for Kinova Robot](https://user-images.githubusercontent.com/16759982/174291951-98116a0a-3ffd-4d77-994e-f6a2361b6c19.png)

*You can directly use the robot in `Prefab` folder instaed of setting up a robot from URDF, if you are not trying to use a new robot.*

## Setup the Scene
### Setup Obi Solver
Obi is a purchased asset(package), we can use the one in the codebase for the time being.
Refer to the tutorial to setup a soft body human
http://obi.virtualmethodstudio.com/manual/6.3/charactersoftbody.html
### Attach an Obi Collider to the cube
![](https://user-images.githubusercontent.com/16759982/174292685-36d0b65a-3e60-42c1-bb23-c432085677b8.png)
### Add ObiSolver and ObiLateFixedUpdate to the root node of human model
![](https://user-images.githubusercontent.com/16759982/174292842-cb0fddb1-e644-4eec-ba52-43ca07a94966.png)
### Add Solver into Updater
![](https://user-images.githubusercontent.com/16759982/174292990-a8b1e685-2739-4bb5-8a00-3b60c140a7ee.png)
### Create Asset: SoftbodySurfaceBluePrint
Click Generate after setting like this

![](https://user-images.githubusercontent.com/16759982/174293230-4412821d-d19e-4c0b-ab65-38a7a9f4b0e8.png)

Please refer to the tutorial of Obi softbody for more details.
### Combine Softbody with human
Add ObiSoftBody and ObiSoftBodySkinner to SMPLX-mesh-male node;
Attach SoftBody to the Source softbody of Skinner;
Attach SoftbodySurfaceBluePrint to the Blueprint in ObiSoftBody
![](https://user-images.githubusercontent.com/16759982/174293459-d1767738-e98f-4fc6-9287-444e08d6e5aa.png)

Clink the Bindskin button on ObiSoftBodySkinner
![](https://user-images.githubusercontent.com/16759982/174293550-2c5eed44-2aa8-44a0-b7b2-6859eb540502.png)

### Make human articulated
Add ArticulationBody on the root node of the skeleton. Untick UseGravity. Add ArticulationBody to the subskeletons, for instance, you need to manipulate a human’s arm, maybe you only need to set this arm as an articulated body. 
You can set joint limits and joint types in the inspector window.
![](https://user-images.githubusercontent.com/16759982/174293737-43aa951d-6883-4a3c-81d1-d958c4d2f6cb.png)

### Add proper colliers
You can add capsale colliders for human limbs, or other shape that fits a human body well.
![](https://user-images.githubusercontent.com/16759982/174293964-80b86535-2b72-440f-b3ec-fc2a8e86f973.png)



## Python Code
Then let's have a look at the 
```
class SoftBodyTestEnv(RFUniverseBaseEnv):
    def __init__(
        self
    ):
        super().__init__(
            articulation_channel=True,
            game_object_channel=True,
            rigidbody_channel=True,
        )
        self.ik_controller = RFUniverseKinovaController(
            robot_urdf=os.path.join(
                assets_path.__path__,
                'URDF\kinova_gen3\GEN3_URDF_V12.urdf'
            )
        )

    def move(self, pos: list, rot: list):
        joint_positions = self.ik_controller.calculate_ik(pos, eef_orn=p.getQuaternionFromEuler(rot))
        self._set_kinova_joints(joint_positions)
        self._get_kinova_forces()

    def _set_kinova_joints(self, joint_positions):
        self.articulation_channel.set_action(
            'SetJointPosition',
            id=31589218,
            joint_positions=list(joint_positions[0:7]),
        )
        self._step()
    
    def _get_kinova_forces(self):
        self.articulation_channel.GetJointInverseDynamicsForce(31589218)
        self._step()
        print(self.articulation_channel.data['inverse_dynamics_force'])
```


