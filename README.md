# LVGL 9.x on Waveshare ESP32-S3-Touch-AMOLED-1.64

This project demonstrates how to run **LVGL 9.x** with touch support on the **Waveshare ESP32-S3-Touch-AMOLED-1.64** board. It includes a minimal FT3168 touch driver (via I²C) and a simple visualization (circle + crosshair lines) to show touch points clearly.

-----

## Features

  - Display: **1.64" AMOLED (280×456), CO5300 driver IC**
  - Touch: **FT3168 capacitive touch controller (I²C)**
  - IMU: **QMI8658C 6-axis sensor**
  - Flash: **W25Q128JVSI 128Mbit**
  - Power: **MP1605GTF-Z buck converter + ETA6098 battery charger**
  - GUI: **LVGL 9.x** with Arduino
  - Example UI:
      - “Hello World” label
      - Circle + crosshair following finger touches

-----

## Arduino Build Settings

| Setting | Value |
| :--- | :--- |
| **Board** | Waveshare ESP32-S3-Touch-AMOLED-1.64" |
| **CPU Frequency** | 240MHz (WiFi) |
| **Partition Scheme** | 16M Flash (3MB App/9.9MB FATFS) |
| **PSRAM** | Enabled |
| **USB CDC On Boot** | Enabled |
| **Upload Speed** | 921600 |

-----

## Board Pin Usage

### Display (AMOLED, CO5300 driver)

  - **GPIO9–14**: QSPI interface
      - GPIO9: OLED\_CS
      - GPIO10: OLED\_CLK
      - GPIO11: OLED\_SIO0
      - GPIO12: OLED\_SIO1
      - GPIO13: OLED\_SIO2
      - GPIO14: OLED\_SIO3
  - **GPIO21**: OLED\_RESET

### Touch Panel (FT3168, I²C)

  - **GPIO47**: SDA
  - **GPIO48**: SCL
  - I²C Address: **0x38**

### Other Onboard Peripherals

  - **USB**: GPIO19 (D-), GPIO20 (D+)
  - **UART0**: GPIO43 (TX), GPIO44 (RX)
  - **SD Card**: GPIO38–41 (CS, MOSI, MISO, CLK)
  - **IMU (QMI8658C)**: GPIO47 (SDA), GPIO48 (SCL), GPIO46 (INT)
  - **BOOT Button**: GPIO0
  - **Power**:
      - 3V3 (regulated output)
      - 5V (USB/external)
      - BAT (battery input, charging supported)

-----

## Project Structure

```
.
├── waveshare-amoled164-lvgl9/
│   └── waveshare-amoled164-lvgl9.ino # Arduino sketch with LVGL + touch
├── lv_conf.h                         # LVGL configuration
└── README.md
```

-----

## `lv_conf.h` Placement

LVGL requires a **project-local `lv_conf.h`** to configure build options.

  - Copy the provided `lv_conf.h` file into the **project root** (same level as `src/`)
  - Alternatively, place it inside `src/`
  - Ensure the following line is **enabled in `lv_conf.h`**:
    ```c
    #define LV_CONF_INCLUDE_SIMPLE 1
    ```
    Arduino/LVGL will automatically detect and use this file.

Not much was changes in the lv_conf.h except for enabling it and enabling `#define LV_USE_DEMO_WIDGETS 1`

-----

## How to Build & Run

1.  Clone this repository.
2.  Open the folder in Arduino IDE or PlatformIO.
3.  **Install required libraries:**
      - **LVGL (v9.x)**: Install via the Arduino Library Manager.
      - **Arduino\_GFX**: This library is a **mandatory dependency** for this project. It must be installed manually. You can get it from the [Arduino\_GFX GitHub repository](https://github.com/moononournation/Arduino_GFX/).
        To install it manually in the Arduino IDE, download the repository as a `.zip` file and use the `Sketch > Include Library > Add .ZIP Library...` option.
4.  Apply the build settings listed above.
5.  Flash to the ESP32-S3 board.
6.  After boot:
      - You will see “Hello World” text in the center.
      - Touch the screen → A red circle and green crosshair will follow your finger.

-----

## Touch Visualization

  - **Circle**: shows precise touch coordinate.
  - **Crosshair lines**: span the entire width and height, intersecting at the touch point → useful if your finger blocks the view.

-----

### Board Documentation

  - **Product Page**: [https://www.waveshare.com/esp32-s3-touch-amoled-1.64.htm](https://www.waveshare.com/esp32-s3-touch-amoled-1.64.htm)
  - **Wiki/Documentation**: [https://www.waveshare.com/wiki/ESP32-S3-Touch-AMOLED-1.64](https://www.waveshare.com/wiki/ESP32-S3-Touch-AMOLED-1.64)