# ATmega328 Stopwatch with Dual 7-Segment Display

This project implements a simple digital stopwatch using an **ATmega328**, a **74HC595 shift register**, and **two common-anode 7-segment displays**. The stopwatch counts from 00 to 99 seconds using precise hardware timing, external interrupts for button control, and fast direct-port manipulation for display updates.

---

## Features

* **Accurate 1 Hz timing** using Timer1 in CTC mode
* **Start/Stop button** on INT1 (PD3)
* **Reset button** on INT0 (PD2)
* **Dual 7-segment common-anode display** driven by a 74HC595
* **Direct port toggling** for fast, clean clock pulses
* **Lookup table** for segment patterns stored in Flash (`const`)
* **Non-blocking operation** using flags set inside ISRs

---

## Hardware Overview

### Microcontroller

* ATmega328 running at **16 MHz**

### Display

* Two **common-anode** 7-segment displays
* Patterns shifted via **74HC595** using:

  * SER → PD6
  * SRCLK → PD7
  * LATCH → PB0
  * RESET → PB1

### Buttons

* **Start/Stop** → PD3 (INT1)
* **Reset** → PD2 (INT0)
* Both use internal pull-ups and active‑low triggers

---

## How It Works

* Timer1 generates a **1-second interrupt**.
* When running, the ISR increments a counter (00–99).
* A lookup table converts digits into 7-segment bit patterns.
* These bytes are clocked into the 74HC595 using direct port writes for maximum speed.
* External interrupts toggle the running state or reset the timer.

---
Feedback and suggestions are welcome!
