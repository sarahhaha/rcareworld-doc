# Scene
A scene is a basic environment in RCareWrorld. There are human avatars, robot agents, assistive devices, and other 3D objects in a scene.
## Scene setup
We will introduce how to make an environment with agents and different kinds of objects here in a high level manner. For details of each category of objects, please refer to the corresponding sections.

### Setting up in Unity Editor
Here's a simple example of how you setup a scene and add objects to it.
![Make a copy of the `Empty` scene](https://user-images.githubusercontent.com/16759982/217998701-4bc5e513-22ec-4ed0-b1f7-c4cbba32ae50.png)

![Rename your new scene](https://user-images.githubusercontent.com/16759982/217998910-756a004c-ed68-4bff-80fc-c18a56f9f8c8.png)

Add your new objects into the scene. Adding new objects into the scene is the same with the steps in Unity. If you are new to Unity, [Unity's Manual](https://docs.unity3d.com/2023.1/Documentation/Manual/CreatingScenes.html) would be helpful for you. We will follow the terms Unity uses in this tutorial, for instance, scene, gameobjects, prefab, layer, etc.

![Add a cube into the scene](https://user-images.githubusercontent.com/16759982/217999121-478c566d-3f26-4db5-bc97-3fa284d936f5.png)

![Attach xxxAttr scripts to the game](https://user-images.githubusercontent.com/16759982/217999536-3d54a93c-841f-4b5f-9958-65b9a1e25c1b.png)

![Asign it an ID](https://user-images.githubusercontent.com/16759982/218000860-1dab1a20-8a90-4286-9856-2a284ccbf1b1.png)

![The object is recognized if you see its name in Unity's log terminal after clicking `Play` button](https://user-images.githubusercontent.com/16759982/218001332-4ad92c7b-c40f-4365-8875-f9562e88918f.png)

Click `RFUniverse/SceneExportToJson` in the tool bar above.
![The bar, click RFUniverse](https://user-images.githubusercontent.com/16759982/218005736-5b3b1ba0-227b-4ab9-8424-a0ca50c1732b.png)

If you see the log of `1` in the terminal, it means the json file is successfully exported. You can find the json file named the same with the scene in `Assets/StreamingAssets/SceneData/`folder.
![Export json file](https://user-images.githubusercontent.com/16759982/218006177-a7e65fb0-3af6-4953-b63a-84bcd9ad3504.png)



### Setting up with Unity Player without paid assets
Unity Player is an empty Scene without any objects in it. Users can create the scene by loading objects, robots, and humans into it. The scene named Empty in Unity Editor has the same functionality. 
Each object must be assigned a unique ID to be loaded into the scene.

To be loaded with Python, the ojects, robots, and human avatars need to be stored in `AddressableData`, which can be simply done by pressing `Ctrl+G` in Unity Editor. If it is not taking effect after trying for several times, click on something else and then get back to this item. You should be able to see box for addressable checked.
![The box is checked if the model has been added to addressable data. The object name is also displayed here.](https://user-images.githubusercontent.com/16759982/217990603-79645783-4c64-4a24-8b2b-26cadaa58ab2.png) 
 
### Setting up with just Python
Don't want to touch Unity side? If you find it enough to just use the assets we provide, it would be as simple as several lines of python code.

The assets we provide as as the following:



