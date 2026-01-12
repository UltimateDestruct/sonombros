# Project Blindsight
This is a project to create technology that enables a blind person a navigate 3-dimensional spaces.

The project will combine several technologies into a package to accomplish its goal:
1. A depth sensor/Lidar, such as the Orbbec Femoto Bolt
2. A logic board for processing signals from the sensor, such as a Raspberry Pi or ESP32
3. A listening device for the user, such as headphones

Those components will be combined in a way that creates a wearable device for the user. There will obviously be additional components such as a battery, adjustable strap, and padding so that the wearable device will be comfortable and have enough power to run for an extended period of time. See the image below for an example render of what the device might look like:

<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/0b9a4de2-8408-47dd-85ab-bf5e9de13d22" />

As for how the device functions, the logic board receives information from the Lidar and converts that into sound (using either an API or data format like JSON). The sound will be specially formatted in such a way that the user can interpret it into information that can be used to navigate a 3-dimensional space.

There are 5 different properties of sound that we can use:
1. Volume: Measures distance. The louder an object is, the closer it is to the user.
2. Pitch: The Y-Axis of the field of vision. Pitch is the "notes" you would see on a piece of sheet music. Pitches such as A, B, C, D, E, F, and G would form an octave, and multiple octaves could be used to define the Y-Axis. A lower note, like a Low-C would register as being lower vertically in the user's field of vision. A high note, like a High-E would register as higher in the user's field of vision.
3. Timing: The X-Axis of the field of vision. The X-Axis will periodically scan from left to right, kind of like a radar.
4. Timbre: Potentially used for color. Timbre can be thought of as the audio equivalent of color; it is the property of sound that allows the listener to distinguish between a violin and a trumpet.
5. Tone: Potentially used for texture. Tone is the "quality" of the sound, so a clear tone could signify a smooth surface, whereas a fuzzy tone could signify a furry surface.

Here's an example of how that all fits together: Imagine a loud sound that covers the Y-Axis, followed by a period of silence, then another loud sound that covers the entire Y-Axis again. You'd be "looking" at a hallway. The loud beginning and ending sounds are the walls to the left and right of you, and the silence denotes a large empty area in between them.

The device should allow for various configuration options:
- Adjust the volume (preferably a low enough volume that the user can still listen to conversations or ambient sounds).
- The speed of the X-Axis: Users who are beginning to use the device may need to turn down the scan rate of the X-Axis so that they can interpret the information. Experienced users will likely speed up the scan rate, similar to how visually impared users turn up the speed of screen readers.
- The Y-Axis range: A higher amount of notes should give a higher fidelity to the vertical field of vision, but there are various factors that can affect the ability to hear notes on the extreme high or extreme low areas of the scale, so the user should be able to adjust the range of the Y-Axis accordingly.
