# Sensors
## Cameras
The camera class in RCareWorld is in `pyrcareworld/sensors/camera.py`. As you can see, the camera class is inherited from `RCareWorldBaseObject`, so it has all the functionalities and properties owned by BaseObjects.

Similar to BaseObjects, you can set the position and rotation, load, copy, and also destroy the camera. For details, please check the `object` section.

### Initialize a camera
To initialize a camera, you need to provide one of the two kinds of information
- Intrinsic matrix: It should be a 9-element list. For instance `[600, 0, 0, 0, 600, 0, 240, 240, 1]`.
- Width, Height, FOV (optional)

```
Example:
```



### Initialize data and get data
In the camera class, the data acquisition is devided into two steps, namely `initialize` and `get`. The `initialize` step informs the Unity side that the user now wants to have access to this kind of data information, and then Unity will start to send this information to Python side. 

For `initialize`, there are three ways to specify the camera parameters. 
- With `intrinsic_matrix`: The functions end with `WithIntrinsic`, like `initializeRGBWithIntrinsic`
- With `height` and `width`
- With `heighr`, `width`, and `fov`

### RGB data
To get RGB data, use `initializeRGBWithIntrinsic` or `initializeRGB`. Don't forget to do a `getRGB` after initializing.

### Depth data
Similarly, use `initializeDepthWithIntrinsic` or `initializeDepth`, and `getDepth`.

### ActiveDepth data
Following [SAPIEN2](https://sapien.ucsd.edu/docs/2.0/tutorial/rendering/raytracing_renderer.html#sensor-simulation-in-kuafu) and [pyrfuniverse](, we now have IR based active depth sensor. 
### 
