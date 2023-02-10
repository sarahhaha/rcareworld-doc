# Scene
A scene is a basic environment in RCareWrorld. There are human avatars, robot agents, assistive devices, and other 3D objects in a scene.
## Scene setup
We will introduce how to make an environment with agents and different kinds of objects here in a high level manner. For details of each category of objects, please refer to the corresponding sections.

### Setting up in Unity Editor
#### Setup your scene and export it as json file
Here's a simple example of how you setup a scene and add objects to it.
![Make a copy of the `Empty` scene](https://user-images.githubusercontent.com/16759982/217998701-4bc5e513-22ec-4ed0-b1f7-c4cbba32ae50.png)

![Rename your new scene](https://user-images.githubusercontent.com/16759982/217998910-756a004c-ed68-4bff-80fc-c18a56f9f8c8.png)

Add your new objects into the scene. Adding new objects into the scene is the same with the steps in Unity. If you are new to Unity, [Unity's Manual](https://docs.unity3d.com/2023.1/Documentation/Manual/CreatingScenes.html) would be helpful for you. We will follow the terms Unity uses in this tutorial, for instance, scene, gameobjects, prefab, layer, etc.

![Add a cube into the scene](https://user-images.githubusercontent.com/16759982/217999121-478c566d-3f26-4db5-bc97-3fa284d936f5.png)

![Attach xxxAttr scripts to the game](https://user-images.githubusercontent.com/16759982/217999536-3d54a93c-841f-4b5f-9958-65b9a1e25c1b.png)

![Asign it an ID](https://user-images.githubusercontent.com/16759982/218000860-1dab1a20-8a90-4286-9856-2a284ccbf1b1.png)

![Drag it to some folder to make it a prefab](https://user-images.githubusercontent.com/16759982/218016555-47fa62e6-4abf-4917-812f-a73c85fcee02.png)

To be loaded with Python, the ojects, robots, and human avatars need to be stored in `AddressableData`, which can be simply done by pressing `Ctrl+G` in Unity Editor. If it is not taking effect after trying for several times, click on something else and then get back to this item. You should be able to see box for addressable checked.
![The box is checked if the model has been added to addressable data. The object name is also displayed here.](https://user-images.githubusercontent.com/16759982/217990603-79645783-4c64-4a24-8b2b-26cadaa58ab2.png) 

![Make it addressable data](https://user-images.githubusercontent.com/16759982/218016785-938e8b40-a7ed-4f60-a915-055905e328fc.png)

![The object is recognized if you see its name in Unity's log terminal after clicking `Play` button](https://user-images.githubusercontent.com/16759982/218001332-4ad92c7b-c40f-4365-8875-f9562e88918f.png)

Click `RFUniverse/SceneExportToJson` in the tool bar above.
![The bar, click RFUniverse](https://user-images.githubusercontent.com/16759982/218005736-5b3b1ba0-227b-4ab9-8424-a0ca50c1732b.png)

If you see the log of `1` in the terminal, it means the json file is successfully exported. You can find the json file named the same with the scene in `Assets/StreamingAssets/SceneData/`folder.
![Export json file](https://user-images.githubusercontent.com/16759982/218006177-a7e65fb0-3af6-4953-b63a-84bcd9ad3504.png)

#### Load your scene with Python
Open the `Empty` scene in Unity, run `example_scene_setup.py` in Python.
```
# Load a scene_file to setup an environment
env = RCareWorld(scene_file='my_new_scene.json')
```

You should be able to see the following output in python terminal.
```
pybullet build time: May 20 2022 19:44:17
Side channel id in use:
534c891e-810f-11ea-a9d0-822485860400
d587efc8-9eb7-11ec-802a-18c04d443e7d
09bfcf57-9120-43dc-99f8-abeeec59df0f
02ac5776-6a7c-54e4-011d-b4c4723831c9
```

![Empty scene](https://user-images.githubusercontent.com/16759982/218021991-f17093df-a62b-4f05-b306-c75f857975df.png)
![The cube is loaded into the scene after running](https://user-images.githubusercontent.com/16759982/218023676-1c12bc11-10d2-4de4-9e34-461ca08e8b65.png)

#### Load an object into the scene with Python
Now we have the asset named Cube. Create a new scene named `load_object` by making a copy of `Empty`.
![Creating the new scene](https://user-images.githubusercontent.com/16759982/218024615-384abff8-bead-45c4-9100-487d330ec3d0.png)
We will try to load the object into the scene as an asset. This loading method allows users to load objects into the scene dynamically suring runtime. Run `example_load_object.py`
```
# Use `assets` parameter to include the assets you want to load by name
env = RCareWorld(assets=['Cube'])
# _create_object initializes the object
# You need to asign an id for it at runtime, which will over write the original id
# If the object is not in the scene yet, and you would like to load it, the `is_in_scene` should be set to false
env._create_object(id = 2333, name = 'Cube', is_in_scene=False)
# This line returns the Object object with the id you specified
cube = env._get_object(2333)
# Load the object into the scene
cube.load()
print(env.instance_channel.data)
while True:
    env._step()
```


### Setting up with Unity Player without paid assets
Unity Player is an empty Scene without any objects in it. Users can create the scene by loading objects, robots, and humans into it. The scene named Empty in Unity Editor has the same functionality. 
Each object must be assigned a unique ID to be loaded into the scene.

 
### Setting up with just Python
Don't want to touch Unity side? If you find it enough to just use the assets we provide, it would be as simple as several lines of python code.

The assets we provide as as the following:


## Python APIs
The `RCareWorld` is the basic environment class in RCareWorld. You can use it to set up an environments with objects, robots, and human agents.

The environment can be initialized by executable file, scene_file, or using Unity Editor. If no scene_file or exectuable file provided, then it uses the Unity editor.
```
class RCareWorld(RFUniverseBaseEnv):
    def __init__(
                 self,
                 executable_file: str = None,
                 scene_file: str = None,
                 custom_channels: list = [],
                 assets: list = [],
                 **kwargs
                 ):
        super().__init__(
            executable_file=executable_file,
            scene_file=scene_file,
            custom_channels=custom_channels,
            assets=assets,
            **kwargs,
        )
        # Information of robot, object, sensor information are stored here
        self.robot_dict = {}
        self.object_dict= {}
        self.camera_dict = {}
        self.sensor_date = {}
        self.human_dict = {}
```

For each environment, we provide these functions to do a global control of the physics parameter of the simulated world.
```
def ignoreLayerCollision(self, layer1:int, layer2:int, ignore:bool):
    self.asset_channel.set_action(
        'IgnoreLayerCollision',
        layer1 = layer1,
        layer2 = layer2,
        ignore = ignore,
    )

    def getCurrentCollisionPairs(self):
        self.asset_channel.set_action(
            'GetCurrentCollisionPairs'
        )
        self._step()
        result = self.asset_channel.data['collision_pairs']
        return result

    def setGravity(self, x:float, y:float, z:float):
        self.asset_channel.set_action(
            'SetGravity',
            x = x,
            y = y,
            z = z,
        )

    def setGroundPhysicMaterial(self, bounciness:float=0, dynamic_friction:float=1, static_friction:float=1, friction_combine:int=0, bounce_combine:int=0):
        self.asset_channel.set_action(
            'SetGroundPhysicMaterial',
            bounciness = bounciness,
            dynamic_friction = dynamic_friction,
            static_friction = static_friction,
            friction_combine = friction_combine,
            bounce_combine = bounce_combine
        )

    def setTimeScale(self, time_scale:float):
        self.asset_channel.set_action(
            'SetTimeScale',
            time_scale = time_scale
        )
 ```
