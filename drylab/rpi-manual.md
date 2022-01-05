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

# Using the RPi Box

## Features
 - The Box
    - Hinged door
        - Closing mechanism is a protected screw that fits into the hole in a protruding hinge
    - Shelves at various hights
    - Adjustable white platform that fits on shelves
        - Optional black base for dark background
    - Two sets of LED lights:
        - Bright white, secured in square spiral under top of box, dial on left side box rotates to turn on/off and adjust intensity
        - Warm white, secured on top edges of box, USB plugs into pi to turn on
    - Two camera-box adaptors (white discs that fit in hole on top of box):
        - One for 6mm RPi camera (small inner radius)
        - One for 16mm RPi camera (larger inner radius)
- The Raspberry Pi (RPi)
    - Raspberry Pi (in its case)
    - Camera
    - Mini touchscreen monitor and keyboard
    - External button on breadboard (for when using [`buttonphoto.py`](https://github.com/Klepac-Ceraj-Lab/RPiCamera/tree/main/scripts#buttonphoto))

## Setting Up an Object
1. Clean interior of box and platform thoroughly with ethanol
    - *The door has a tendency to swing closed. If you need to keep the door open, tape it to a surface or prop it behind another object.*
2. Place platform on desired shelf
    - Make sure matte side of white base faces up
    - *The white base is almost but not quite square so one side fits more snugly than the other. Depending on what you need to use the box for, either works; one orientation is just more secure and one is more flexible.*
    - If using the black base, secure it to the white base with tape
3. Place object on platform
4. Place camera with desired lens into the adaptor, with lens facing down
5. Preview camera view by running [`preview.py`](https://github.com/Klepac-Ceraj-Lab/RPiCamera/tree/main/scripts#preview)
    - *For orienting the view - the side where the ribbon comes out of the camera board is the bottom of the photo*
6. Adjust things as needed
    - Put platform on different shelf
    - Turn on leds
        - *If the object is reflective it may reflect the spiral of bright white leds. in that case using side lights may be better*
    - Adjust focus and aperture on the camera lens
        - **Only adjust one aspect at a time. Leave the other knob fixed. This makes adjusting easier and faster.**
        - To adjust: unscrew/loosen knob
        - To fix: screw/tighten knob
        - Knob nearest to board (labelled with "NEAR" and "FAR") adjusts focus
        - Knob nearest to lens (labelled with "OPEN" and "CLOSE") adjusts aperture
            - First find proper lighting with leds
            - If and only if necessary, adjust aperture
7. Secure camera and box settings
    - Fix/tighten knobs
    - Gently tape camera into place
    - If necessary, tape object down or mark it's placement
8. Close and secure door
    - Make sure the screw is fitted securely in the hole

## Taking Photos/Videos

The [RPiCamera](https://github.com/Klepac-Ceraj-Lab/RPiCamera) repository contains all the necessary code to take photos and videos.
Detailed information on how to use the repository and run its scripts can be found in the [repository README](https://github.com/Klepac-Ceraj-Lab/RPiCamera/blob/main/README.md) and the [scripts README](https://github.com/Klepac-Ceraj-Lab/RPiCamera/blob/main/scripts/README.md) respectively.
