WiFi NTP Clock with TM1637 Display (WeMos D1)
A compact, internet-connected digital clock built using a WeMos D1 (ESP8266) microcontroller and a TM1637 4-digit 7-segment display. The clock automatically syncs the current time from an NTP (Network Time Protocol) server over WiFi and alternates between displaying the time (HH:MM) and the date (MM:DD) at a fixed interval.

Purpose
Traditional digital clocks require manual time-setting and drift over time. This project solves that by pulling accurate time from internet time servers, ensuring the clock is always correct — even after power outages. It demonstrates core IoT concepts: WiFi connectivity, NTP time synchronization, timezone handling, and embedded display control.

How It Works
On boot, the WeMos D1 connects to a local WiFi network using stored credentials.

Once connected, it queries an NTP server (pool.ntp.org) to fetch the current UTC time.

A timezone offset (e.g., UTC+2 for South Africa) is applied to convert UTC to local time.

The ESP8266 formats the time as HH:MM and the date as MM:DD.

A toggle timer switches the display between time and date every 5 seconds.

The colon separator on the display is ON in time mode and OFF in date mode, making the mode visually clear.

The NTP client resyncs every 60 seconds to prevent drift.

Hardware Requirements
Component	Quantity	Notes
WeMos D1 (ESP8266)	1	WiFi-enabled microcontroller
TM1637 4-digit display	1	7-segment LED display module
Jumper wires	4	For CLK, DIO, VCC, GND
USB power supply	1	5V, stable current
(Optional) 100µF capacitor	1	Across VCC/GND for stability
(Optional) 4.7kΩ resistors	2	Pull-ups on CLK/DIO if signal is unstable
🔌 Pin Connections
TM1637 Pin	WeMos D1 Pin	GPIO
CLK	D6	GPIO12
DIO	D7	GPIO13
VCC	5V	—
GND	GND	—
Software & Libraries
Arduino IDE with ESP8266 board support

ESP8266WiFi.h — WiFi connectivity

WiFiUdp.h — UDP for NTP

NTPClient.h — NTP time fetching

TM1637Display.h — Display driver

Features
Automatic time sync via internet (NTP)

No manual time setting required

Timezone-aware (configurable offset)

Auto-toggles between time and date

Visual mode indicator (colon on/off)

Auto-resync every 60 seconds

Compact, low-cost build (~R100 in parts)

Expandable (buttons, sensors, alarms, OTA)

Challenges & Solutions
Challenge	Solution
Display flickering	Removed/replaced faulty capacitors on TM1637 module; ensured stable 5V supply
Display toggling too fast	Made previousMillis a global variable (not reset each loop)
Timezone mismatch	Applied correct UTC offset (7200s for SAST)
WiFi disconnection	Added reconnection logic and periodic NTP updates
Possible Extensions
Push button to manually switch modes

DHT11/DHT22 for temperature & humidity display

Auto-dimming at night

Alarm with buzzer

OTA (Over-The-Air) firmware updates

Blynk/Web dashboard for remote control

Concepts Demonstrated
IoT device connectivity (WiFi)

Network Time Protocol (NTP) usage

Timezone and epoch time handling

Embedded C++ programming

I2C-like serial display protocol (TM1637)

Non-blocking timing with millis()

Hardware debugging (signal integrity, power)

