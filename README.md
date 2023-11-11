# InnoGames Houdini Tools

Welcome to InnoGames' open-source repository of Houdini tools for mobile game production!

These nodes have been crafted to optimize our mobile FX pipeline creation. 
The emphasis here is on simplifying the process of generating meshes, alongside offering tools for enhancing production workflows.  
Our collection of custom HDA's has been specifically designed to create game assets for mobile productions.

All of the code in this repository is open-source, which means that you can view, modify, and contribute to it in any way you see fit. 
Thank you for visiting our repository, and we hope that these HDA's will help you in your mobile production pipeline!

## Table of Contents
- [Installation](#installation)
- [OBJ](#obj)
  - [Global Executer](#global-executer)
- [SOP](#sop)
  - [Attribute Path](#attribute-path)
  - [Color UV Ramp](#color-uv-ramp)
  - [Copy Parms](#copy-parms)
  - [Dot Mask](#dot-mask)
  - [Fbx Exporter Extended](#fbx-exporter-extended)
  - [Get Min Max](#get-min-max)
  - [Group By Color](#group-by-color)
  - [Set Vertex Color](#set-vertex-color)
  - [Simple Renderer](#simple-renderer)
  - [Split By Attribute](#split-by-attribute)
  - [Swipe Mesh](#swipe-mesh)
  - [UV By Color](#uv-by-color)
  - [Vertex Motion Generator](#vertex-motion-generator)
<br>

## Installation
1. Create a folder named "InnoGamesHoudiniSetup" on your C:\ drive. If you're using a different operating system like Mac/Linux, modify the path in the JSON file accordingly.
2. Copy the 'otl' folder into the newly created folder.
3. Copy the InnoGames_Package.json file into your Houdini application folder. For example under Windows, it could be located at: `C:\Program Files\Side Effects Software\Houdini 19.5.569\packages`
> **Note:** For more information about json packages check the SideFx documentation:
> https://www.sidefx.com/docs/houdini/ref/plugins.html#overview
4. Open Houdini, and the HDAs will be loaded.
<br>

## OBJ
### Overview
These nodes are designed to work at the object level.
<br>

### Global Executer
#### Overview
The Global Executer takes a node as input and extracts the name of a parameter and the path to a source node from its parameters. 
It then finds all nodes in the current Houdini scene and checks if they are of the same type as the source node. If so, it executes the specified parameter on the target node.
<br>

![Example](https://github.com/innogames/IgHoudiniTools/blob/main/Docs/Images/executer_01.gif)
Spread: This function takes a node as input, along with a source node and a list of parameter names from its parameters. 
It finds all nodes in the scene and checks if they have the same name as the source node. If so, it copies the values of the specified parameters from the source node to the target node.
<br>

![Example](https://github.com/innogames/IgHoudiniTools/blob/main/Docs/Images/CopyParms_01.gif)
Rename Nodes: This function takes a node as input and receives the path to a root node, a string to replace, and a new string. 
It then finds all children of the root node and renames nodes containing the old string in their name by replacing it with the new string.
<br>

![Example](https://github.com/innogames/IgHoudiniTools/blob/main/Docs/Images/Nodes_Renamed_01.gif)
#### Properties Global Executer
| Properties        | Description                                                                                   |
|-------------------|-----------------------------------------------------------------------------------------------|
| Source Node Path  | Path to the source node from which the parameter values will be copied.                       |
| Parameter Execute | Name of the parameter that will be executed on nodes of the same type as the source node.     |
#### Properties Parameter Spreader
| Properties        | Description                                                                                  |
|-------------------|----------------------------------------------------------------------------------------------|
| Source Node Path  | Path to the source node from which the parameter values will be copied.                      |
| Parameter To Copy | Names of the parameter tuples to be copied from the source node to the target nodes.         |
#### Properties Renamer
| Properties          | Description                                                                   |
|---------------------|-------------------------------------------------------------------------------|
| Root Path To Search | Path to the root node where the children nodes will be searched for renaming. |
| String To Replace   | The string to be replaced in the node names.                                  |
| New String          | The new string that will replace the old string in the node names.            |
<br>

## SOP
### Overview
These nodes are designed to work at the SOP level.
### Attribute Path
#### Overview
The "Path Attribute" node is used to generate a path as a primitive attribute. 
This can be helpful when you want to export separate meshes as FBX files, for instance. 
By setting a unique path for each mesh using this node, you can ensure that they are exported as separate objects.
<br>

![Example](https://github.com/innogames/IgHoudiniTools/blob/main/Docs/Images/attrib_path_01.gif)
#### Properties
| Properties | Description                |
|------------|----------------------------|
| Path       | Set the attribute name.    |
<br>

### Color UV Ramp
#### Overview
This node takes UV coordinates as input and generates a color ramp based on those coordinates.
<br>

![Example](https://github.com/innogames/IgHoudiniTools/blob/main/Docs/Images/color_uv_ramp_01.gif)
#### Properties
| Properties        | Description                                                      |
|-------------------|------------------------------------------------------------------|
| Group             | Select the group to apply the color.                             |
| Color             | Set the color as a ramp.                                         |
| Projection Axis   | Set the axis for the UV projection.                              |
| Texture Type      | Select the projection type to use.                               |
| Use Uv From Input | Uses the UV from input geometry as a reference for the ramp.     |
<br>

### Copy Parms
#### Overview
This node copies parameter values, parameter references, and node names.
#### Properties
| Properties      | Description                                                             |
|-----------------|-------------------------------------------------------------------------|
| Copy Parameters | Copies the values of the parameters.                                    |
| Copy Parameters | Copies parameter references.                                            |
| Copy Parameters | Copies the node name.                                                   |
| Source Node     | Drag and Drop the node here or add the path of the source node.         |
| Target Node     | Drag and Drop the node here or add the path of the target node.         |
<br>

### Dot Mask
#### Overview
The Dot Mask tool creates black and white areas based on dot product values, 
representing alignment or deviation from a target point.
<br>

![Example](https://github.com/innogames/IgHoudiniTools/blob/main/Docs/Images/dot_mask_01.gif)
#### Properties
| Properties        | Description                                                      |
|-------------------|------------------------------------------------------------------|
| Use Own Direction | Enables the second input to use a custom target point.           |
| Attribute         | The name of the attribute storing the mask data.                 |
| Direction         | Built-in direction coordinates.                                  |
| Ramp              | Controls the transition between white and black.                 |
<br>

### Fbx Exporter Extended
#### Overview
This node is base on the 'Rop Fbx Output', with some transform, cleanup and InnoGames / Unity specific workflow adjustments. 
#### Properties
| Properties                                           | Description                                                                         |
|------------------------------------------------------|-------------------------------------------------------------------------------------|
| Translate                                            | Translates the position of the export geo.                                          |
| Rotation                                             | Rotates the the export geo.                                                         |
| Flip Mesh                                            | Flips the normals of the geo.                                                       |
| Set Normals                                          | Set a custom value.                                                                 |
| Normals Angle                                        | Sets the angle of the normals.                                                      |
|                                                      |                                                                                     |
| Vertex Alpha To Uv                                   |                                                                                     |
|                                                      |                                                                                     |
| Disable Alpha To Uv                                  | If this enabled the vertex alpha value will not written in other attribute.         |
| Set Attribute                                        | By adding a attribute name, it will ad this attribute with the vertex alpha values. |
|                                                      |                                                                                     |
| Delete Attributes                                    |                                                                                     |
|                                                      |                                                                                     |
| Point Attributes                                     | Deletes the selected point attribute.                                               |
| Vertex Attributes                                    | Deletes the selected vertex attribute.                                              |
| Primitive Attributes                                 | Deletes the selected primitive attribute.                                           |
| Detail Attributes                                    | Deletes the selected detail attribute.                                              |
|                                                      |                                                                                     |
| Export                                               |                                                                                     |
|                                                      |                                                                                     |
| Use Path Attrib                                      | With using the path attribute you can define different path for geo elements.       |
| Mesh Name                                            | Set here name for the mesh if you not using the path attribute.                     |
| Output File                                          | Path of the export geometry.                                                        |
| Save Disk                                            | Saving the fbx file to disk.                                                        |
| Valid Frame Range                                    | Selecting here the .                                                                |
| Start/End/Inc                                        | Controls the transition between white and black.                                    |
|                                                      |                                                                                     |
| Export Settings                                      |                                                                                     |
|                                                      |                                                                                     |
| For Export Settings parameters check the SideFX page | https://www.sidefx.com/docs/houdini/nodes/out/filmboxfbx.html                       |
<br>

### Get Min Max
#### Overview
The Get Min Max node grabs the min and max values of an attribute for each frame or from a selected frame. 
The min and max values are set as detail attributes.
<br>

![Example](https://github.com/innogames/IgHoudiniTools/blob/main/Docs/Images/min_max_01.gif)
#### Properties
| Properties                  | Description                                                          |
|-----------------------------|----------------------------------------------------------------------|
| Get Min Max From Each Frame | Grabs Min Max Values from an attribute for each frame.               |
| Get Min Max From Frame      | Selects the frame to get min max values.                             |
| Original Class              | Selects the geometry class, point, prim, etc.                        |
| Min From Attribute          | Specifies the attribute name for getting the min value.              |
| Max From Attribute          | Specifies the attribute name for getting the max value.              |
<br>

### Group By Color
#### Overview
The Group By Color node creates groups based on a specific color value.
#### Properties
| Properties         | Description                                         |
|--------------------|-----------------------------------------------------|
| Prim Attribute     | Creates groups based on a specific color value.     |
| Color To Group     | Selects the color value to create groups from.      |
| Group Name         | Specifies the name for the created groups.          |
<br>  

### Set Vertex Color
#### Overview
This node sets vertex colors by a range on points, prims, or elements. It can be used to generate vertex color ranges.
<br>
> **BUG NOTE:** When the HDA is initialized for the first time in the SOP Network, the first index of the selector will not work.
Workflow: After the first initialization, add a selector, delete it, and add a new one. From this point on, all other selectors will work.

![Example](https://github.com/innogames/IgHoudiniTools/blob/main/Docs/Images/SetVertexColors_01.gif)
#### Properties
| Properties         | Description                                                  |
|--------------------|--------------------------------------------------------------|
| Points Selection   | Sets the selection type to points.                           |
| Prims Selection    | Sets the selection type to prims.                            |
| Elements Selection | Sets the selection type to 3D connected geometry.            |
| Add Selector       | Sets the number of selectors.                                |
| Red                | Sets the selector to the red vertex channel.                 |
| Green              | Sets the selector to the green vertex channel.               |
| Blue               | Sets the selector to the blue vertex channel.                |
| Alpha              | Sets the selector to the alpha vertex channel.               |
| Range              | Increases the selection area when set to a higher value.     |
| Range Hardness     | Masks the selection more sharply when set to a higher value. |
| Position           | Sets the position vector of the selector.                    |
<br>  

## Simple Renderer
### Overview
The Simple Renderer node is a render node used at the SOP Level. 
It's designed for quick and fast rendering of shapes to generate textures. The rendered output is based on the Cd (color) attribute of the geometry.
### History
I needed something to bake simple gradients, distortions maps, colors etc, and to render geometries quick and with out any render time.
I found something here in cgwiki from Matt Estela.<br> 
https://www.tokeru.com/cgwiki/HoudiniCops#Using_cops_as_a_renderer <br>  
Which is based on Konstantin Magnus render solution in cops.  
https://www.youtube.com/watch?v=iDeE_XtaKk0&t=2s&ab_channel=KonstantinMagnus <br> 
Here a detailed documentation about the Custom Raytracer.
https://procegen.konstantinmagnus.de/custom-raytracer

I took this solutions and build my own rendering GUI and created a HDA out of it.
<br>

![Example](https://github.com/innogames/IgHoudiniTools/blob/main/Docs/Images/SimpleRenderer_01.gif)
#### Properties Main
| Properties           | Description                                  |
|----------------------|----------------------------------------------|
| Open Renderer Window | Opens the renderer window.                   |
#### Properties Scene Rendering
| Properties        | Description                                 |
|-------------------|---------------------------------------------|
| Resolution        | Pixel resolution of the rendering image.    |
| Start/End/Inc     | Frame range for rendering.                  |
| Valid Frame Range | Validates the frame range.                  |
| Output Picture    | Path of the rendered image.                 |
| Render            | Saves the rendered image to disk.           |
#### Properties UV Rendering
| Properties        | Description                                 |
|-------------------|---------------------------------------------|
| Resolution        | Pixel resolution of the rendering image.    |
| Start/End/Inc     | Frame range for rendering.                  |
| Valid Frame Range | Validates the frame range.                  |
| Output Picture    | Path of the rendered image.                 |
| Render            | Saves the rendered image to disk.           |
#### Properties Camera
| Properties   | Description                          |
|--------------|--------------------------------------|
| Translate    | Move the camera along XYZ axis.      |
| Rotate       | Rotate the camera along XYZ axis.    |
| Focal Length | Focal length of the camera.          |
<br>

## Split By Attribute
### Overview
The Split By Attribute node organizes objects based on a specified attribute in the geometry. 
Additional nodes can be added to the split network, and they are connected in a specific order.
<br>

![Example](https://github.com/innogames/IgHoudiniTools/blob/main/Docs/Images/SplitByAttribute_01.gif)
#### Properties
| Properties           | Description                           |
|----------------------|---------------------------------------|
| Attribute To Split   | Attribute for splitting the geometry. |
| Add Nodes            | Add nodes to the split network.       |
| Split                | Initiates the splitting process.      |
<br>

## Swipe Mesh
### Overview
The Swipe Mesh node is an extension of the sweep node with additional custom features. 
It allows saving vertex alpha into the UV1 channel, enabling separation of vertex alpha from particle alpha in Unity. It integrates resample features, providing flexibility in density and detail.
<br>

![Example](https://github.com/innogames/IgHoudiniTools/blob/main/Docs/Images/SwipeMesh_01.gif)
> **Note:** Please refer to the documentation for sweep and resample node properties for more details:
> - Sweep Node: https://www.sidefx.com/docs/houdini/nodes/sop/sweep.html
> - Resample Node: https://www.sidefx.com/docs/houdini/nodes/sop/resample.html

> **Note:** The Alpha option adds vertex alpha to the UV1 attribute. This is important for later use in the game engine, where Unity particles apply their own vertex colors and alpha to the original mesh. To retain control over alpha, vertex alpha is stored in UV1 index 0, which is supported by our Unity shaders.
#### Properties Alpha
| Properties | Description                       |
|------------|-----------------------------------|
| Mask U     | Ramp relative to U coordinates.   |
| Mask V     | Ramp relative to V coordinates.   |
<br>

## Uv By Color
### Overview
The Uv By Color node grabs vertex colors RGB as a group to layout UV packages dynamically. It's useful for creating simple UV maps layouts.
<br>

![Example](https://github.com/innogames/IgHoudiniTools/blob/main/Docs/Images/UvByRGB_01.gif)
#### Properties
| Properties                     | Description                                    |
|--------------------------------|------------------------------------------------|
| Disable Cd to promote to prim. | Disables promoting Cd to prim.                 |
| Color To Group                 | Selects the color value to create groups from. |
| Group Name                     | Specifies the name for the created groups.     |
<br>

## Vertex Motion Generator
### Overview
The Vertex Motion Generator tool applies vertex colors as weights for animation. 
Vertex colors are then used in shaders to animate the mesh using sine and cosine functions, creating wave-like animations.
### History
This HDA was inspired by Andres Glad's Vertex Color Based Animation. <br>
https://vimeo.com/396568661 <br> <br>
I rewrite the Unreal shader setup in VEX to have the right preview in Houdini.
And put some ramps properties to have easy control of the weights. 
In Unity I rewrite the same calculation in a shader to have the same result in the Engine like in Houdini.<br>
Here the shader function for Unity:
```ruby
float _Speed;
float _StrengthX;
float _StrengthY;
float _useSymX;
float _useSymY;

float4 _customData1;
float4 _customData2;

float4 particleMotion(float4 position, float4 morphTarget, float animationOffset, float4 color)
{
    float time = (_Time.y * _Speed) - animationOffset;
    float sinTime = sin(time);
    float absTime = abs(sinTime);
    
    float4 morph = position;
    float constantBiasR = (color.r - 0.5) * 2;
    float constantBiasG = (color.g - 0.5) * 2;
    float linearR = sinTime * color.r;
    float linearG = sinTime * color.g;
    float symetryR = absTime * -constantBiasR;
    float symetryG = absTime * -constantBiasG;
    float switchR = lerp(linearR * _StrenghX, symetryR * _StrengthX, _useSymX);
    float switchY = lerp(linearG * _StrenghY, symetryG * _StrengthY, _useSymY);
    position.x = lerp(position.x, morphTarget.x, switchR); 
    position.z = lerp(position.z, morphTarget.z, switchY);
    
    return position;
}
```
<br>

![Example](https://github.com/innogames/IgHoudiniTools/blob/main/Docs/Images/VertexMotion_01.gif)
#### Visualize Properties
| Properties               | Description                           |
|--------------------------|---------------------------------------|
| Enable Animation Preview | Visualizes the animation.             |
| Speed                    | Animation speed.                      |
| Vertex Motion X Axis     | Strength of the X-axis animation.     |
| Vertex Motion Y Axis     | Strength of the Y-axis animation.     |
#### Visualize
| Properties | Description                        |
|------------|------------------------------------|
| Ramp X     | Visualizes X-axis ramp.            |
| Ramp Y     | Visualizes Y-axis ramp.            |
| Ramp Power | Visualizes power ramp.             |
### Vertex Weights Properties
| Properties         | Description                       |
|--------------------|-----------------------------------|
| Set Ramp Direction | Sets the ramp direction.          |
| X Direction        | Aligns the ramp to the X-axis.    |
| Y Direction        | Aligns the ramp to the Y-axis.    |
| Z Direction        | Aligns the ramp to the Z-axis.    |
#### Ramps
| Properties             | Description                                 |
|------------------------|---------------------------------------------|
| Enable Symmetry X Axis | Activates symmetry for the X-axis.          |
| Enable Symmetry Y Axis | Activates symmetry for the Y-axis.          |
| X Axis Ramp            | Sets weights for the X-axis animation.      |
| Z Axis Ramp            | Sets weights for the Y-axis animation.      |
| Power  Ramp            | Sets weight for the power.                  |
| Power                  | Maximum power value.                        |
#### Morph Target Properties
| Properties              | Description                                   |
|-------------------------|-----------------------------------------------|
| Use Custom Morph Target | Enables using a custom morph target.          |
| Blend Morph Target      | Blends original mesh with the morph target.   |
#### Transform
| Properties | Description                                 |
|------------|---------------------------------------------|
| Translate  | Translates the default morph target.        |
| Rotate     | Rotates the default morph target.           |
| Scale      | Scales the default morph target.            |
<br> 
