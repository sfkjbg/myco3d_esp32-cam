
How-To Guide: Getting Started with ESP32-CAM

This guide will help you set up and get started with the ESP32-CAM module, a versatile camera module with an integrated ESP32 chip that supports Wi-Fi and Bluetooth connectivity.
Table of Contents

    Prerequisites
    Hardware Setup
    Software Setup
    Uploading a Basic Camera Sketch
    Accessing the Camera Stream
    Conclusion

1. Prerequisites

Before starting, ensure you have the following components:

    ESP32-CAM module
    FTDI programmer (USB to UART converter)
    Breadboard (optional)
    Jumper wires
    Micro-USB cable
    External 5V power supply (optional)

2. Hardware Setup

Follow these steps to set up the hardware connections for the ESP32-CAM module:

    Connect the FTDI programmer to the ESP32-CAM module using jumper wires:
        GND to GND
        VCC to 5V
        TX to U0R
        RX to U0T

    To enable flashing mode, connect the GPIO0 pin to the GND pin. You can use a jumper wire or a pushbutton for this purpose.

    Connect the FTDI programmer to your computer using a Micro-USB cable.

Note: During normal operation, the ESP32-CAM module requires a stable 5V power supply. If you encounter issues during normal operation, consider using an external 5V power supply instead of powering the module through the FTDI programmer.
3. Software Setup

    Install the Arduino IDE on your computer.

    Open the Arduino IDE and go to File > Preferences. In the "Additional Boards Manager URLs" field, add the following URL:


    ```https://dl.espressif.com/dl/package_esp32_index.json
```

    Go to Tools > Board > Boards Manager. Search for "ESP32" and install the "esp32" package by Espressif Systems.

    Select the ESP32-CAM board by going to Tools > Board > ESP32 Arduino > AI Thinker ESP32-CAM.

    Configure the upload settings by going to Tools and setting the following options:
        Upload Speed: "115200"
        Port: Select the appropriate COM port for your FTDI programmer

4. Uploading a Basic Camera Sketch

    In the Arduino IDE, go to File > Examples > ESP32 > Camera > CameraWebServer.

    In the CameraWebServer.ino sketch, locate the section with multiple camera configurations. Uncomment the appropriate configuration for the AI Thinker ESP32-CAM module:

    ```#elif defined(CAMERA_MODEL_AI_THINKER)
        #define PWDN_GPIO_NUM    32
        #define RESET_GPIO_NUM   -1
        #define XCLK_GPIO_NUM     0
        #define SIOD_GPIO_NUM    26
        #define SIOC_GPIO_NUM    27
        #define Y9_GPIO_NUM      35
        #define Y8_GPIO_NUM      34
        #define Y7_GPIO_NUM      39
        #define Y6_GPIO_NUM      36
        #define Y5_GPIO_NUM      21
        #define Y4_GPIO_NUM      19
        #define Y3_GPIO_NUM      18
        #define Y2_GPIO_NUM       5
        #define VSYNC_GPIO_NUM   25
        #define HREF_GPIO_NUM    23
        #define PCLK_GPIO_NUM    22
        ```


    Double-check that the selected board, upload speed, and port are correct in the Tools menu.

    Press and hold the GPIO0 button or connect GPIO0 to GND to enable flashing mode.

    Click the "Upload" button (arrow icon) in the Arduino IDE to compile and upload the sketch to the ESP32-CAM module.

    After the upload is complete, disconnect GPIO0 from GND or release the GPIO0 button.

    Press the "Reset" button on the ESP32-CAM module or cycle the power to restart the module.

5. Accessing the Camera Stream

    Open the Serial Monitor in the Arduino IDE by going to Tools > Serial Monitor.

    Set the baud rate to "115200" in the Serial Monitor.

    Press the "Reset" button on the ESP32-CAM module or cycle the power to restart the module.

    Observe the Serial Monitor output. The ESP32-CAM module will connect to Wi-Fi and start the camera server. Once the camera server is running, it will display an IP address. Make a note of this IP address.

    Open a web browser on a device connected to the same Wi-Fi network as the ESP32-CAM module.

    Enter the IP address noted earlier in the browser's address bar and press Enter.

    The ESP32-CAM web interface should now be accessible. You can view the live camera stream, capture still images, and adjust various camera settings.

6. Conclusion

In this guide, you've learned how to set up the hardware and software for the ESP32-CAM module, upload a basic camera sketch, and access the camera stream through a web interface. You can now use the ESP32-CAM module to build various projects, such as security cameras, smart doorbells, and other IoT applications.













####################### 

Title: Comprehensive ESP32-Camera Module Manual and Shortcuts

Table of Contents:
1. Introduction
2. Features
3. Hardware Requirements
4. Software Requirements
5. Wiring and Pin Configuration
6. Basic Usage and Commands
   6.1. Camera Configuration
   6.2. Capturing an Image
   6.3. Streaming Video
   6.4. Face Recognition and Detection
   6.5. Saving Images to SD Card
7. Advanced Features and Applications
8. Troubleshooting
9. Resources and References

1. Introduction
(Refer to the previous response.)

2. Features
(Refer to the previous response.)

3. Hardware Requirements
(Refer to the previous response.)

4. Software Requirements
(Refer to the previous response.)

5. Wiring and Pin Configuration
(Refer to the previous response.)

6. Basic Usage and Commands

6.1. Camera Configuration
Camera settings such as resolution, format, and quality can be adjusted using the camera configuration structure. The following example demonstrates how to set up a basic camera configuration in Arduino IDE:
```python
#include "esp_camera.h"

camera_config_t config;

void setupCamera() {
  config.ledc_channel = LEDC_CHANNEL_0;
  config.ledc_timer = LEDC_TIMER_0;
  config.pin_d0 = 5;
  config.pin_d1 = 18;
  config.pin_d2 = 19;
  config.pin_d3 = 21;
  config.pin_d4 = 36;
  config.pin_d5 = 39;
  config.pin_d6 = 34;
  config.pin_d7 = 35;
  config.pin_xclk = 0;
  config.pin_pclk = 22;
  config.pin_vsync = 25;
  config.pin_href = 23;
  config.pin_sscb_sda = 26;
  config.pin_sscb_scl = 27;
  config.pin_pwdgitn = 32;
  config.pin_reset = -1;
  config.xclk_freq_hz = 20000000;
  config.pixel_format = PIXFORMAT_JPEG;
  config.frame_size = FRAMESIZE_SVGA;
  config.jpeg_quality = 12;
  config.fb_count = 1;

  // Initialize the camera
  esp_err_t err = esp_camera_init(&config);
  if (err != ESP_OK) {
	Serial.printf("Camera init failed with error 0x%x", err);
	return;
  }
}
```
- config.pixel_format: Set the pixel format (e.g., PIXFORMAT_JPEG, PIXFORMAT_RGB888, PIXFORMAT_GRAYSCALE).
- config.frame_size: Set the frame size (e.g., FRAMESIZE_QVGA, FRAMESIZE_VGA, FRAMESIZE_SVGA).
- config.jpeg_quality: Set the JPEG quality (1-63, lower values mean higher quality and larger image size).

6.2. Capturing an Image
(Refer to the previous response for a basic example.)

6.3. Streaming Video
(Refer to the previous response for a basic example.)

6.4. Face Recognition and Detection
To use face recognition and detection, the dl_lib.h library and a pre-trained model are required. Follow these steps to implement basic face recognition:

1. Include the necessary libraries:
```
#include "esp_camera.h"
#include "fd_forward.h"
#include "fr_forward.h"
#include "dl_lib.h"
```

2. Initialize the face detection and recognition models:
```
mtmn_config_t mtmn_config
```



1. Include the necessary libraries:
```
#include "esp_camera.h"
#include "fd_forward.h"
#include "fr_forward.h"
#include "dl_lib.h"
```


2. Initialize the face detection and recognition models:
```
mtmn_config_t mtmn_config = mtmn_init_config();
dl_matrix3du_t *aligned_face = dl_matrix3du_alloc(1, FACE_WIDTH, FACE_HEIGHT, 3);


face_id_list_init(&id_list, FACE_ID_SAVE_NUMBER, FACE_WIDTH, FACE_HEIGHT);

// Load the face detection model
face_detection_init("fd_forward");

// Load the face recognition model
face_recognition_init("fr_forward");
```
3. Capture an image and perform face detection:
```
camera_fb_t *fb = esp_camera_fb_get();

if (!fb) {
  Serial.println("Failed to capture image");
  return;
}

box_array_t *net_boxes = face_detect_net_boxes(fb, mtmn_config);

if (!net_boxes) {
  Serial.println("No faces detected");
} else {
  Serial.printf("Detected %d faces\n", net_boxes->len);
}

```
4. Perform face recognition on the detected faces:
```
for (int i = 0; i < net_boxes->len; i++) {
  fptp_t similarity = {0};

  // Align the face in the image
  face_align_net(aligned_face, fb, net_boxes->box[i].box_p);

  // Perform face recognition
  int matched_id = recognize_face(aligned_face, &id_list, &similarity);

  if (matched_id >= 0) {
	Serial.printf("Face matched with ID %d, similarity: %f\n", matched_id, similarity);
  } else {
	Serial.printf("Face not recognized, similarity: %f\n", similarity);
  }
}
```
5. Don't forget to release the allocated resources after use:
```
dl_matrix3du_free(aligned_face);
free(net_boxes);
esp_camera_fb_return(fb);
```


6. Saving Images to SD Card

To save images to an SD card, follow these steps:

1. Include the necessary libraries:
```
#include "FS.h"
#include "SD_MMC.h"
```
2. Initialize the SD card:
```
void setupSDCard() {
  if (!SD_MMC.begin()) {
	Serial.println("Failed to initialize SD card");
	return;
  }
  Serial.println("SD card initialized");
}
```

3. Save the captured image to the SD card:
```
void saveImageToSDCard(camera_fb_t *fb, const char *filename) {
  File file = SD_MMC.open(filename, FILE_WRITE);

  if (!file) {
	Serial.println("Failed to open file for writing");
	return;
  }

  file.write(fb->buf, fb->len);
  file.close();
}

```
