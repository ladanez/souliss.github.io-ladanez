---
layout: article
title: "Basic tutorial to ESP8266 WIFI."
categories: media
excerpt: "Basic tutorial with images for first steps with modules WIFI ESP8266 in Souliss"
ads: false
share: true
author: ladanez
image:
  feature: 
  teaser: 
  credit: 
  creditlink: 
---

I hope that this tutorial you'll be useful for those like me, we started with the hardware.
In this tutorial only we use the module ESP8266-01, it is the model with only 2 pins GPIO which be able to find.

I thank you who helped me and hope that this manual and others I'll be doing to be useful to the community.


Sorry but I have not been able to put pictures in English.


## HARDWARE: (I do not specified usb wires, PC and other wires conection.)

- ESP8266 module.
![image02](https://cloud.githubusercontent.com/assets/1657291/9608868/d368f570-50d0-11e5-9c3f-77585d4bbc25.jpg)

- FTDI (to connect ESP8266 with to the PC).
![imagen_2b](https://cloud.githubusercontent.com/assets/1657291/10479875/1b73520e-7267-11e5-8e8d-d77420907190.png)

- Protoboard.
![image14](https://cloud.githubusercontent.com/assets/1657291/9608930/269d1abe-50d1-11e5-8779-36ad3ff43c2c.jpg)

- Mobile/Tablet with android for instalation the SOULISS app.


## SOFTWARE:
 
We need install the Arduino IDE to load an sketch on the ESP8266 module. You can find it here: (https://www.arduino.cc/en/Main/Software).

Once downloaded the IDE you need to add the ESP8266 core on Arduino IDE to upload an sketch into the ESP8266.

The following window will open:
![imagen_4](https://cloud.githubusercontent.com/assets/1657291/10479572/771a42b8-7265-11e5-8d97-d36f9ae27d28.png)

In the red area it is necessary write it the same that you can see in the image: (You can see the docs here https://github.com/esp8266/Arduino)

http://arduino.esp8266.com/stable/package_esp8266com_index.json

Once we do this step, we click in Tools >> Boards  >> Boards Manager.
![image08](https://cloud.githubusercontent.com/assets/1657291/9609049/d177a72e-50d1-11e5-82d0-87641dc406a3.png)

In the following window we go down to find it the next:
![image04](https://cloud.githubusercontent.com/assets/1657291/9609068/e522360e-50d1-11e5-8fec-47795e02513c.png)

Click the button “Install”. In my windows it is already installed and in the button you can see “Removed”. 

To review that all it is ok, you return to the menu Tools >> Boards >> Boards Manager. And in the below of menu you can see Boards ESP8266 Generic. If you can see that, you have the install perfectly.

We selected this boards and we put the default configuration like that:
![image16](https://cloud.githubusercontent.com/assets/1657291/9609152/6bb1a632-50d2-11e5-82a7-f917fa3203ab.png)

I've been using to this tutorial exactly this model of Banggood  (http://www.banggood.com/es/Upgraded-Version-1M-Flash-ESP8266-ESP-01-WIFI-Transceiver-Wireless-Module-p-979509.html)  and however the sketch load up well. So if you have similar boards, do not worry, sure you can load with this configuration.

Now, we have configured the software needed to load any sketch that we want in the module ESP8266.


#### FTDI connection with ESP8266..

** IMPORTANT!!! The module ESP8266 works with 3,3V, we NEVER connect to 5v if you do not want burn it. **

- Connection of  FTDI.
![image22](https://cloud.githubusercontent.com/assets/1657291/9610456/ff83dbd0-50d9-11e5-9918-343b2ff7bc33.png)


- Connection module ESP8266.
![image18](https://cloud.githubusercontent.com/assets/1657291/9610462/0edaa6ea-50da-11e5-8ef2-812ebdd21a24.png)


To program the module, we need connect the FTDI with ESP of this way:

#### FTDI:

    - The RX pin must be connected to TX of the ESP8266.
    - The TX pin must be connected to RS of the ESP8266.
    - Its 3,3v give its energy to all circuit
    - ●	The ground it will be the ground to all circuit.

#### En el ESP8266:

    - The RX pin must be connected to TX of the FTDI.
    - The TX pin must be connected to RX of the FTDI.
    - The VCC pin must be connected to 3,3v
    - The GND pin is connected to (GND protoboard/breadboard).
    - The GPIO0 pin connect it to GND, this only is necessary while load the sketch into the module ESP8266. When we finish to load the sketch we must unconnect this pin.
    - The GPIO2 for the moment, don´t connect. We will use to test the led.
    - The CH_PD connect it to 3,3v to work the module.
    - ●	And the RST pin, if you want to reboot the module we connect to ground, during 1 second, this reboot the module. My advice is connect to button, like you see in the image, because sometimes the load of sketch failed and we need reboot the module while load the sketch. 

In my project is something like this (I am sorry for quality of photo, and I know that it is not very good, however I hope you like to get an idea):

Note. In the picture you can see how the GPIO2 is connected to a led and this to ground. You can put it directly like this, because the program will use the GPIO2 to turn on the led.

![image11](https://cloud.githubusercontent.com/assets/1657291/9610468/19170126-50da-11e5-8e43-5d786e01dcf9.jpg)

![image20](https://cloud.githubusercontent.com/assets/1657291/9610478/2aa51f72-50da-11e5-83bf-449cb42a347b.jpg)

How the quality of the photos it is not good, I write any link to you can see how will be, Note that not everyone has the FTDI pins located in the same way, so be careful with that.

https://importhack.files.wordpress.com/2014/11/esp8266-reflash-firmware.png?w=590&h=242
http://www.martyncurrey.com/wp-content/uploads/2014/12/ESP8266-01-to-FTDI-281x300.jpg
https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcSZvJV-pVyldULYuZXVxUsmek3o-ywbzPKLabE1VGqHpBx62lcpLA

In some images you can see a resistance to rx/tx pin and this to ground. If i do not mistake, it is use to delete interference in the transmission, it is not necessary, but recommended.

Well, we come to this point we have the software to load the sketch, the FTDI and ESP8266 correctly connected each other and work it.

Now we load the sketch in the module ESP8266. We open arduino program and selected the boards like we saw at the beginning of the tutorial

Is important connect the port that we have to the FTDI, Es importante conectar el puerto que tengamos para el FTDI, if not we do not load the sketch to the module.

![image16](https://cloud.githubusercontent.com/assets/1657291/9610490/33ee680e-50da-11e5-96ec-d4339436d756.png)

Now and after to load the program, we need download the libraries of souliss to not  have problems of compilation.
To this we go to the project web and download the zip of the project.


Once we have it downloaded, is necessary put in the program that it use this libraries to do the compilation of the project.


We do selected in Program >> Include Library >> Add .ZIP library.
![image03](https://cloud.githubusercontent.com/assets/1657291/9610503/3ff56d14-50da-11e5-9706-d7e1ab862e0f.png)

In the window shown we looking for the zip you just downloaded and select it.
Now, we can load the sketch into the module ESP8266.

The sketch that we use is the basic example that we can find it in the repository Github of Souliss, here is it the direct link. With one exception, in the source code that I shown, I use the GPIO2 pin to the switch on/off of a led. This you can see the code in **bold**.

In the code with **bold** lines, you must set the same name of your SSID, this is the name of your wifi. In my case BOFH_WIFI.

```objective-c
/**************************************************************************
        Souliss - Hello World for Expressif ESP8266
        This is the basic example, create a software push-button on Android
        using SoulissApp (get it from Play Store).  
        Load this code on ESP8266 board using the porting of the Arduino core
        for this platform.
***************************************************************************/

// Configure the framework
#include "bconf/MCU_ESP8266.h"                  // Load the code directly on the ESP8266
#include "conf/Gateway.h"                       // The main node is the Gateway, we have just one node
#include "conf/IPBroadcast.h"
// **** Define the WiFi name and password ****
#define WIFICONF_INSKETCH
#define WiFi_SSID       "SSID"
#define WiFi_Password   "PASSWORD"
// Include framework code and libraries
#include <ESP8266WiFi.h>
#include <EEPROM.h>
#include "Souliss.h"
// This identify the number of the LED logic
#define MYLEDLOGIC              0                  

// **** Define here the right pin for your ESP module ****
//This is my modification of GPIO2 named it above.
#define    OUTPUTPIN                    2
//########################
void setup(){  
        Initialize();
        // Connect to the WiFi network and get an address from DHCP
        GetIPAddress();                              
        SetAsGateway(myvNet_dhcp);           // Set this node as gateway for SoulissApp  
        // This is the vNet address for this node, used to communicate with other
        // nodes in your Souliss network
        SetAddress(0xAB01, 0xFF00, 0x0000);
        SetAsPeerNode(0xAB02, 1);
        Set_SimpleLight(MYLEDLOGIC);            // Define a simple LED light logic
        pinMode(OUTPUTPIN, OUTPUT);             // Use pin as output
}
void loop(){
        // Here we start to play
        EXECUTEFAST() {                        
            UPDATEFAST();  
            FAST_50ms() {   // We process the logic and relevant input and output every 50 milliseconds
                Logic_SimpleLight(MYLEDLOGIC);
                DigOut(OUTPUTPIN, Souliss_T1n_Coil,MYLEDLOGIC);
            }
            // Here we handle here the communication with Android
            FAST_GatewayComms();                                            
        }
}
```

Now we do a test to sure that all it is right, before we load in ESP8266, we can click Verify. This makes a compilation and warns us that everything has gone well or if there have been failures in the code.
![image09](https://cloud.githubusercontent.com/assets/1657291/9610686/691b066c-50db-11e5-9c44-e2a46706705c.png)

If all went well, now we can load the sketch in the module. To do that we push the button with an arrow next to the button which we pressed before.

If when we try to load the sketch show us the next message:
error: espcomm_open failed, it usually because do not transfer the code in the ESP.

I resolved this pushing the button of reboot just after that show me the next message:

Sketch uses 309.752 bytes (71%) of program storage space. Maximum is 434.160 bytes.
Global variables use 49.224 bytes (60%) of dynamic memory, leaving 32.696 bytes for local variables. Maximum is 81.920 bytes.

in the serial out.


If all goes well, we should see something like this.
![image13](https://cloud.githubusercontent.com/assets/1657291/9610710/87db09f8-50db-11e5-88b6-378f92b74d84.png)

**Once load the SKETCH, should get out the connection to ground with the GPIO0 pin.**

We only have one more step. Install the app in the mobile phone or tablet and configure it to do the test to be sure that the load of sketch it is correctly.

To do this, we need two programs, the Souliss app and the Fing application. We can download them of Play Store.

The Fing application we will use to know the IP that our router put to module ESP.


#### FING.
You open the app in your phone, and this it connected to your wifi.
We press the round arrow on top and it start to scan all device connected to our wifi.
In my case my module has the IP 192.168.1.37 like Espressif.

If you can't see it, verify the unconnected of GIPO0 to the ground. And you do the reboot to the module.

![image00](https://cloud.githubusercontent.com/assets/1657291/9610775/d8cd3a70-50db-11e5-97e5-93acb3b8d2f1.png)

Now, we know the ip of our module. This module is the gateway of Souliss.

We open the app Souliss in Phone or Tablet.
![image17](https://cloud.githubusercontent.com/assets/1657291/9610788/f23742d0-50db-11e5-94c5-ae35481e425a.jpg)

We must see something like that.

Press the three dots beside OFFLINE red in the upper right corner. And access the configuration menu.

In the menu, in the left side selected Net options and in the new menu which shown, where in the option where it is says “Souliss local address” we set the IP direction of our new module, in my case 192.168.1.37.

![image25](https://cloud.githubusercontent.com/assets/1657291/9610799/ffafc46e-50db-11e5-8d26-a879460ade9e.jpg)

Now, we have our gateway module making in our system.

You close it completely and reopen it to make sure that you see something like that:

![image05](https://cloud.githubusercontent.com/assets/1657291/9610807/0e0229e4-50dc-11e5-82b8-96863af82ee8.jpg)

Now let's run a test using the gateway module which we just added.

Note that this is the most basic steps and that it can be improved greatly.


We access to the menu in the upper right part where the “SoulissApp” text appears and select manual. Show it a message that tells us that do not appears database of devices. And we go to the next option in which press "Get Souliss Nodes". We will show up a warning, we press OK and we continue.

![image23](https://cloud.githubusercontent.com/assets/1657291/9610812/1debf7f4-50dc-11e5-8f90-a674a97004f3.jpg)

Once we do it that, it show us the node 0. It is the gateway. ( if do not see that, reboot the app).

![image01](https://cloud.githubusercontent.com/assets/1657291/9610820/2866cc72-50dc-11e5-8bfc-e2dcf2620772.png)

We select the node 0, now we can see how our led switch on/off.

![image21](https://cloud.githubusercontent.com/assets/1657291/9610825/33e863c6-50dc-11e5-9555-61ecf15848dc.jpg)



**IMPORTANT NOTES.**

It can happen that the FTDI module it is unable to provide sufficient amps. The module itself does not use much power, but it could happen that the usb that only give 0.5 amps, this it is not enough, less if you want to connect a relay.
So it is recommended, but not absolutely necessary for the basic test, connect an external power supply that assures us that at least more than 500mA which gives the computer's USB.

Note that if connect externally to power supply, the pins that are used from the FTDI are not needed.

To use an external power supply we can buy different modules and we have many ways to do:

- Connecting a mobile phone charger. There are some mobile charger that allows connecting a USB cable. We will use this module and connect to FTDI. It is easy and safe. Such chargers usually provide 0.8A.
![image10](https://cloud.githubusercontent.com/assets/1657291/9610839/5474ac76-50dc-11e5-8a21-8868b663b1b9.jpg)

- Connecting a computer power supply and extract the necessary voltage pins that connect to the board. There are many videos which explains how to do it. This way is relatively safe, since the power supplies of computers, have good regulators and the tensions are accurate.
![image12](https://cloud.githubusercontent.com/assets/1657291/9610848/5fa7cbfa-50dc-11e5-8e8f-257eed02ce87.jpg)

- You can also connect through a battery connector, taking care not to exceed the 3.5V maximum allowed to ESP8266. You can adjust the tension with a cheapie module like this.
![image07](https://cloud.githubusercontent.com/assets/1657291/9610863/70cc69e0-50dc-11e5-87a4-1b591cce08cc.jpg)
![image15](https://cloud.githubusercontent.com/assets/1657291/9610864/70f0a562-50dc-11e5-93f0-1bacdb995c34.jpg)

-●	Finally you can use a cheap module that supply the circuit through the breadboard. The only thing to consider in this module is to put the Jumper (in red) in 3.3v, always supply the circuit with at least 9V. If you do it through a mobile phone charger; with jumper on 3.3V, do not supply more than 2.5V, but if you put the jumper on 5v, the output provides 3.6v, high, but safe to supply the circuit.
![image24](https://cloud.githubusercontent.com/assets/1657291/9610871/82323de0-50dc-11e5-8c54-9b8633534cc4.png)

Note for purchasing this module. Observe welding skewers that go to the breadboard. In my case the weld was bad, as I do: -D, and were linked. So when I plugged, he began to take a nice smoke through the input transistor. 
Forewarned :-D
