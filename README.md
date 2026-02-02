# STM32F767 – DHT22 Temperature & Humidity Display (I²C LCD)

![STM32](https://img.shields.io/badge/STM32-F7-blue)
![Language](https://img.shields.io/badge/Language-C-green)
![HAL](https://img.shields.io/badge/Framework-STM32%20HAL-orange)
![Status](https://img.shields.io/badge/Status-Working-success)

---

##  Project Description

This project demonstrates how to interface a **DHT22 temperature and humidity sensor** with an **STM32F767ZI (Nucleo)** board and display real-time sensor readings on a **16×2 I²C LCD**.

The DHT22 protocol is timing-critical, so this implementation uses **TIM6** to generate **microsecond-accurate delays**, ensuring reliable communication without blocking the system using `HAL_Delay()`.

---

##  Features

- Accurate DHT22 temperature & humidity readings
- Microsecond timing using **TIM6**
- Dynamic GPIO mode switching (Output ↔ Input)
- Real-time display on **I²C 16×2 LCD**
- Checksum validation and error handling
- Fully HAL-based (easy to extend or refactor)

---

##  Hardware Requirements

- STM32F767ZI Nucleo Board  
- DHT22 (AM2302) Sensor  
- 16×2 I²C LCD (PCF8574)  
- 10kΩ pull-up resistor (DHT22 DATA line)  
- Jumper wires  

---

## 🔌 Pin Connections

### DHT22 Sensor

| DHT22 Pin | STM32 Pin | Description |
|---------|----------|------------|
| VCC | 3.3V | Power |
| DATA | **PB1** | One-wire data |
| GND | GND | Ground |

>  **Important:** The DATA line requires a pull-up resistor (≈10kΩ) to 3.3V.

---

### I²C LCD

| LCD Pin | STM32 Pin |
|-------|----------|
| SDA | PB9 |
| SCL | PB8 |
| VCC | 5V / 3.3V |
| GND | GND |

---

##  Software Configuration

- **IDE:** STM32CubeIDE  
- **Framework:** STM32 HAL  
- **Timer:** TIM6 (used for µs delays)  
- **I²C Peripheral:** I²C1  

---

##  Timing Strategy (Why TIM6?)

The DHT22 communication protocol depends on pulse widths measured in **microseconds**.

This project:
- Uses TIM6 as a free-running counter
- Implements a custom `delay(us)` function
- Samples DHT22 bits based on pulse duration
- Avoids unreliable software delays

This ensures **stable and repeatable sensor readings**.

---

## 📟 LCD Output Format

```c
TEMP: 24.60 C
RH: 55.30 %
```

If communication fails, the LCD displays:
```c
Checksum/Error
```

---

## 📚 Learning Reference

This project was inspired by concepts from the  
**ControllersTech YouTube channel**, adapted and extended for STM32F7 timing, HAL usage, and I²C LCD integration.

---

##  Possible Improvements

- Separate DHT22 driver (`dht22.c / dht22.h`)
- GPIO interrupt-based timing
- UART debugging output
- RTC timestamped logging
- CMSIS / bare-metal GPIO rewrite

---

##  What This Project Teaches

- Timing-critical sensor protocols
- Hardware timer usage for precision delays
- Runtime GPIO reconfiguration
- Multi-peripheral coordination (GPIO + TIM + I²C)
- Embedded debugging and validation

---

##  Author

Developed as part of hands-on learning in  
**Embedded Systems & Microcontroller Programming**.
