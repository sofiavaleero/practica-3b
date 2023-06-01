# INFORME PRACTICA 3b

## CODI:
```

#include <Arduino.h>

//This example code is in the Public Domain (or CC0 licensed, at your option.)
//By Evandro Copercini - 2018
//
//This example creates a bridge between Serial and Classical Bluetooth (SPP)
//and also demonstrate that SerialBT have the same functionalities of a normal Serial

#include "BluetoothSerial.h"

#if !defined(CONFIG_BT_ENABLED) || !defined(CONFIG_BLUEDROID_ENABLED)
#error Bluetooth is not enabled! Please run `make menuconfig` to and enable it
#endif

BluetoothSerial SerialBT;

void setup() {
  Serial.begin(115200);
  SerialBT.begin("ESP32test"); //Bluetooth device name
  Serial.println("The device started, now you can pair it with bluetooth!");
}

void loop() {
  if (Serial.available()) {
    SerialBT.write(Serial.read());
  }
  if (SerialBT.available()) {
    Serial.write(SerialBT.read());
  }
  delay(20);
}
```

# FUNCIONAMENT

Primer, com en totes les pràctiques hem de declarar l'objecte, en aquest cas és el BluetoothSerial que permet conectar i interactuar amb el dispositiu a través de Bluetooth.

En el setup inicialitzem l'objecte(anomenant-lo ESP32test) 

Finalment en el loop inluirem la implementació de que volem que fagi quan el dispositiu s'inicialitzi. En aquest cas amb el primer if revisem si s'ha esccrit text desde la ESP32 i ho mostra al dispositiu. El segon condicional fa que si s'ha escrit el text pel dispositiu ho mostri per la terminal. 
Després de la execució hi ha un delay de 20ms abans de tornar-se a executar el bucle. 

Hi ha un video amb la demostració a la carpeta. 