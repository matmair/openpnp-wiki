# What is it?
As you know, the closer an object is to a camera, the larger it appears in the camera view. When you need to measure or detect certain shapes, sizes or distances, you need to know at what distance the subject is. On a Pick and Place machine, the first and foremost method of ensuring this, is to make sure, all such subjects (the Homing Fidcuial, PCBs, feeders, nozzle tip changers etc.) are all at the same distance from the camera, i.e. all flush with one universal machine table surface level, i.e. all at the same Z coordinate. For your machine, this should still be an important design goal. 

However, this is not always possible, especially in a DIY environment. Some feeders may be mounted on top of the table etc. Enter **OpenPnP 3D Units per Pixel** (brought to OpenPnP by Tony Luken). These are used to determine the camera viewing scale at different distances, i.e. at different Z coordinates. Whenever the Z coordinate is known (such as the pick location Z of a feeder), we can now automatically adjust the viewing scale, called Units per Pixel, to the Z.

# Calibrating and Enabling 3D Units per Pixel

Camera 3D Units per Pixel are automatically calibrated, when you use [[Issues and Solutions]] Milestones [Vision Solutions](https://github.com/openpnp/openpnp/wiki/Vision-Solutions). Once all the steps have been completed, the camera shows an enabled 3D configuration:

![3D Units per Pixel](https://user-images.githubusercontent.com/9963310/131219497-938464d2-697e-4ec2-90c0-dc706fbca421.png)

Manual calibration is also possible, follow the instructions on the camera Wizard:

![Manual Calibration](https://user-images.githubusercontent.com/9963310/131219525-911702a1-7275-432f-86c2-f5468a69bc1a.png)

# Camera Z Axis sets the Viewing Plane

For the 3D Units per Pixel to be effective, the camera must have a [virtual Z axis](https://github.com/openpnp/openpnp/wiki/Machine-Axes#referencevirtualaxis) assigned (see [[Mapping Axes]]). Whenever the camera moves to a location to perform a vision operation (e.g. over a pick location on a feeder), it will physically move in X, Y but also virtually in Z. By thus moving the Z, it will implicitly set its Units per Pixel to the right scale. 

The viewing plane Z is now visible in the Camera View lower right corner, and if you have the Ruler reticle activated, you will also see how the ticks on the ruler change according to scale (select the camera in the Machine Controls and jog Z up and down): 

![Camera View 3D Z](https://user-images.githubusercontent.com/9963310/131219680-fa0a4dc5-9800-49a8-ac0d-119e098e6c5c.png)

Note: although this was not tested, it should theoretically work the same way for a camera that has its own _real/physical_ Z axis, that can move up and down to focus subjects. The Units per Pixel would not change in this scenario, but the camera viewing or focal plane would. Because the camera still has a distance from its focal plane, moving the camera down in Z is still safe. The 1:1 working principle shows that using the Z axis to "focus" on a subject is quite a natural way.

# Using with Feeders

All the OpenPnP feeders using Computer Vision should now work in 3D (if not, please report a bug :-)). When scale is important, e.g. to recognize carrier tape sprocket holes by their size and pitch, the relevant Z must be known, for the feeder vision to work. Therefore, you might see an error if this Z coordinate is not yet set:

![Z missing Error](https://user-images.githubusercontent.com/9963310/131219923-afa8f871-2773-4f16-9532-67028acb96b4.png)

You might have to change your routine when setting up new feeders, always probe and enter the Z first. For simple feeders, you can probably just copy the Z coordinate over (and know it by heart, after a while). 
 