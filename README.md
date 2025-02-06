# TinyControllerWebDisplay
A joypad viewer for [OBS](https://obsproject.com). Add as a browser source.

For anti-fingerprinting, the [Gamepad API](https://developer.mozilla.org/en-US/docs/Web/API/Gamepad_API) does not present any controllers until a button has been pressed. As such, TinyControllerWebDisplay will not show up until a button on a controller has been pressed. Once a button on a controller has been pressed, TinyControllerWebDisplay will display the state of that controller and only that controller until it is restarted. To display a specific controller number, append a fragment after the URL; `#0` at the end for the first controller, `#1` for the second, etc. If you would prefer to display a different controller than the ones listed below, the image assets can be replaced, so long as the filenames are kept. However, the trigger arcs will need to be in the same place, and all moving components will still move in the same directions by the same amount.

TinyControllerWebDisplay takes two optional URL parameters: `?color=F00&type=bar`. To use these in OBS, you need to uncheck the "Local file" option and prefix the filepath with `file://` (add an extra `/` on Windows: `file:///C:...`).

To display a DualShock 4 v2 instead of an Xbox One Elite pad, replace `bar` with `ps4`, `ds4`, `ds4_v2`, or `ds4_rev2`; eg `type=ds4`.

To display a DualSense, use `type=dualsense`, `ds5`, or `ps5`.

To display a fightstick, use `type=fightstick`, `fight_stick`, `arcadestick`, or `arcade_stick`. If your stick maps the shoulder bumpers to the top row of buttons, add `&bumpers_up=true` to the end of the URL.

To display a hitbox, use `type=hitbox`, `leverless`, `stickless`, or `slab`.

To display a Smash rectangle, use `type=rectangle`, `b0xx`, `frame1`, `gram`, or `smashbox`. Please note that this input viewer is based upon the [20-button  Melee input mode available in this fork of Haybox](https://github.com/UMS-Ultra/BubbleBox-Firmware/blob/master/src/modes/Melee20Button.cpp); if you are using a different input mode, the mod buttons may not display correctly. (Support for additional input modes coming soon...) For WASD mode, append `&wasd_mode=true` to the end of the URL.

For fightstick, hitbox, or rectangle displays, append `&transparent=true` to the URL to have a transparent background.

To change the color of the light on the pad displays or the buttons and sticktop on the stick/box displays, replace `F00` with a different [hexcode](https://www.codeconquest.com/hex-color-codes/). TCWD understands `RGB`, `RGBA`, `RRGGBB`, and `RRGGBBAA` color formats.


HIGHER RESOLUTION GUIDE
-------------------------------

To make it 1920x1080 instead of 57x37 you will need to make a few changes to the code and also create some new GIF images. 

1) In the html file TinyControllerWebDisplay-master/tiny-controller-display.html you will need to edit the <canvas> tags to be 1920 x 1080.

2) In the js file TinyControllerWebDisplay-master/tiny-controller-display.js youll need to change line 260 to the new resolution. Here is the line so you can search for it easier
const width = 57, height = 37, triggerArcHeight = 15; 

3) You will then need to make new GIF files for the faceplate and all of the different button activations. Make sure the active buttons GIFs have a white background so you can still take advantage of the color html parameter later on!
The new GIF files need to go in TinyControllerWebDisplay-master\sprites\rectangle.
I also recommend Canva pro for this as its easy to create GIFs with transparent backgrounds, but you can use any software you like. 
It is important to keep the same naming conventions unless you are going to edit the code further. (That is necessary for allowing L3 R3 Left bumper select etc. to activate).

The active faceplates will need to be named faceplate & faceplate_transparent. But you can keep unused faceplates with another name if you'd like to try out a few others or swap between them by renaming them and refreshing the page. I included some faceplate examples if you'd like to use those.

For my fellow Rivals 2 mode players (on Gram firmware 1.0): you will need to adjust the code to swap left right, c right and c left, and dpad left right. otherwise it will appear wrong. This project was made for the Melee mode so it doesn't work perfectly for Rivals 2. Also mod x and mod y will not display properly once in game. 


SETUP
---------
Now for setting up this software, I find the easiest way is to create the url and just paste that into firefox. Afterwards use OBS to capture the window, or if you use a 2nd pc you can either use a capture card to send it to the other pc or NDI. 

This approach saves you from having to rely on any other default software and you can use an OBS color key filter to remove the background if you want to.

If you are using a window capture I recommend setting the page to be 90% zoomed in and then use an OBS filter to crop the borders. 

Here is an example URL with WASD mode:
file:///D:/TinyControllerWebDisplay-master/tiny-controller-display.html?type=rectangle&wasd_mode=true&color=F00

After that you can add the source to whatever scene and size it accordingly.

Enjoy the input display!