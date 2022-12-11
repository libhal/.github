<div align="center">
<img height="250" src="profile/logo.png">
<br />
<br />

```
🚚 portable 🦾 flexible 📦 accessible 🍰 easy to use
```
<br />
</div>

<div align="center">

[![GitHub stars](https://img.shields.io/github/stars/libhal/libhal.svg)](https://github.com/libhal/libhal/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/libhal/libhal.svg)](https://github.com/libhal/libhal/network)
[![GitHub issues](https://img.shields.io/github/issues/libhal/libhal.svg)](https://github.com/libhal/libhal/issues)
[![Discord](https://img.shields.io/discord/800515757871726622?color=7389D8&logo=discord&logoColor=ffffff&labelColor=6A7EC2)](https://discord.gg/p5A6vzv8tm)

[Install](#-install)
| [Overview](#ℹ%EF%B8%8F-overview)
| [Glossary](#-glossary)
| [Usage](#%EF%B8%8F-usage)
| [Badges](#-library-badges)
| [Standards](#-library-standards)
| [Libraries](#-libraries)
| [Motivation](#-motivation)
| [Contributing](#-contributing)

🚧 **_This document is still in construction and is subject to change at any time_** 🚧

</div>

# [📚 libhal APIs](https://libhal.github.io/libhal/api)

# 📥 Install

Libhal is simply a set of interfaces for hardware drivers. It can be adopted in
many ways, one of which is simply downloading the header only library and using
the interfaces directly, but this will not give as much of a benefit without a
package manager to make managing, upgrading, and changing dependencies easier.

## Using Conan (RECOMMENDED)

Link to the [Install Conan Prerequisites](conan-prerequisites.md) page.

### Install from `libhal-trunk`

`libhal-trunk` is a remote conan server with the latest version of the code.

Run the following to add `libhal-trunk` to your list of conan remote servers.

NOTE: that the `--insert` argument places this server at the highest priority
for conan, meaning updates will be checked at this server first before
attempting to check out servers like the CCI.

```bash
conan remote add libhal-trunk https://libhal.jfrog.io/artifactory/api/conan/trunk-conan --insert
conan config set general.revisions_enabled=True
```

### Create conan package locally

```bash
git clone https://github.com/libhal/libhal.git
cd libhal
conan create .
```

# ℹ️ Overview

libhal exists to make hardware drivers:

- **🚚 portable**
- **🦾 flexible**
- **📦 accessible**
- **🍰 easy to use**

## Project Attributes

- Header only
- Available on Conan (coming soon to vcpkg)
- Does not throw exceptions
- Does not dynamically allocate
- Uses tweak header files for customization
- Designed to be modular, dynamic, composable, and lightweight
- System agnostic
- Follows C++ Core Guidelines
- Dependencies:
  - C++20
  - [Boost.LEAF](https://boostorg.github.io/leaf/) for error handling

# 🚀 Getting Started (INCOMPLETE)

Check out the [libhal-starter](https://github.com/libhal/libhal-starter) project
to get started with libhal.

## Finding Utilities

libhal is just a set of interfaces without any helper methods. This was done
intentionally to keep the API clear and concise, keep compile times short,
and to keep dependencies as small as possible. But this has also means that
using the APIs directly may not make for a nice experience. Some APIs also need
additional software support to manage hardware resources.

To help with this, the [libhal-util](https:://github.com/libhal/libhal-util)
package exists to improve quality of life and to provide minimal software layers
to manage hardware resources such as thread-safe wrappers for APIs and helper
functions for generating timeout objects, writing strings to ports without the
boiler plate and much more.

## Using Soft Drivers

TBD

# 🪪 Library Badges

![supported](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Flibhal%2Flibhal%2Fmain%2Fbadges%2Fsupported.json)
![safety critical](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Flibhal%2Flibhal%2Fmain%2Fbadges%2Fsafety_critical.json)
![allocates](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Flibhal%2Flibhal%2Fmain%2Fbadges%2Fallocates.json)
![double](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Flibhal%2Flibhal%2Fmain%2Fbadges%2Fdouble.json)
![throws](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Flibhal%2Flibhal%2Fmain%2Fbadges%2Fthrows.json)

The badges above are displayed in a library's README.md right below the title to
indicate attributes of the library. When searching for a library to use for your
project, these badges can help you decide if the project meets your
requirements.

## Supported

All libraries that implement libhal interfaces should have this badge to
indicate library users/consumers.

## 🦺 SAFETY CRITICAL

If a library follows completely the AUTOSAR C++20 guidelines.

## ⚠️ ALLOCATES

This badge is placed for a libraries that have the possibility to dynamically
allocate memory via `new`, `malloc`, `std::allocator` or a standard library
that uses any of the allocating functions.

## ⚠️ DOUBLES

If a library uses double floating point arithmetic anywhere in its
implementation. Some points to consider when seeing a library that uses doubles:

- Double floating point operations take up flash space for devices without a
  hardware FPU (floating point unit).
- The cost is only paid once because the software implementation of floating
  point support code can be called each time for each operation. So if you are
  already using doubles in your code then it is likely that using this library
  will not add more space to a project.
- Software driven double floating point arithmetic is slow compared to integer
  or single floating point arithmetic.

## ⚠️ THROWS

If a library ever throws an exception anywhere in its code base.
Some points to consider when seeing a library that uses floats:

- Exceptions can be quite slow to propagate when they occur, although this is
  not always the case.
- If a project has exceptions turned off, this library will not compile, and thus
  cannot be used.
- Using exceptions generally incurs an increase in size for your binary (around
  8kB for the exception runtime environment for arm cortex-m).
- The infrastructure for error handling is already handled by Boost.LEAF so
  exceptions are redundant.
- Exceptions require dynamic memory allocate.

# Making your own libhal Interfaces and Drivers

In order to demonstrate how to create an interface a thoroughly
documented/commented set of example code has been written. The comments in these
files acts as guides to help new developers learn how to create their own
libhal interfaces, peripheral drivers, device drivers and soft drivers.

The following files are a guide to how to write their respective driver:

- Peripheral Drivers:
  - [`lpc40xx::adc.hpp`](https://github.com/libhal/liblpc40xx/blob/main/include/liblpc40xx/adc.hpp)
- Device Drivers:
  - [`mma8452q::accelerometer.hpp`]() TBD
- Soft Drivers;
  - [`hal::rc_servo.hpp`]() TBD
  - [`hal::bit_bang_spi.hpp`]() TBD

# 📚 Libraries

## Processors

- [libarmcortex](https://github.com/libhal/libarmcortex): Drivers for the ARM
  Cortex M series of processors.
- [libriscvi32](https://github.com/libhal/libriscvi32): Coming soon. Drivers for
  32-bit RISC-V processors.

## Targets

- [liblpc40xx](https://github.com/libhal/liblpc40xx): Drivers the lpc40xx
  series of microcontrollers. This includes startup code, linker scripts, and
  peripheral drivers.
- [libstm32f1xx](https://github.com/libhal/libstm32f1xx): Coming soon.
  Drivers the stm32f1xx series of microcontrollers.

### Drivers

- [libesp8266](https://github.com/libhal/libesp8266): Drivers for the
  esp8266 micro-controller as well as drivers for the WiFi/Internet firmware AT
  client.
- [libmpu6050](https://github.com/libhal/libmpu6050): Coming soon.
  Accelerometer and gyroscope device. Requires an i2c driver.

# 💡 Motivation

The world of embedded systems is written almost entirely in C and C++. More and
more of the embedded world move away from C and towards C++. This has to do with
the many benefits of C++ such as type safety, compile time features,
meta-programming, multiple programming paradigms which, if use correctly can
result in smaller and higher performance code than in C.

But a problem for embedded software in C++, as well as in C, is that there isn't
a consistent and common API for embedded libraries. Looking around, you will
find that each hardware vendor has their own set of libraries and tools for
their specific products. If you write a driver on top of their libraries, you
will find that your code will only work for that specific platform/product. In
some cases you may also be limited to just their toolchain. You as the developer
are locked in to this one specific setup. And if you move to another platform,
you must do the work of rewriting all of your code again.

libhal seeks to solve this issue by creating a set of generic interfaces
for embedded system concepts such as serial communication (UART), analog to
digital conversion (ADC), inertial measurement units (IMU), pulse width
modulation (PWM) and much more. The advantage of building a system on top of
libhal is that higher level drivers can be used with any target platform
whether it is a stm32, a nxp micro controller, a RISC-V, or is on an
embedded linux.

This project is inspired by the work of Rust's embedded_hal and follows many of
the same design goals.

libhal's design goals:

1. Serve as a foundation for building an ecosystem of platform agnostic drivers.
2. Must abstract away device specific details like registers and bitmaps.
3. Must be generic across devices such that any platform can be supported.
4. Must be minimal for boosting performance and reducing size costs.
5. Must be composable such that higher level drivers can build on top of these.
6. Be accessible through package mangers so that developers can easily pick and
   choose which drivers they want to use.

# 📃 Glossary

Here is a list of terms used in libhal. It is HIGHLY RECOMMENDED that
new users of libhal read this section.

## Target

Targets are defined as MCUs (micro-controllers), SOCs (system-on-chip),
operating systems, or operating systems running on a particular SBC
(single-board-computer).

### MCU target examples

- LPC40xx series family of MCUs
- STM32F10x series family of MCUs
- RP2040

### SOCs target examples

- AM335x
- Samsung Exynos5422

### Operating Systems target examples

- Linux
- Windows CE

### SBC examples

- Raspberry Pi
- ODROID UX
- BeagleBone Black

## Interface

Interfaces are the basic building blocks of libhal and enable the
flexibility needed to be portable and flexible.

An interface is a contract of functions that an implementing class must adhere
to. Interface documentation explains in detail the expected behavior that each
function should have on hardware regardless of the implementation. When a
program is compiled and a driver implements an interface, the compiler detects
if any of the functions have not been provided and if so, will report an error.

In libhal each interface corresponds to a type of embedded system
primitive such as:

- Digital I/O (input/output pins)
- Analog to digital converter (adc)
- Pulse width modulation (pwm)
- Serial peripheral interface (spi)
- Universal asynchronous receiver transmitter (serial/uart)
- Accelerometer

## Peripheral drivers

Peripheral drivers are drivers for a target that is embedded within the device
and therefore cannot be removed from the chip and is fixed in number.

- Example: A digital output and input pin
- Example: 1 of 5 hardware timers within a micro-controller
- Example: Integrated analog-to-digital converter

## Device drivers

Device drivers are drivers for devices external to a target. In order to
communicate with such a device the target must have the necessary peripherals
and peripheral drivers to operate correctly.

- Example: an accelerometer driver for the mpu6050
- Example: a memory storage driver for a at581 flash memory
- Example: a black and white pixel display

## Soft drivers

Soft drivers are drivers that do not have any specific underlying hardware
associated with them. They are used to emulate, give context to, or alter the
behavior of interfaces. For a driver to be a soft driver it must implement or
have a way to generate, construct or create implementations of hardware
interfaces.

### Emulation Example

- Emulate spi by using 2 output pins and 1 input pin.
- Emulate uart transmission with a 16-bit spi driver and some clever bit
  positioning.

### Context Example

- Implement a rotary encoder by using an adc, a potentiometer and some
  specification of the potentiometer like min and max angle, along with min and
  max voltage.
- Implement a dac using multiple output pins and a set of resistors and an op
  amp.

### Alteration example

- Implement an input pin that inverts the readings of an actual input pin
- Implement an i2c driver that is thread safe by taking an i2c and locking
  mechanism provided by the user.

In general, software drivers tend to incur some overhead so nesting them
deeply will effect performance.

## Hard drivers

Hard drivers are peripheral drivers and device drivers.

## Off Interface Function

Off interface functions are public class functions that a driver can have that
is beyond what is available for the interface it is implementing. These
functions usually configure a peripheral or device in a way that is outside
the scope of the implementing interface. For peripherals these are platform
specific. For drivers these are device specific features. Examples of such
specific functions are as follows:

- An output pin driver with a high drain current mode
- An input pin driver with support for inverting the voltage level of what it
  reads in hardware.
- Enabling/disabling continuous sampling from an accelerometer where sampling
  continuously would make reading samples faster but would consume more power
  and disabling continuous sampling would do the opposite.
