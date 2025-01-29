# main guide
https://blog.cloudflare.com/building-a-pet-cam-using-a-raspberry-pi-cloudflare-tunnels-and-teams/

## bug
- v4l2_fps_set: Error setting fps. Return code -1
  - https://github.com/Motion-Project/motion/issues/1720
    - https://motion-project.github.io/motion_config.html#basic_setup_picam
      

```The raspberry Pi camera is set up via an application called libcamera. libcamera provides access to the camera as a v4l2 device but this interface is only available when using a special application. Users must run Motion using the command libcamerify motion and then specify the /dev/videoX device in the Motion configuration file.```
  - apt install libcamera-tools -y
  - libcamerify motion
    - v4l2-compat.so from LD_PRELOAD cannot be preloaded: ignored.
      - sudo apt-get install motion
        sudo apt-get install libcamera-v4l2
        sudo apt-get install libcamera-tools
  - 

- rpicam doc
  - https://datasheets.raspberrypi.com/camera/picamera2-manual.pdf
    - python example to test cam
      - RuntimeError: Failed to reserve DRM plane
        - https://forums.raspberrypi.com/viewtopic.php?t=365473
          - ```picam2.start_preview(Preview.NULL)```

      
```
from picamera2 import Picamera2, Preview
import time
picam2 = Picamera2()
camera_config = picam2.create_preview_configuration()
picam2.configure(camera_config)
picam2.start_preview(Preview.DRM)
picam2.start()
time.sleep(2)
picam2.capture_file("test.jpg")
```

