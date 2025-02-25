# Robots
`Robot` is the class for articulated robot arms in RCareWorld. The backend physics computation is handled by [PhysX](https://docs.unity3d.com/2023.1/Documentation/Manual/PhysicsOverview.html), which is the native physics backend of Unity. 
## Load a robot
There are two ways of loading a robot into a scene, namely, using Python or using Unity Editor.
### Use Python API
If you want to use Python to load a robot, make sure the robot is supported by RCareWorld. 
Currently, we support these robots. 


```eval_rst
+---------------------------+-----------+---------------+
| Robot                     | ID        | Gripper       |
+===========================+===========+===============+
| kinova_gen2_7dof-3finger  | 315894    | 3-finger hand |
+---------------------------+-----------+---------------+
| kinova_gen3_7dof-robotiq85| 315893    | robotiq85     |
+---------------------------+-----------+---------------+
```

Assume you have already created an environment by doing `env = RCareWorld(assets=[<asset_name>])`. 

To create a kinova_gen3_7dof_robotiq85 robot, add a line of code
```
env._create_robot(315894, [3158940], 'kinova_gen3_7dof')
```
Here `315894` is the id of the robot, and `3158940` is the id of the gripper. By default, gripper id is `robot_id` * 10. Use `env._get_robot(robot_id)` to get the robot you just created.
```
robot = env._get_robot(315894)
# if the robot is not in the scene, you need to load it
robot.load()
```
You sohuld be able to see the robot in the scene after doing these steps.

### Use Unity Editor
If your robot is not natively available in RCareWorld as a prefab, you need to use the Unity Editor to load it. Refer to [URDF Importer](https://github.com/Unity-Technologies/URDF-Importer#importing-the-robot-using-urdf-file) for more details.
After performing the steps in *URDF Importer*, you need to remove the scripts add by this add-on. 

![1. Import the robot with URDF importer.](https://user-images.githubusercontent.com/16759982/216427827-fbe4fcb1-e615-43bc-9d81-330b8c7205c8.png)

![2. Assign the ropbot an ID after importing.](https://user-images.githubusercontent.com/16759982/218605859-56b8f880-3f89-413d-9dfc-da5e19bb27ec.png)

If the robot does not have gripper on it, you will also need to load the gripper from the corresponding URDF files and attach it to the robot. We demonstrate this step with a robotiq85 gripper in this tutorial.
![3. Similarly, import the gripper into the scene with URDF importer.](https://user-images.githubusercontent.com/16759982/218606528-59225952-b9e5-4b95-847c-ba8ac152fe53.png)

![4. Drag the gripper and make it as child of the EndEffector_Link. Modify the transform of it to be (0,0,0). ](https://user-images.githubusercontent.com/16759982/218606834-87f92dda-646f-4b7c-9337-20f0dc3823c3.png)

![5. Do the `InitializeRCareWorldRobotJoints` step, and click `GetJointParameters`.](https://user-images.githubusercontent.com/16759982/218607048-2a36ba90-8139-497b-ba0f-7af8dbfcd603.png)

![6. In childs of the robot arm, add the ghripper. It can be accessed with `robot_id`\*10 as its id.](https://user-images.githubusercontent.com/16759982/218607273-d39be889-8d84-4b8a-b58f-44373bda3e1b.png)




<!-- ![2. Check if the robot is completely imported.](https://user-images.githubusercontent.com/16759982/216428034-d7cf6bd7-21dc-47da-8026-7fc663190b61.png)


![3. Click on the robot in the `Hierarchy` tab on the left side. Then click `CareTool/Articulation Body/Initialize RCareWorld Robot Joints` in the bar above.](https://user-images.githubusercontent.com/16759982/216428206-513cf1c2-f97b-40a2-b2a4-827548b0ec38.png)

![The tool bar](https://user-images.githubusercontent.com/16759982/216428412-16504e60-bd8e-4306-9d01-9e06fdb473aa.png)

![4. Original scripts from URDF importer should be removed and the robot should look like this in the inspector window.](https://user-images.githubusercontent.com/16759982/216428483-b19d7a2d-9730-4f2d-95e2-fb0739b61372.png)

![5. Click on the get `GetArticulationDatas` and `GetJointParameters` . The joint parameters should have been added to the script. You can unfold it to check if the parameters are added correctly.](https://user-images.githubusercontent.com/16759982/216429777-4e4ca04a-3ad8-4218-9f65-d001fc566a37.png)


![6. Select the robot in the scene, and drag it into some folders, to make it a prefab. Press `Ctrl + G` to make it addressable assets, which can be loaded by Python into the Scene.
The `addressble` box should be checked if the step is successful.](https://user-images.githubusercontent.com/16759982/216430606-41a6754b-ee63-408f-8243-3d94bc35d905.png) -->

Remember to etup URDF for Python. Specify URDF path when you initialize the robot. Note, the path here should be an absolute path.
```
env._create_robot(315894, [3158940], YOUR_PATH_TO_URDF)
```

## Move a robot
### In joint space
Use `setJointPositions` to set joint target positions, and move to the target position graduately. Use `setJointPositionsDirectly` to teleport joints. The joint positions are in `degrees`. Use `setJointPositionsContinue` if `BioIK` is enabled. 

The order of the list of positions starts from the `root` of the articulation body. Take robots as the example, the 0-th element is its first movable joint from the base.
```
# Example:
# Have a robot object
my_robot = env.robot()
# Have a list of joint positions, in dergees
joint_positions = [0, 10, 10, 10, 10, 10, 100]
# Set joint positions
my_robot.setJointPositions(joint_positions = joint_positions)
# Teleport joint positions
my_robot.setJointPositionsDirectly(joint_positions = joint_positions)
```

### In task space
There are two ways to move robots in the task space, THe difference is which IK to use.
### With Pybullet IK
You can 
### With BioIK
![Check this box to initialize BioIK](https://user-images.githubusercontent.com/16759982/217403513-2fc3108d-3d41-4a3f-93e9-dc674b55e089.png)
If BioIK is initialized, you will be able to use the following functions:
```
```


