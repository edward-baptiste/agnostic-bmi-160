# BMI160 Platform-Agnostic Embedded Driver

The goal of this project was to create a lightweight, reusable C driver for the [Bosch BMI160](https://www.bosch-sensortec.com/products/motion-sensors/imus/bmi160/) inertial measurement unit (IMU), designed to be **hardware abstraction layer (HAL)-independent** and portable across microcontroller platforms. 


## Features

- Written in C
- Platform-agnostic design
- HAL interface using function pointers (`read`, `write`, `delay`)
- I²C compatible
- Implements BMI160 initialization, configuration, self tests, and basic sensor reads
- Follows UNIX-style API (open, ioctl, read, etc.)
- Can be integrated into RTOS, bare-metal, or test environments
- Includes self-test routines and register access helpers


## How to Use

1. **Include the driver in your project**


2. **Connect your platform's I²C API**

Implement the HAL functions and pass them to the driver:


```c
uint8_t my_i2c_read(uint8_t reg, uint8_t *data, uint16_t len, struct bmi160_dev_t *dev);
uint8_t my_i2c_write(uint8_t reg, uint8_t *data, uint16_t len, struct bmi160_dev_t *dev);
void my_delay_ms(uint8_t ms);
```

3. **Initialize the device**

```c
struct bmi160_dev_t dev = {
    .read = my_i2c_read,
    .write = my_i2c_write,
    .delay_ms = my_delay_ms
};

bmi160_open(&dev);
```
