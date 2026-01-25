# Project Blindsight
This is a project to create technology that enables a blind person to navigate 3-dimensional spaces.

The system operates by mapping spatial data derived from a depth sensor to multiple orthogonal properties of sound, enabling the user to infer three-dimensional structure through auditory perception.

The project will combine several technologies into a package to accomplish its goal:
1. A depth sensor/Lidar, such as the Orbbec Femoto Bolt
2. A logic board/computer; for processing signals from the sensor, such as a Raspberry Pi or ESP32
3. A listening device for the user, such as headphones

Those components will be combined in a way that creates a wearable device for the user. There will obviously be additional components such as a battery so that the device will have enough power to run for an extended period of time, adjustable strap, a camera (for tasks like determining colors), and padding so that the wearable device will be comfortable. See the image below for an example render of what the device might look like:

<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/5a6611be-9d35-479b-bbbf-284aa1b37d11" />


## How the device works

As for how the device functions, the logic board receives information from the Lidar and converts that into sound (using either an API or data format like JSON). The sound will be specially formatted in such a way that the user can interpret it into information that can be used to navigate a 3-dimensional space.

There are 5 different properties of sound that we can use:
1. Volume: Measures distance. The louder an object is, the closer it is to the user.
2. Pitch: The Y-Axis of the field of vision. Pitch is the "notes" you would see on a piece of sheet music. Pitches such as A, B, C, D, E, F, and G would form an octave, and multiple octaves could be used to define the Y-Axis. A lower note, like a Low-C would register as being lower vertically in the user's field of vision. A high note, like a High-E would register as higher in the user's field of vision.
3. Timing: The X-Axis of the field of vision. The X-Axis is encoded temporally, scanning from left to right like a radar sweep. This temporal scanning encodes horizontal position as a function of time.
4. Timbre: Potentially used for color. Timbre can be thought of as the audio equivalent of color; it is the property of sound that allows the listener to distinguish between a violin and a trumpet.
5. Tone: Potentially used for texture. Tone is the "quality" of the sound, so a clear tone could signify a smooth surface, whereas a fuzzy tone could signify a furry surface.

The descriptions above are intended to illustrate one possible approach. Alternative mappings, encodings, and implementations are possible within the scope of the project.

Here's an example of how that all fits together: Imagine a loud sound that covers the Y-Axis, followed by a period of silence (broken by an upside down U sound "shape" near the lower pitches), then another loud sound that covers the entire Y-Axis again. You'd be "looking" at a hallway with a table in it. The loud beginning and ending sounds are the walls to the left and right of you, the silence denotes a large empty area in between them, and that upside down U sound shape is the table.

Here is a visual example of what the audio experience might sound like:

<img width="400" height="376" alt="image" src="https://github.com/user-attachments/assets/1dd23ff9-cfa4-4652-8365-789db974a7f3" />

Here is what a cave with stalactites and stalagmites could sound like:

<img width="400" height="376" alt="image" src="https://github.com/user-attachments/assets/fa9f5738-c8b6-4553-88c1-31f16bf162fa" />

A few trees in a park:

<img width="400" height="376" alt="image" src="https://github.com/user-attachments/assets/376a80d6-edd0-4330-ba1b-1c84a0396e43" />

Or even looking down at your own legs or feet; the device follows your field of vision:

<img width="400" height="376" alt="image" src="https://github.com/user-attachments/assets/4fb8b0a4-bb9a-4697-b681-36a74e72f439" />

The device should allow for various configuration options:
- Adjust the volume (preferably a low enough volume that the user can still listen to conversations or ambient sounds).
- The speed of the X-Axis: Users who are beginning to use the device may need to turn down the scan rate of the X-Axis so that they can interpret the information. Experienced users will likely speed up the scan rate, similar to how visually impared users turn up the speed of screen readers.
- The Y-Axis range: A higher amount of notes should give a higher fidelity to the vertical field of vision, but there are various factors that can affect the ability to hear notes on the extreme high or extreme low areas of the scale, so the user should be able to adjust the range of the Y-Axis accordingly.

## How color works with the device

For color, Project Blindsight uses HSV (Hue, Saturation, Value) colors and converts them into sound using specific instrument "personalities." For example, hues could be arranged like this:

### Hue

- Red: Horns/Brass, a red hue that is lower on the Y-Axis would be similar to a tuba; a red hue that is higher on the Y-Axis would sound more like a trumpet.
- Green: Woodwinds, a green hue that is lower on the Y-Axis could be a bit like a bassoon; a green hue that is higher on the Y-Axis would sound more like a flute.
- Blue: Strings, a blue hue that is lower on the Y-Axis would be like a cello; a blue hue that is higher on the Y-Axis would be similar to a violin.

The different hues mapped to the Y-Axis could be mapped to different instruments, but they don't necessarily need to be. The digital sound that the user hears could take a trumpet or a flute, and lower its pitch to levels that would be impossible for a human to play.

### Saturation

You can think of saturation as the level of vibrant color vs how washed out it is. As for how this interacts with color in Project Blindsight, this could be represented by the sound of a voice.

### Value

Value is the amount of brightness vs darkness. This would be represented by a sound like a piano (or possibly a gong).

HSV can be imagined as a cone, but it's easier to imagine it as 3 sliders (Hue, Saturation, and Value). The values on here can be mapped to Hexidecimal values that are often used for digital colors.

Here are a few examples of what that might look and sound like:

* <img width="10" height="10" alt="image" src="https://github.com/user-attachments/assets/793150c8-b84a-45f9-bf2e-95814a9a0dba" /> #FF0000: Red, a sound that is all brass/horn.
* <img width="10" height="10" alt="image" src="https://github.com/user-attachments/assets/3b466287-3017-4088-b162-09ea6388c5cf" /> #00FF00: Green, a sound that is all woodwind.
* <img width="10" height="10" alt="image" src="https://github.com/user-attachments/assets/a25901a9-15b9-43b1-9af1-7cc1334c3b4a" /> #0000FF: Blue, a sound that is all strings.
* <img width="10" height="10" alt="image" src="https://github.com/user-attachments/assets/94bcaf09-d1db-449f-a07c-28a726c06495" /> #FFFFFF: White, a sound that is all vocal.
* <img width="10" height="10" alt="image" src="https://github.com/user-attachments/assets/a977b320-9cc2-48e4-b32c-5940e8ec5d5f" /> #000000: Black, a sound that is all piano.
* <img width="10" height="10" alt="image" src="https://github.com/user-attachments/assets/edc8f10d-db15-41a6-bdd7-a40bcc16848c" /> #FF00FF: Purple, a sound that mixes brass and strings (red and blue).
* <img width="10" height="10" alt="image" src="https://github.com/user-attachments/assets/6cf75700-3553-4ad5-b233-0d2581b818af" /> #FFFF00: Yellow, a sound that mixes brass and woodwind (red and green).
* <img width="10" height="10" alt="image" src="https://github.com/user-attachments/assets/189a2fff-803b-4a74-9224-7096056b805c" /> #FFB45E: A pastel orange, mostly red and green with a little bit of blue mixed in. It has a medium saturation with a high value. That translates to something with quite a bit of brass and woodwinds, and a hint of strings. There's also a little bit of a vocal undertone, but no piano.

The Hex values can be converted to HSV to determine what percentage of the sound has each element mixed in, then that can be mapped to the pitch on the Y-Axis.

To determine what color each sector of the X/Y axis should show, a camera on the device could measure the average of the colors within the coordinates of the grid, then return that value as a Hex color.

Once again, the descriptions above are intended to illustrate one possible approach. Alternative mappings, encodings, and implementations are possible within the scope of the project.

## License Information
- Software for this project is licensed under the Apache 2.0 license
- Hardware for this project is licensed under the CERN Open Hardware Licence Version 2 - Permissive license
- Documentation for this project is licensed under the CC-BY 4.0 license: https://creativecommons.org/licenses/by/4.0/
