# Basic Information

## Names and Details
- `emmanuelle`
    - Name: anikaraspberrypi.wellesley.edu
    - IP Address: 149.130.206.37
    - must access remotely (eg. through [ssh](https://www.raspberrypi.com/documentation/computers/remote-access.html#ssh))
- `doudna`
    - Name: anikaraspberrypi2.wellesley.edu
    - Address: 149.130.206.38    
    - connected to RPi Box
    - connected to touch screen monitor and keyboard
    - can also access remotely (eg. through ssh)

# Using the RPi Camera

## Taking Photos/Videos

The [RPiCamera](https://github.com/Klepac-Ceraj-Lab/RPiCamera) repository contains all the necessary code to use the RPi Camera.
Detailed information on how to use the repository and run the scripts can be found in the [repository README](https://github.com/Klepac-Ceraj-Lab/RPiCamera/blob/main/README.md) and the [scripts README](https://github.com/Klepac-Ceraj-Lab/RPiCamera/blob/main/scripts/README.md) respectively.

# Using the RPi Box

## Features of Box
 - box
    - door
    - platform
        - white base that fits on shelves
        - optional black base
    - shelves for platform
    - led lights
        - bright white, adjustable with dial on left side box, in square spiral under top
        - warm white, not adjustable, on top edges of box, USB plugs into pi
    - camera-box adaptors (white discs that fit in hole on top of box)
        - 6mm camera (small inner radius)
        - 16mm camera (larger inner radius)
- pi
    - pi
    - camera
    - mini touchscreen monitor
    - keyboard
    - breadboard with button

## Setting Up an Object
- clean interior of box and platform thoroughly with ethanol
    - **Note:** The door has a tendency to swing closed. If you need to keep the door open, just tape it to a surface.
- place platform on desired shelf
    - make sure matte side of white base faces up
    - the white base is almost but not quite square so one side fits more snugly than the other
        - depending on what you need to use the box for, either works, one is just more secure and one is more flexible
    - if using the black base, secure it to the white base with tape
- place object on platform
- place camera with desired lens into the adaptor, with lens facing down
- preview camera view by running `preview.py` (refer to [Taking Photos/Videos] (**link**)
    - note for orienting the view: the side where the ribbon comes out of the camera board is the bottom
- adjust things as needed
    - put platform on diff shelf
    - turn on leds
        - can adjust brightness of bright white leds
        - if the object is reflective it may reflect the shadows in the spaces between the spiral of bright white leds. in that case using side lights may be better
    - adjust focus and aperture
        - to adjust: unscrew/loosen knob
        - to fix: screw/tighten knob
        - knob nearest to board (labelled with "NEAR" and "FAR") adjusts focus
        - knob nearest to lens (labelled with "OPEN" and "CLOSE") adjusts aperture
            - first find proper lighting with leds
            - if and only if necessary, adjust aperture
            - fix focus knob first to make adjusting aperture easier
- secure camera settings
    - fix/tighten knobs
    - gently tape camera into place
- close door
- take photo(s)/video(s)!

<!--

# Using the Code

All code is run using the [command-line interface](https://en.wikipedia.org/wiki/Command-line_interface) in terminal.
(The terminal icon on RPi's is a black rectangle with ">_" inside and blue bar on top )
For a quick guide on how to use command line, see [Lesson 1](http://bisc195.wellesley.edu/lessons/Lesson01/) of Kevin's BISC 195.

For the tutorials below, the RPiCamera repository is in the `~/Desktop/` directory of `anika`.
In addition, all files should be saved to `~/Pictures/` to consolidate and easily keep track of media.

## To Preview Photo (for 60sec)
- Execute `$ python <path to RPiCamera>/RPiCamera/scripts/preview.py`
    - Examples:
        - From home: `anika@raspberrypi:~ $ python ~/Desktop/RPiCamera/scripts/preview.py`
        - From RPiCamera: `anika@raspberrypi:~/Desktop/RPiCamera $ python scripts/preview.py`
- Run command as many times as needed to optimize photo

## To Take a Photo
- Check that directory to which you want to send the photo exists
- If not, make a directory within `~/Pictures/`
    - Examples:
        - From home: `anika@raspberrypi:~ $ mkdir ~/Pictures/directory1`
        - From Pictures: `anika@raspberrypi:~/Pictures $ mkdir directory2`
    - **Note**: Directory names should not contain any spaces or special characters. If you would like words to be separated use a hyphen "-" or underscore "_".
- Execute: `$ python <path to RPiCamera>/RPiCamera/scripts/photo.py <path to dir where photo will go>/`
    - Examples:
        - From home: `anika@raspberrypi:~ $ python ~/Desktop/RPiCamera/scripts/photo.py ~/Pictures/directory1/`
        - From RPiCamera: `anika@raspberrypi:~/Desktop/RPiCamera $ python scripts/photo.py ~/Pictures/directory1/`
        - From directory: `anika@raspberrypi:~/Pictures/directory1 $ python ~/Desktop/RPiCamera/scripts/photo.py ./`
    - **Note**: The path to directory where photo will go should always end in "/". If not, the directory name will be added onto the photo name, and the photo will go into the parent directory. -->
