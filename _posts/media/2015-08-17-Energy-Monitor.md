---
layout: article
title: "Energy Monitor with Arduino."
categories: media
excerpt: "Energy Monitor with Arduino and CT Sensor using Emonlib Library"
ads: false
share: true
author: juanpintom
image:
  feature: 
  teaser: 
  credit: Name
  creditlink: http://alink.com
---

# Energy Monitor with Arduino

We can meassure power consumption using Emonlib, you can find this library here:
https://github.com/openenergymonitor/EmonLib

##Wiring Diagram: 
![currentvoltage_bb 1](https://cloud.githubusercontent.com/assets/7034151/9333874/333d281e-45cc-11e5-8d51-38f13907ae3b.jpg)

This Wiring Diagram to the Arduino can be used to read Current and Voltage, but you can meassure Current only.

##Scheme:
![current 1](https://cloud.githubusercontent.com/assets/7034151/9333886/41632768-45cc-11e5-925a-b8e07c319c74.png)

Where RVD = 10kohm and Burden to use with SCT-013-000 is 220ohm. 

Note: Remember connect the CT sensor ONLY on one wire.

##Example: 
https://github.com/juanpintom/Souliss_Examples/blob/master/E05_EnergyMonitor_StaticIP_W_Debug.ino
```objective-c
/**************************************************************************
    Souliss - Energy Monitor with Static IP and Debug Enabled.
    
    This example uses EmonLib to read Current. 
    Library can be found here: https://github.com/openenergymonitor/EmonLib
    
    Run this code on one of the following boards:
      - Arduino Ethernet (W5100) 
      - Arduino with Ethernet Shield (W5100)
      
    As option you can run the same code on the following, just changing the
    relevant configuration file at begin of the sketch
      - Arduino with W5200 Ethernet Shield
      - Arduino with W5500 Ethernet Shield
        
***************************************************************************/

#include "EmonLib.h"             // Include Emon Library 
EnergyMonitor emon1;             // Create an instance 

#define CT_PIN  A1               // Pin to CT Sensor 


#define MaCaco_DEBUG_INSKETCH
#define MaCaco_DEBUG  		    1

#define VNET_DEBUG_INSKETCH
#define VNET_DEBUG  		      1

// Configure the framework
#include "bconf/StandardArduino.h"          // Use a standard Arduino
#include "conf/ethW5100.h"                  // Ethernet through Wiznet W5100
#include "conf/Gateway.h"                   // The main node is the Gateway, we have just one node
#include "conf/Webhook.h"                   // Enable DHCP and DNS

// Include framework code and libraries
#include <SPI.h>
#include "Souliss.h"

// This identify the number of the LED logic
#define CURRENT             0
#define WATTS               2
 

uint8_t ip_address[4]  = {192, 168, 1, 77};
uint8_t subnet_mask[4] = {255, 255, 255, 0};
uint8_t ip_gateway[4]  = {192, 168, 1, 1};
#define myvNet_address	ip_address[3]		// The last byte of the IP address (77) is also the vNet address

void setup()
{   
    Serial.begin(115200);
    Initialize();

    Souliss_SetIPAddress(ip_address, subnet_mask, ip_gateway);
	  SetAsGateway(myvNet_address);
    
    Set_Current(CURRENT);
    Set_Power(WATTS);

    emon1.current(CT_PIN, 10);       // Current: input pin, calibration. (use 10 with a 220ohm burden and SCT-013-000)

}

void loop()
{ 
    // Here we start to play
    EXECUTEFAST() {                     
        UPDATEFAST();   
        
        FAST_210ms() {   // We process the logic and relevant input and output every 50 milliseconds
          Logic_Current(CURRENT);
          Logic_Power(WATTS);
        }
        FAST_710ms()    {
            float current = emon1.calcIrms(1480);
            Souliss_ImportAnalog(memory_map, CURRENT, &current); 
            float watt = current*230; 
            Souliss_ImportAnalog(memory_map, WATTS, &watt);
        }
              
        // Here we handle here the communication with Android, commands and notification
        // are automatically assigned to MYLEDLOGIC
        FAST_GatewayComms();                                        
        
    }
} 
```

##Related links:
####Emoncms Web: 
http://emoncms.org/
####Library: 
https://github.com/openenergymonitor/EmonLib


