# Basic Information

## Names and Details
- `emmanuelle`
    - IP: 149.130.206.37
    - must connect remotely (eg. through [ssh](https://www.raspberrypi.com/documentation/computers/remote-access.html#ssh))
- `doudna`
    - IP: 149.130.206.38
    - connected to RPi Box
    - connected to touch screen monitor and keyboard

## Login
- username: anika
- password: humanm1cr0b10m3

# [RPiCamera Repository](https://github.com/Klepac-Ceraj-Lab/RPiCamera)

The RPiCamera Repository contains all the necessary code to use the RPi Camera.
Detailed information on how to use the repository and run the scripts can be found in the [repository README](https://github.com/Klepac-Ceraj-Lab/RPiCamera/blob/main/README.md) and the [scripts README](https://github.com/Klepac-Ceraj-Lab/RPiCamera/blob/main/scripts/README.md) respectively.

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
    - **Note**: The path to directory where photo will go should always end in "/". If not, the directory name will be added onto the photo name, and the photo will go into the parent directory.
