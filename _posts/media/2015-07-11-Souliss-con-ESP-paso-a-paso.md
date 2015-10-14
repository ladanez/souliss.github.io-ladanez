---
layout: article
title: "Tutorial Basico para el ESP WIFI."
categories: media
excerpt: "Cuestiones basicas con imagenes para los primeros pasos con los modulos ESP WIFI en Souliss"
ads: false
share: true
author: luisadanez
image:
  feature: 
  teaser: 
  credit: 
  creditlink: 
---

Bueno, este tutorial básico espero os sea útiles a los que como yo, empezamos en esto del hardware.
Tan solo trataremos de usar, en un principio, el módulo ESP8266-01 que es un modelo con menos pines de uso (GPIO) del mercado.

Agradezco a los que me habéis ayudado a orientarme un poco y espero que este manual y otros esté en desarrollo y mejoras para que sea útil a la comunidad.


## HARDWARE: (No especificó los cables usb, ordenador y cableado para las conexiones)

- Módulo ESP8266.
![image02](https://cloud.githubusercontent.com/assets/1657291/9608868/d368f570-50d0-11e5-9c3f-77585d4bbc25.jpg)

- FTDI (para poder conectar el módulo ESP8266 al ordenador).
![imagen_2b](https://cloud.githubusercontent.com/assets/1657291/10479875/1b73520e-7267-11e5-8e8d-d77420907190.png)

- Protoboard.
![image14](https://cloud.githubusercontent.com/assets/1657291/9608930/269d1abe-50d1-11e5-8779-36ad3ff43c2c.jpg)

- Móvil/Tablet con android para la instalación del programa SOULISS.


## SOFTWARE:
Para poder introducir el sketch en el módulo es necesario instalar el programa arduino que podeis encontrar aqui.(https://www.arduino.cc/en/Main/Software)

Una vez descargado es necesario realizar una actualización de un módulo para poder “grabar” el proyecto (sketch) sobre el módulo ESP8266.

Para ello una vez instalado el programa Arduino iremos al menú superior Archivo >> Preferencias

Se abrirá la siguiente ventana:
![imagen_4](https://cloud.githubusercontent.com/assets/1657291/10479572/771a42b8-7265-11e5-8d97-d36f9ae27d28.png)

En el área que se muestra en rojo es necesario escribir lo siguiente, como se puede ver en la imagen: (podéis ver la documentación aqui https://github.com/esp8266/Arduino)

http://arduino.esp8266.com/stable/package_esp8266com_index.json

Una vez hecho este paso, vamos a Herramientas >> Placa (la que este seleccionada) >> Boards Manager.
![image08](https://cloud.githubusercontent.com/assets/1657291/9609049/d177a72e-50d1-11e5-82d0-87641dc406a3.png)

Se mostrará la siguiente ventana y hay que bajar hasta encontrar lo siguiente:
![image04](https://cloud.githubusercontent.com/assets/1657291/9609068/e522360e-50d1-11e5-8fec-47795e02513c.png)

Darle al botón “Install” en mi caso como ya está instalado se muestra “Removed”. Paciencia porque tarda un poco, aunque depende de cada conexión de internet.

Para comprobar que todo ha ido correctamente volved a acceder a  Herramientas >> Placa (la que esté seleccionada) >> Boards Manager. Y en la parte inferior del menú deberá verse la placa ESP8266 Generic. 

Seleccionamos dicha placa y dejamos la configuración por defecto que suele ser:
![image16](https://cloud.githubusercontent.com/assets/1657291/9609152/6bb1a632-50d2-11e5-82a7-f917fa3203ab.png)

En mi caso mi placa ESP8266 es exactamente este modelo de Banggood  (http://www.banggood.com/es/Upgraded-Version-1M-Flash-ESP8266-ESP-01-WIFI-Transceiver-Wireless-Module-p-979509.html)  y sin embargo a cargado correctamente el sketch. Así que si tenéis esta o placas similares no os preocupeis, seguro que os carga con esta configuración.

En este momento, ya tenemos configurado el software necesario para cargar cualquier sketch que queramos sobre el módulo ESP8266.

#### Conexión de FTDI con ESP8266.

**!!! IMPORTANTÍSIMO!!! El módulo ESP8266 funciona a 3,3V, de manera que no se debe conectar a un voltaje de 5v si no quieres fundirlo.**

- Conexiones de FTDI.
![image22](https://cloud.githubusercontent.com/assets/1657291/9610456/ff83dbd0-50d9-11e5-9918-343b2ff7bc33.png)


- Conexiones del módulo ESP8266.
![image18](https://cloud.githubusercontent.com/assets/1657291/9610462/0edaa6ea-50da-11e5-8ef2-812ebdd21a24.png)


Para programar el módulo quedaría todo de la siguiente forma:

#### En el FTDI:

    - El RX deberá conectarse con el TX del ESP8266.
    - El TX deberá conectarse con el RS del ESP8266.
    - Los 3,3v alimentarán todo el circuito.
    - El GND será la masa de todo el circuito.

#### En el ESP8266:

    - El RX se conectará al TX del FTDI.
    - El TX se conectará al RX del FTDI.
    - El VCC se conectará a 3,3v.
    - El GND se conectará a masa (GND).
    - El GPIO0 se conectará a masa, esto solo es necesario para introducir el programa(Sketch). Una vez instalado el programa es necesario quitarlo.
    - El GPIO2 de momento no lo conectamos a nada. Ya veremos según el programa.
    - El CH_PD es necesario ponerlo a 3,3v para que funcione el módulo.
    - Y el RST en el caso que queramos resetear el módulo, lo conectamos a GND, durante 1 seg, esto ejecuta el reset en el módulo. Mi consejo es conectarlo a un botón, como podéis ver en la imagen, ya que para la carga del sketch va a ser necesario. 

En mi caso queda algo así (Siento la definición y la foto, ya que no es muy buena, no obstante espero que os sirva para haceros una idea):

Nota. En la imagen podéis ver como el GPIO2 está conectado a un led y este a su vez a masa. Podéis ponerlo directamente así, ya que el programa que cargaremos a continuación usará el GPIO2 para encender dicho led.

![image11](https://cloud.githubusercontent.com/assets/1657291/9610468/19170126-50da-11e5-8e43-5d786e01dcf9.jpg)

![image20](https://cloud.githubusercontent.com/assets/1657291/9610478/2aa51f72-50da-11e5-83bf-449cb42a347b.jpg)

Como la calidad de las fotos no es muy buena, pongo varios enlaces para que veais como sería, tened en cuenta que los FTDI no todos tienen los pines situados de la misma forma, así que tened cuidado con eso.

https://importhack.files.wordpress.com/2014/11/esp8266-reflash-firmware.png?w=590&h=242
http://www.martyncurrey.com/wp-content/uploads/2014/12/ESP8266-01-to-FTDI-281x300.jpg
https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcSZvJV-pVyldULYuZXVxUsmek3o-ywbzPKLabE1VGqHpBx62lcpLA

En algunas imagenes podeis ver una resistencia en el rx/tx que van a masa. Si no me equivoco se usan para eliminar interferencias en la transmisión, no es necesaria, pero si recomendable.

Bueno, llegados a este punto ya tenemos, el software para cargar el sketch y el FTDI y ESP8266 correctamente conectados y funcionando.

Ahora vamos a cargar el sketch en el módulo. Abrimos el programa arduino y seleccionamos el board como hemos visto al principio del tutorial.

Es importante conectar el puerto que tengamos para el FTDI, sino no podremos transferir el proyecto al módulo.

![image16](https://cloud.githubusercontent.com/assets/1657291/9610490/33ee680e-50da-11e5-96ec-d4339436d756.png)

Ahora y antes de cargar el programa, necesitamos descargarnos las librerías de souliss para que no tengamos problemas de compilación.

Para ello accedemos a la página del proyecto y descargamos el zip del proyecto.

Una vez lo tengamos descargado es necesario decirle a nuestro programa Arduino que use estas librerías para realizar la compilación de nuestro proyecto.

Lo haremos seleccionando en Programa >> Include Library >> Add .ZIP library.

![image03](https://cloud.githubusercontent.com/assets/1657291/9610503/3ff56d14-50da-11e5-9706-d7e1ab862e0f.png)

En la ventana que se muestra buscamos el zip que acabamos de descargar y lo seleccionamos.

Llegados a este punto tan solo nos queda grabar el sketch dentro del módulo ESP8266.

El sketch que vamos a usar es el ejemplo básico que podemos encontrar en el repositorio de Github de souliss, aqui está el enlace directo. Con una salvedad, en el código que muestro a continuación, ya he establecido el uso del PIN GPIO2 para el encendido y apagado de un led. Este punto puedes verlo en el codigo en **negrita**.

En el código las líneas en **negrita**, debéis establecer el nombre de tu SSID, esto es el nombre de la wifi a la que te conectas. En mi caso BOFH_WIFI.
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
//ESTA ES LA MODIFICACION DEL USO DEL PIN GPIO2 PARA EL MODULO ESP8266
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

Para hacer una prueba de que todo va bien, antes de meterlo en el ESP8266 podemos pulsar Verificar. Esto realizará una compilación y nos avisará que todo ha ido bien o si se han producido fallos.
![image09](https://cloud.githubusercontent.com/assets/1657291/9610686/691b066c-50db-11e5-9c44-e2a46706705c.png)


Si todo ha ido bien, ya podemos cargar el sketch dentro del módulo, para eso pulsaremos el botón con una flecha junto a que acabamos de pulsar para hacer la prueba.
Si cuando tratamos de realizar este paso nos aparece el mensaje:
error: espcomm_open failed suele ser porque no logra transferir correctamente al módulo ESP8266.
Yo lo solucione con pulsar el botón de reset justo después de que se mostrará el mensaje:

_Sketch uses 309.752 bytes (71%) of program storage space. Maximum is 434.160 bytes.
Global variables use 49.224 bytes (60%) of dynamic memory, leaving 32.696 bytes for local variables. Maximum is 81.920 bytes._

en la salida de datos.

Si todo ha ido bien deberíamos ver algo parecido a esto.
![image13](https://cloud.githubusercontent.com/assets/1657291/9610710/87db09f8-50db-11e5-88b6-378f92b74d84.png)

**Una vez cargado el SKETCH, debemos quitar la conexión a GND del GPIO0.**

Ya tan solo nos queda un paso más. Instalar la aplicación en el móvil/tablet y configurarlo para realizar la prueba de que la carga ha ido correctamente.

Para ello necesitamos dos programas, lógicamente la aplicación Souliss y también la aplicación Fing. Ambas aplicaciones podemos descargarla desde Play Store.

La aplicación fing la usaremos para saber que ip le ha asignado el router a nuestro módulo.

#### FING.
Abrimos la aplicación desde nuestro móvil, que tenemos conectado a nuestra wifi.

Pulsamos en la flecha circular de la parte superior y comenzará a escanear todos los dispositivos conectados a nuestra wifi. En mi caso el modulo ESP8266 aparece con la ip 192.168.1.37 como Espressif.

Si No te apareciera, comprueba que has quitado el GPIO0 de la masa (GND). Y hazle un Reset.

![image00](https://cloud.githubusercontent.com/assets/1657291/9610775/d8cd3a70-50db-11e5-97e5-93acb3b8d2f1.png)

Ya tenemos la IP de nuestro módulo ESP8266 que está haciendo de Gateway en Souliss.

Ahora abrimos la aplicación Souliss de nuestro android. En mi caso una tablet.
![image17](https://cloud.githubusercontent.com/assets/1657291/9610788/f23742d0-50db-11e5-94c5-ae35481e425a.jpg)

Veremos algo así.

Pulsamos en los tres puntos que hay junto a OFFLINE en rojo en la esquina superior derecha. Y accedemos al menú de configuración.

En el menú, en la parte izquierda seleccionamos Opciones de Red y en el nuevo menú que nos muestra, en la opción donde pone “Dirección local de Souliss (obligatorio)” establecemos la ip de nuestro flamante nuevo módulo, en mi caso la ip 192.168.1.37.
![image25](https://cloud.githubusercontent.com/assets/1657291/9610799/ffafc46e-50db-11e5-8d26-a879460ade9e.jpg)

Ya tenemos el módulo haciendo de gateway en nuestro sistema.

Cierra completamente y vuelve a abrirla para comprobar que se muestra algo parecido a lo siguiente:

![imagen_18](https://cloud.githubusercontent.com/assets/1657291/10479980/bdb1e008-7267-11e5-8257-72929fd5070d.jpg)

Ahora vamos a realizar una prueba del uso del módulo gateway que acabamos de añadir.

Tened en cuenta que esto es los pasos más básicos y que es posible mejorarlo mucho en cuanto a la configuración.


Accedemos al menú de la parte superior derecha donde aparece el texto SoulissApp y seleccionamos manual. Nos aparece un mensaje en el que nos avisa que no hay base de datos de dispositivos. Y nos lleva a la siguiente opción en la que pulsaremos “Get Souliss Nodes”. Nos saldrá un mensaje de advertencia, le damos Ok y continuaremos.

![image23](https://cloud.githubusercontent.com/assets/1657291/9610812/1debf7f4-50dc-11e5-8f90-a674a97004f3.jpg)

Una vez hecho esto, se nos mostrará el nodo 0, que es la gateway. (si no aparece, reiniciar la aplicación).

![image01](https://cloud.githubusercontent.com/assets/1657291/9610820/2866cc72-50dc-11e5-8bfc-e2dcf2620772.png)

Ya seleccionamos el Nodo 0, y ya podemos ver como actúa encendiendo y apagando nuestro led.

![imagen_20](https://cloud.githubusercontent.com/assets/1657291/10479990/e23becc0-7267-11e5-859a-db0f879b1399.jpg)




**NOTAS A TENER EN CUENTA.**

Puede ocurrirnos que el módulo FTDI no sea capaz de dar la suficiente intensidad (Amperios). El módulo por sí solo no usa mucho, pero podría darse el caso que el usb que solo suele dar unos 0,5 amperios no sea suficiente, menos aún si queremos conectar un actuador. Por lo que es recomendable, aunque no totalmente necesario para la prueba básica, conectarle un alimentador externo que nos asegure que al menos más de los 500mA que nos da el USB del equipo.

Tened en cuenta que si lo conectais de forma externa, los pines que se usan desde el FTDI ya no son necesarios.

Para ello existen varios módulos y formas de hacerlo:

- Conectar un cargador de móvil. Hay algunos cargadores de móvil que permite conectarle un cable usb. Usaremos este módulo y lo conectaremos al FTDI. Es sencillo y seguro. Ese tipo de cargadores suelen proporcionar 0,8A.
![image10](https://cloud.githubusercontent.com/assets/1657291/9610839/5474ac76-50dc-11e5-8a21-8868b663b1b9.jpg)

- Conectar un fuente de alimentación de ordenador y extraer el voltaje necesario de los pines que se conectan a la placa. Hay muchos videos donde se explica como hacerlo. Esta forma es relativamente segura, ya que las fuentes de alimentación de ordenadores, tienen buenos reguladores y las tensiones son exactas.
![image12](https://cloud.githubusercontent.com/assets/1657291/9610848/5fa7cbfa-50dc-11e5-8e8f-257eed02ce87.jpg)

- También podéis conectar pilas a través de un conector, teniendo cuidado de no superar los 3,5v máximo que permite el ESP8266. Podéis regular la tensión con un módulo muy baratito como este.
![image07](https://cloud.githubusercontent.com/assets/1657291/9610863/70cc69e0-50dc-11e5-87a4-1b591cce08cc.jpg)
![image15](https://cloud.githubusercontent.com/assets/1657291/9610864/70f0a562-50dc-11e5-93f0-1bacdb995c34.jpg)

-Por último podéis usar un módulo que es barato para poder alimentar el circuito a través de la protoboard. Lo único que hay que tener en cuenta en este módulo es poner los Jumper (en rojo) en 3,3v, siempre que alimentan el circuito con al menos 9V, si lo haceis como yo a través de un cargador de móvil; con los jumper en 3,3v, no da de salida más de 2,5v, pero si pones los jumper en 5v, la salida proporciona 3,6v, alto, pero seguro para alimentar el circuito de protoboard.
![image24](https://cloud.githubusercontent.com/assets/1657291/9610871/82323de0-50dc-11e5-8c54-9b8633534cc4.png)

Nota para los que compreis este módulo. Echad un vistazo a la soldadura de los pinchos que van a la placa protoboard. En mi caso la soldadura era de las malas, como las que hago yo, y estaban puenteados. De manera que cuando lo conecte, comenzó a echar un agradable humillo a través del transistor de la entrada y me quede con cara de tonto. Avisados quedáis :-D.
