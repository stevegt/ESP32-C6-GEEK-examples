# ESP32-C6-GEEK Demo Repository

This repository is a collection of vendor-style demonstration projects for the Waveshare ESP32-C6-GEEK board. It includes Arduino sketches, ESP-IDF sample applications, bundled Arduino libraries, a few sample images, and one prebuilt firmware image.

The examples are mostly independent of each other. Treat each example directory as its own small project.

## Repository Layout

- `Arduino/examples/` contains 17 Arduino sketches that exercise the board LCD, button, BLE, Wi-Fi, SD card, MQTT, UART, ADC, and sensor interfaces.
- `Arduino/libraries/` contains the Arduino libraries expected by the sketches in this repo.
- `Arduino/pic/` contains sample JPEGs that can be copied onto a microSD card for the SD + LCD demo.
- `ESP-IDF/` contains 6 standalone ESP-IDF projects.
- `Firmware/` contains a prebuilt binary image.

## Hardware You May Need

Different demos need different peripherals. Depending on which example you want to run, you may need:

- the ESP32-C6-GEEK board itself,
- a USB data cable,
- a microSD card,
- a BME68x I2C sensor,
- a phone or computer for BLE tests,
- a Wi-Fi network or a second client device,
- an MQTT broker or access to the configured broker.

## Arduino Quick Start

Use this workflow for the sketches under `Arduino/examples/`:

1. Install the Arduino IDE and configure ESP32 board support for the ESP32-C6-GEEK platform.
2. Make sure the libraries in `Arduino/libraries/` are available to your Arduino sketchbook environment.
3. Open the example sketch you want to run.
4. Select the ESP32-C6 target and the correct serial port.
5. Edit any hardcoded credentials, IP addresses, broker settings, or device IDs before uploading.
6. Upload the sketch and open Serial Monitor when the example mentions serial output.

Notes:

- Many sketches use `115200` baud on the serial port.
- The `Readme.txt` files included with a few Arduino examples mainly record LCD pin mappings.
- The networked sketches are demo-oriented and often ship with hardcoded settings that you should replace before use.

## Arduino Examples

### Basic I/O and Sensor Demos

- `Arduino/examples/01_OneButton`  
  Shows single-click, double-click, and long-press events on the LCD.  
  How to use: upload it, then press the onboard button with short, double, and long presses to watch the label change.

- `Arduino/examples/02_ADC_Read`  
  Reads ADC channel 0 and prints both raw and millivolt values.  
  How to use: connect a safe analog input source, upload the sketch, open Serial Monitor at `115200`, and vary the input to watch the readings change.

- `Arduino/examples/03_IIC_BME68X_Sensor`  
  Polls a BME68x sensor over I2C and prints temperature, pressure, humidity, and gas resistance.  
  How to use: wire a BME68x sensor, confirm the expected I2C address, upload the sketch, and watch the serial output.

- `Arduino/examples/04_UART0`  
  Simple serial echo test for newline-terminated input.  
  How to use: upload it, open Serial Monitor at `115200`, send a line of text, and verify that the same text is echoed back.

### LCD and Storage Demos

- `Arduino/examples/05_LCD_Button`  
  Displays built-in images on the LCD and changes the screen state based on button presses.  
  How to use: upload it, short-press the button to cycle images, and long-press to turn off the backlight.

- `Arduino/examples/06_LCD_Time`  
  Connects to Wi-Fi, synchronizes time, and shows date/time on the LCD.  
  How to use: edit the Wi-Fi credentials and time settings in the sketch, upload it, then wait for Wi-Fi and NTP synchronization.

- `Arduino/examples/07_SD_Test`  
  Exercises microSD mounting plus directory and file operations.  
  How to use: insert a microSD card, upload the sketch, open Serial Monitor, and review the filesystem and throughput test output.

- `Arduino/examples/08_SD_LCD`  
  Loads JPEGs from microSD and renders them on the LCD, with a fallback to built-in images.  
  How to use: copy `.jpg` or `.jpeg` files to the root of a microSD card, insert the card, upload the sketch, and use short presses to cycle images. The sample files in `Arduino/pic/` are a reasonable starting point.

### BLE Demos

- `Arduino/examples/09_BLE_LCD`  
  BLE text demo that mirrors received or transmitted text on the LCD.  
  How to use: upload it, connect from a BLE UART-style app, exchange text with the board, and watch the LCD update.

- `Arduino/examples/10_BLE_UART`  
  BLE UART bridge between the board and a serial terminal.  
  How to use: upload it, connect with a BLE UART app, and pass lines of text between the BLE client and Serial Monitor.

- `Arduino/examples/11_BLE_Keyboard`  
  Emulates a BLE keyboard and sends demo keystrokes once paired.  
  How to use: upload it, pair the board with a host that accepts BLE keyboards, and be ready for automatic typing every few seconds.

### Wi-Fi Demos

- `Arduino/examples/12_WIFI_AP_LCD`  
  Starts a Wi-Fi access point and serves a simple web page that changes LCD colors or shows a picture.  
  How to use: upload it, join the board-hosted access point, open the IP address shown by the sketch, and use the page controls to change the LCD.

- `Arduino/examples/13_WIFI_TCP_Client`  
  Connects to Wi-Fi and then to a TCP server, sending a demo string and displaying the response on the LCD.  
  How to use: edit the Wi-Fi credentials plus server IP and port, start your TCP server, upload the sketch, and send back a short line for the LCD to display.

- `Arduino/examples/14_WIFI_TCP_Server`  
  Joins Wi-Fi and listens for TCP clients on port `8080`, then shows received text on the LCD.  
  How to use: edit the Wi-Fi credentials, upload the sketch, note the IP address, then connect from another device with a TCP client such as `nc` and send a line of text.

- `Arduino/examples/15_WIFI_Web_Server`  
  Starts an AP-hosted web page with a text box that sends text to the LCD.  
  How to use: upload it, join the board-hosted access point, browse to the served page, enter a short message, and press Send to display it on the screen.

### MQTT Demos

- `Arduino/examples/16_MQTT_sub_pub`  
  Connects to Wi-Fi and MQTT, publishes a device identifier, and updates the LCD in response to subscribed control messages.  
  How to use: edit the Wi-Fi and MQTT settings in the sketch, upload it, then publish the expected JSON control payload to the configured topic.

- `Arduino/examples/17_MQTT_BLE_Keyboard`  
  Bridges MQTT control messages into BLE keyboard actions and LCD status updates.  
  How to use: edit the Wi-Fi, MQTT, and any sensitive demo strings before uploading, pair the board as a BLE keyboard, then publish the expected payloads to trigger the configured key sequences.

## ESP-IDF Quick Start

Use this workflow for the projects under `ESP-IDF/`:

1. Install the ESP-IDF toolchain and IDE integration you prefer.
2. Open one project directory at a time, such as `ESP-IDF/04_button`.
3. Confirm that the target is set to `esp32c6`.
4. Review `sdkconfig` and any local source changes you need, especially for Wi-Fi credentials.
5. Build, flash, and open a serial monitor for the project.

Notes:

- The checked-in `sdkconfig` files are usually the best snapshot of how the examples were last built.
- Some `sdkconfig.defaults` files look older than the checked-in `sdkconfig` files, so review both if you run into target or flash-size confusion.
- The LVGL example READMEs are generic upstream text; the local source files are more specific about what these board demos actually do.

## ESP-IDF Examples

- `ESP-IDF/01_SD_Card`  
  SD card smoke test that mounts the card, writes a file, reads it back, and repeats.  
  How to use: insert a microSD card, build and flash the project, then watch the serial log for card info and file read/write output.

- `ESP-IDF/02_WIFI_AP`  
  Starts the board as a Wi-Fi access point and logs connected client information.  
  How to use: build and flash the project, join the configured access point from another device, and watch the serial log for connection events and assigned client IP data.

- `ESP-IDF/03_WIFI_STA`  
  Station-mode Wi-Fi connect test that joins an AP and logs the acquired IP address.  
  How to use: edit the hardcoded SSID and password first, then build, flash, and watch the monitor until the board reports a successful connection.

- `ESP-IDF/04_button`  
  LVGL + LCD + button demo that reacts to single, double, and long presses of the boot button.  
  How to use: build and flash the project, wait for the LCD to show the startup label, then interact with the button and watch both the screen and serial log.

- `ESP-IDF/05_lvgl_example_v8`  
  Minimal LVGL v8 LCD bring-up example that shows a centered version label.  
  How to use: build and flash the project, then confirm that the LCD lights up and prints the LVGL v8 version string.

- `ESP-IDF/06_lvgl_example_v9`  
  Minimal LVGL v9 LCD bring-up example that shows a centered version label.  
  How to use: build and flash the project, then confirm that the LCD lights up and prints the LVGL v9 version string.

## Prebuilt Firmware

- `Firmware/01_SD_LCD.bin`  
  Prebuilt firmware image included as-is.  
  How to use: flash it only if you specifically want to experiment with the vendor-provided binary image. The repo does not include a clear source-to-binary mapping for this artifact, so treat it as a convenience image rather than a documented primary workflow.

## Practical Tips

- Review any sketch or project before uploading because several examples contain hardcoded credentials, IP addresses, topics, or demo strings.
- Expect the LCD-oriented Arduino examples to share a lot of duplicated support code. They are demos first, not a unified application framework.
- If you want to turn one of these demos into a maintained project, choose the example closest to your goal and refactor it into a dedicated application directory rather than editing many example folders at once.
