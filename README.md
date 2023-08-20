# Esp32-Smartwatch

![Screenshot (1731)](https://github.com/No-Need-Loi/Esp32-Smartwatch/assets/142481076/f8dbc46e-ba95-4d0b-a72a-078f2cfa9765)

This is a simple esp32 smart watch made with esp32 chip and some complementary components for its working such as the capacitors resistor and other components for their operational feature smartwatch that is easy to reprogram and use as an IOT controller or just as a DIY fashion statement.

Serial communication and charging are handled on-board through a single micro-usb connector without any external dock. The watch is built around the ESP32 WROOM module and is programable using the espressif or Arduino IDE. Using the ESP32 allows for the user to develop their software while leveraging the open-source libraries and examples that are available online for quick development.

Specifications
ESP32-pico-D4: 2x240MHz, 320KB RAM
Bluetooth 4.2 BR/EDR BLE
WiFi 2.4GHz 802.11 b/g/n
GC9A01 240x240 16bit TFT display (round)
BMA400 Accelerometer + Pedometer
MCP73831 LiPo Charger
CH340E USB Serial
Quectel L96 GPS module
4MB RAM
microSD

Low-cost: you can get an ESP32 starting at $6, which makes it easily accessible to the general public;

Low-power: the ESP32 consumes very little power compared with other microcontrollers, and it supports low-power mode states like deep sleep to save power;

![Screenshot (1730)](https://github.com/No-Need-Loi/Esp32-Smartwatch/assets/142481076/aa4f7e54-2c3a-459d-8175-2bb35188dbd4)

Wi-Fi capabilities: the ESP32 can easily connect to a Wi-Fi network to connect to the internet (station mode), or create its own Wi-Fi wireless network (access point mode) so other devices can connect to it—this is essential for IoT and Home Automation projects—you can have multiple devices communicating with each other using their Wi-Fi capabilities

In many electronic projects, working with accurate time is essential, whether it’s displaying it to the user or performing specific operations at specific times. However, the generic Real-time clock (RTC) chips may not always provide the precision required. The internal clocks of devices like ESP32 may not be highly accurate, and they can drift over time due to various factors like temperature changes or component aging. By querying an NTP server, which typically uses highly accurate time sources like atomic clocks or GPS, the ESP32 can synchronize its internal clock and maintain a more accurate time reference.

![Screenshot (1732)](https://github.com/No-Need-Loi/Esp32-Smartwatch/assets/142481076/4dd880f6-e121-439b-ad77-074b2b418b96)


A more precise solution involves accessing the central NTP server via the Internet to obtain accurate date and time information. The NTP server is widely used worldwide and offers timestamps with a precision of a few milliseconds of the Coordinated Universal Time (UTC) without the need for additional hardware setup and costs. By utilizing the Network Time Protocol (NTP) server, we can easily request the current date and time through our local WIFI network. This ensures that our electronic projects have reliable and synchronized time information.

![Screenshot (1742)](https://github.com/No-Need-Loi/Esp32-Smartwatch/assets/142481076/67cea719-4849-4d33-a64e-ba959180a6ff)

This project contains PCB and which was made with the help of JLCPCB

JLCPCB has upgraded the via-in-pad process of all 6-20 layer PCBs for free and provides free ENIG to make PCB products more stable and reliable. It is worth mentioning that due to large-scale production capabilities, JLCPCB is able to reduce the cost, allowing everyone to truly enjoy the benefits of the JLCPCB advanced fabrication. Here at JLCPCB, you can also get 1-8 layer PCBs at only $2


Go to JLCPCB website and create a free account.  

![Screenshot (1743)](https://github.com/No-Need-Loi/Esp32-Smartwatch/assets/142481076/b4e05aec-1b71-4484-bdcf-e14b19701c4a)


Register and Login using Google Account is also possible.

Step 2 – Upload Gerber File
Once you have successfully created an account, Click on “Quote Now” and upload your Gerber File.

Gerber File contains information about your PCB such as PCB layout information, Layer information, spacing information, tracks to name a few.

Step 3 – Preview the File
Once the Gerber file is uploaded, it will show you a preview of your circuit board.

Make sure this is the PCB Layout of the board you want.

Step 4 – Choose Necessary PCB Options

![FEP2OKBLL9GI263](https://github.com/No-Need-Loi/Make-Your-Own-ESP32-Simple/assets/142481076/ee79a6b2-8171-4edc-8f75-58105317fb0d)

Below the PCB preview, you will see so many options such as PCB Quantity, Texture, Thickness, Color etc. Choose all that are necessary for you. 

Network Time Protocol (NTP)
NTP is a standard internet protocol that is widely used to synchronize computer clocks to a reference network. With a precision of approximately 50ms over the wide-area network (WAN) and less than 5ms over the local area network (LAN), it synchronizes epoch time of all networked devices to the UTC.

NTP Server Architecture
The NTP Server is based on a hierarchical structure consisting of three levels where each level is known as the stratum. In the first level (Stratum 0) there are highly precise atomic/radio clocks that provide the exact time. The second level (Stratum 1) is directly connected with the first level and thus contains the most precise time available which it receives from the first level. The third and last level (Stratum 2) is the device that makes the request to the NTP server for the date/time from the second level. In the hierarchy, each level synchronizes with the level above it.

![Screenshot (1728)](https://github.com/No-Need-Loi/Esp32-Smartwatch/assets/142481076/3dc0d2bb-b0b2-491b-9b7b-f4da43c76a33)

NTP (Network Time Protocol)
NTP stands for Network Time Protocol and it is a networking protocol for clock synchronization between computer systems. In other words, it is used to synchronize computer clock times in a network.

There are NTP servers like pool.ntp.org that anyone can use to request time as a client. In this case, the ESP32 is an NTP Client that requests time from an NTP Server (pool.ntp.org).

Getting Date and Time from NTP Server
To get date and time with the ESP32, you don’t need to install any libraries. You simply need to include the time.h library in your code.

The following code gets date and time from the NTP Server and prints the results on the Serial Monitor. It was based on the example provided by the time.h library.

![Screenshot (1738)](https://github.com/No-Need-Loi/Esp32-Smartwatch/assets/142481076/c2d1cac6-e5b9-4062-812b-b782680799ea)

How the Code Works
Let’s take a quick look at the code to see how it works. First, include the libraries to connect to Wi-Fi and get time.

#include <WiFi.h>
#include "time.h"
Setting SSID and Password
Type your network credentials in the following variables, so that the ESP32 is able to establish an Internet connection and get date and time from the NTP server.

// Replace with your network credentials
const char* ssid = "REPLACE_WITH_YOUR_SSID";
const char* password = "REPLACE_WITH_YOUR_PASSWORD";
NTP Server and Time Settings
Then, you need to define the following variables to configure and get time from an NTP server: ntpServer, gmtOffset_sec and daylightOffset_sec.

NTP Server

We’ll request the time from pool.ntp.org, which is a cluster of timeservers that anyone can use to request the time.

const char* ntpServer = "pool.ntp.org";
GMT Offset

The gmtOffset_sec variable defines the offset in seconds between your time zone and GMT. We live in Portugal, so the time offset is 0. Change the time gmtOffset_sec variable to match your time zone.

![Screenshot (1726)](https://github.com/No-Need-Loi/Esp32-Smartwatch/assets/142481076/b60061a6-741a-458c-8bae-7fea91178169)

const long gmtOffset_sec = 0;
Daylight Offset

The daylightOffset_sec variable defines the offset in seconds for daylight saving time. It is generally one hour, that corresponds to 3600 seconds

const int daylightOffset_sec = 3600;
setup()
In the setup() you initialize the Serial communication at baud rate 115200 to print the results:

Serial.begin(115200);
These next lines connect the ESP32 to your router.

// Connect to Wi-Fi
Serial.print("Connecting to ");
Serial.println(ssid);
WiFi.begin(ssid, password);
while (WiFi.status() != WL_CONNECTED) {
  delay(500);
  Serial.print(".");
}
Serial.println("");
Serial.println("WiFi connected.");
Configure the time with the settings you’ve defined earlier:

configTime(gmtOffset_sec, daylightOffset_sec, ntpServer);
printLocalTime()
After configuring the time, call the printLocalTime() function to print the time in the Serial Monitor.

In that function, create a time structure (struct tm) called timeinfo that contains all the details about the time (min, sec, hour, etc…).

struct tm timeinfo;
The tm structure contains a calendar date and time broken down into its components:

tm_sec: seconds after the minute;
tm_min: minutes after the hour;
tm_hour: hours since midnight;
tm_mday: day of the month;
tm_year: years since 1900;
tm_wday: days since Sunday;
tm_yday: days since January 1;
tm_isdst: Daylight Saving Time flag;
Code started by including the WiFi and time library. WiFi library will help to connect ESP32 with a network while time library will handle the NTP server synchronization.

![Screenshot (1737)](https://github.com/No-Need-Loi/Esp32-Smartwatch/assets/142481076/f8024b5d-4fd6-4145-b606-19bd5e747d23)

After that SSID and password of the network to which ESP32 will connect is defined. Replace your network credential here. After that we have defined GMT offset as 18000 sec which is (UTC+5 hour). You can replace your own timezone UTC

The micro-USB port is used for both charging as well as programming purposes. The power and data connections from the micro-USB port is connected to TVS ESD protection diodes. These diodes will protect the entire circuit from any ESD spikes on the USB input. The 5V from the USB port is then connected the input of MCP7383 1S Li ion battery charger. The out put from the charging IC is then fed to the protection circuit built around the DW01 IC and the FS8205 MOSFET. This protection circuit combination will protect the battery from over current discharges and deep discharge.

The power then passes through two LDOs. The main voltage regulator used in the circuit is the NCP167AMX330TBG from ON Semi. It can provide a maximum current of 700ma. The main advantage of using this chip is the size. The NCP167AMX comes in a 1mmx1mm 4-XDFN package. Which saves a lot of space. The second Low voltage regulator in the circuit is a XC620P182MR-G 1.8V LDO. This LDO is used for the MAX30102 Heart Rate sensor chip.

The power then passes through two LDOs. The main voltage regulator used in the circuit is the NCP167AMX330TBG from ON Semi. It can provide a maximum current of 700ma. The main advantage of using this chip is the size. The NCP167AMX comes in a 1mmx1mm 4-XDFN package. Which saves a lot of space. The second Low voltage regulator in the circuit is a XC620P182MR-G 1.8V LDO. This LDO is used for the MAX30102 Heart Rate sensor chip.

![Screenshot (1739)](https://github.com/No-Need-Loi/Esp32-Smartwatch/assets/142481076/98e2a859-dc3a-4daf-b8ac-2ef0e9da4331)


There are other specifiers you can use to get information in other format, for example: abbreviated month name (%b), abbreviated weekday name (%a), week number with the first Sunday as the first day of week one (%U)

We also show you an example, if you want to save information about time in variables. For example, if you want to save the hour into a variable called timeHour, create a char variable with a length of 3 characters (it must save the hour characters plus the terminating character). Then, copy the information about the hour that is on the timeinfo structure into the timeHour variable using the strftime() function.
