# Lab 4: Liquid crystal display (LCD)

<!--
![LCD-keypad shield](images/arduino_uno_lcd-shield.jpg)
-->

### Learning objectives

After completing this lab you will be able to:

* Use alphanumeric LCD
* Understand the digital communication between MCU and HD44780
* Use library functions for LCD
* Generate custom characters on LCD

The purpose of the laboratory exercise is to understand the serial control of Hitachi HD44780-based LCD character display and how to define custom characters. Another goal is to learn how to read documentation for library functions and use them in your own project.

### Table of contents

* [Pre-Lab preparation](#preparation)
* [Part 1: Synchronize repositories and create a new project](#part1)
* [Part 2: LCD display module](#part2)
* [Part 3: Library for HD44780 based LCDs](#part3)
* [Part 4: Stopwatch](#part4)
* [Part 5: Defined and custom characters](#part5)
* [Experiments on your own](#experiments)
* [Post-Lab report](#report)
* [References](#references)

<a name="preparation"></a>

## Pre-Lab preparation

1. Use schematic of the [LCD keypad shield](https://oshwlab.com/tomas.fryza/arduino-shields) and find out the connection of LCD display. What data and control signals are used? What is the meaning of these signals?

   | **LCD signal(s)** | **AVR pin(s)** | **Description** |
   | :-: | :-: | :-- |
   | RS | PB0 | Register selection signal. Selection between Instruction register (RS=0) and Data register (RS=1) |
   | R/W | GND | 0=write, 1=read |
   | E | PB1 | enable signal (falling edge) |
   | D[3:0] | unconnected |  |
   | D[7:4] | PD[7:4] |  |
   | K | PB1 | backlight cathode |

2. What is the ASCII table? What are the codes/values for uppercase letters `A` to `Z`, lowercase letters `a` to `z`, and numbers `0` to `9` in this table?

   | **Char** | **Decimal** | **Hexadecimal** |
   | :-: | :-: | :-: |
   | `A` | 65 | 0x41 |
   | `B` | 66 | 0x42 |
   | `C` | 67 | 0x43 |
   | `D` | 68 | 0x44 |
   | `E` | 69 | 0x45 |
   | `F` | 70 | 0x46 |
   | `G` | 71 | 0x47 |
   | `H` | 72 | 0x48 |
   | `I` | 73 | 0x49 |
   | `J` | 74 | 0x4A |
   | `K` | 75 | 0x4B |
   | `L` | 76 | 0x4C |
   | `M` | 77 | 0x4D |
   | `N` | 78 | 0x4E |
   | `O` | 79 | 0x4F |
   | `P` | 80 | 0x50 |
   | `Q` | 81 | 0x51 |
   | `R` | 82 | 0x52 |
   | `S` | 83 | 0x53 |
   | `T` | 84 | 0x54 |
   | `U` | 85 | 0x55 |
   | `V` | 86 | 0x56 |
   | `W` | 87 | 0x57 |
   | `X` | 88 | 0x58 |
   | `Y` | 89 | 0x59 |
   | `Z` | 90 | 0x60 |
   | ... | ... | ... |
   | `a` | 97 | 0x61 |
   | `b` | 98 | 0x62 |
   | ... |  |  |
   | `0` | 48 | 0x30 |
   | `1` | 49 | 0x31 |
   | ... |  |  |

<a name="part1"></a>
