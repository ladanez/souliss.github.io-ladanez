---
layout: article
title: "The ESP8266 in Commercial Products!"
categories: articles
author: plinio_seniore
excerpt: "Andreas just found an ESP8266 in a cheap RGBWW LED Controller."
tags: [arduino, esp8266, led strib, rgb led]
modified: 2015-08-29
ads: false  
image:
  feature: 2015-08/rgbww_esp8266.JPG
  teaser: 2015-08/rgbww_esp8266-teaser.jpg
  credit: Chaozlabs
  creditlink: http://chaozlabs.blogspot.de/2015/08/esp8266-in-wild-wifi-led-controller-hack.html?m=1
---

The ESP8266 is a cheap WiFi SoC that is getting a growing interest within Makers and many people have asked them-self if this extremely low price (is sold at 5$ for a single piece) is hitting the market of cheap products.

[Andreas](http://chaozlabs.blogspot.de/2015/08/esp8266-in-wild-wifi-led-controller-hack.html?m=1) looking inside an RGBWW (5 channels, 3 for RGB and 2 for White) controller has found an ESP8266 and even the connector to program it with the [Arduino cores](https://github.com/esp8266/Arduino).

<iframe width="1600" height="900" src="https://www.youtube.com/embed/OrIDz9ky8zk" frameborder="0" allowfullscreen></iframe>

This device sells at 10$ for a single piece and can be used with any custom Arduino sketch, like this one below

{% highlight c %}
/**************************************************************************
    Souliss - RGB LED Strip Hack
    
    Control and RGB LED or a Strip using the PWM, fade in/out and flash 
    effects are available as the Android interface or openHAB.
 
    Run this code on one of the following boards:
      - RGBW Led Strip Driver based on ESP8266
    
***************************************************************************/

// Configure the framework
#include "bconf/MCU_ESP8266.h"              // Load the code directly on the ESP8266
#include "conf/Gateway.h"                   // The main node is the Gateway, we have just one node

// **** Define the WiFi name and password ****
#define WIFICONF_INSKETCH
#define WiFi_SSID               "mywifi"
#define WiFi_Password           "mypassword"    

// Include framework code and libraries
#include <ESP8266WiFi.h>
#include <EEPROM.h>
#include "Souliss.h"

#define LEDCONTROL        0
#define LEDRED            1
#define LEDGREEN          2
#define LEDBLUE           3
#define LEDWHITE1         4
#define LEDWHITE2         6

void setup()
{   
    Initialize();

    // Get the IP address from DHCP
    GetIPAddress();                          
    SetAsGateway(myvNet_dhcp);                  // Set this node as gateway for SoulissApp                        
                
    Set_LED_Strip(LEDCONTROL);                  // Set a logic to control a LED strip
    Set_DimmableLight(LEDWHITE1);
    Set_DimmableLight(LEDWHITE2);
   
    // Define inputs, outputs pins
    pinMode(12, OUTPUT);                 // Power the LED
    pinMode(13, OUTPUT);                 // Power the LED
    pinMode(15, OUTPUT);                 // Power the LED    
    pinMode(14, OUTPUT);                 // Power the LED
    pinMode(4,  OUTPUT);                 // Power the LED 
}

void loop()
{ 
    // Here we start to play
    EXECUTEFAST() {                     
        UPDATEFAST();   

        // Execute the code every 1 time_base_fast      
        FAST_10ms() {
                    
            // Execute the logic that handle the LED
            Logic_LED_Strip(LEDCONTROL);
            Logic_DimmableLight(LEDWHITE1);
            Logic_DimmableLight(LEDWHITE2);

            // Use the output values to control the PWM
            analogWrite(12, mOutput(LEDRED)*4);
            analogWrite(13, mOutput(LEDGREEN)*4);
            analogWrite(15, mOutput(LEDBLUE)*4);
            analogWrite(14, mOutput(LEDWHITE1)*4);
            analogWrite(4, mOutput(LEDWHITE2)*4);

            // Just process communication as fast as the logics
            ProcessCommunication();
        } 

        // Process the other Gateway stuffs
        FAST_GatewayComms();
          
    }
    EXECUTESLOW()
    {   
        UPDATESLOW();

        SLOW_10s()  {
        
            // The timer handle timed-on states
            Timer_LED_Strip(LEDCONTROL); 
            Timer_DimmableLight(LEDWHITE1);
            Timer_DimmableLight(LEDWHITE2);                       
        }     
    }       
} 
{% endhighlight %}

A couple of friends are just [getting a sample](https://groups.google.com/forum/?utm_medium=email&utm_source=footer#!msg/souliss/x_ZmFFRWVCo/9-DwshERBgAJ) to use it with Souliss, stay tuned!