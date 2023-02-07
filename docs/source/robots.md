# Robots
`Robot` is the class for articulated robot arms in RCareWorld. The backend physics computation is handled by [PhysX](https://docs.unity3d.com/2023.1/Documentation/Manual/PhysicsOverview.html), which is the native physics backend of Unity. 
## Load a robot
There are two ways of loading a robot into a scene, namely using Python or using Unity Editor.
### Use Python API
If you want to use Python to load a robot, make sure the robot is supported by RCareWorld. 
Currently, we support these robots. 


```eval_rst
+-------------------------+-----------+
| Robot                   | ID        | 
+=========================+===========+ 
| Kinova_gen2_7dof_3finger| 315894    | 
+------------+------------+-----------+ 
```

Assume you have already created an environment by doing `env = RCareWorld(assets=['MyNewCube'], is_in_scene = False)`. To load a Kinova_gen2_7dof_3finger robot, add a line of code
```
env._create_robot(315894, [3158940], 'kinova_gen2_7dof')
```
Here `315894` is the id of the robot, and `3158940` is the id of the gripper. By default, gripper id is `robot_id` * 10. Use `env._get_robot(robot_id)` to get the robot you just created.
```
robot = env._get_robot(315894)
```

### Use Unity Editor
If your robot is not natively available in RCareWorld now as a prefab, you need to use the Unity Editor to load it. Refer to [URDF Importer](https://github.com/Unity-Technologies/URDF-Importer#importing-the-robot-using-urdf-file) for reference.
After performing the steps in *URDF Importer*, you need to remove the scripts add by this add-on. 

![1. Import the robot with URDF importer.](https://user-images.githubusercontent.com/16759982/216427827-fbe4fcb1-e615-43bc-9d81-330b8c7205c8.png)


![2. Check if the robot is completely imported.](https://user-images.githubusercontent.com/16759982/216428034-d7cf6bd7-21dc-47da-8026-7fc663190b61.png)


![3. Click on the robot in the `Hierarchy` tab on the left side. Then click `CareTool/Articulation Body/Initialize RCareWorld Robot Joints` in the bar above.](https://user-images.githubusercontent.com/16759982/216428206-513cf1c2-f97b-40a2-b2a4-827548b0ec38.png)

![The tool bar](https://user-images.githubusercontent.com/16759982/216428412-16504e60-bd8e-4306-9d01-9e06fdb473aa.png)

![4. Original scripts from URDF importer should be removed and the robot should look like this in the inspector window.](https://user-images.githubusercontent.com/16759982/216428483-b19d7a2d-9730-4f2d-95e2-fb0739b61372.png)

![5. Click on the get `GetArticulationDatas` and `GetJointParameters` . The joint parameters should have been added to the script. You can unfold it to check if the parameters are added correctly.](https://user-images.githubusercontent.com/16759982/216429777-4e4ca04a-3ad8-4218-9f65-d001fc566a37.png)


![6. Select the robot in the scene, and drag it into some folders, to make it a prefab. Press `Ctrl + G` to make it addressable assets, which can be loaded by Python into the Scene.
The `addressble` box should be checked if the step is successful.](https://user-images.githubusercontent.com/16759982/216430606-41a6754b-ee63-408f-8243-3d94bc35d905.png)

7. Setup URDF for Python. Specify URDF path when you initialize the robot. Note, the path here should be an absolute path.
```
env._create_robot(315894, [3158940], YOUR_PATH_TO_URDF)
```
