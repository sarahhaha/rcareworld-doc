# Scene
A scene is a basic environment in RCareWrorld. There are human avatars, robot agents, assistive devices, and other 3D objects in a scene.
## Scene setup
We will introduce how to make an environment with agents and different kinds of objects here in a high level manner. For details of each category of objects, please refer to the corresponding sections.

### Setting up in Unity Editor
![image](https://user-images.githubusercontent.com/16759982/217997188-308adcbe-61df-4443-ba96-be132bb622f8.png)


### Setting up with Unity Player without paid assets
Unity Player is an empty Scene without any objects in it. Users can create the scene by loading objects, robots, and humans into it. The scene named Empty in Unity Editor has the same functionality. 
Each object must be assigned a unique ID to be loaded into the scene.

To be loaded with Python, the ojects, robots, and human avatars need to be stored in `AddressableData`, which can be simply done by pressing `Ctrl+G` in Unity Editor. If it is not taking effect after trying for several times, click on something else and then get back to this item. You should be able to see box for addressable checked.
![The box is checked if the model has been added to addressable data. The object name is also displayed here.](https://user-images.githubusercontent.com/16759982/217990603-79645783-4c64-4a24-8b2b-26cadaa58ab2.png) 
 
### Setting up with just Python
Don't want to touch Unity side? If you find it enough to just use the assets we provide, it would be as simple as several lines of python code.

The assets we provide as as the following:



