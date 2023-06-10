# Practica ESP32 con HC-SR04 CON LCD 
Este repositorio muestra como podemos programar una ESP32 con el sensor DHT11.

## Introducción

### Descripción

La ```Esp32``` la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor (```HC-SR04```) para adquirir la distancia ; Cabe aclarar que esta practica se usara un simulador llamado [WOKWI](https://https://wokwi.com/).


## Material Necesario

Para realizar esta practica necesitas lo siguiente

- [WOKWI](https://https://wokwi.com/)
- Tarjeta ESP 32
- HC-SR04
- LCD 16X2 (I2C)
- VCC
- GND



## Instrucciones

### Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://https://wokwi.com/).


### Instrucciones de preparación de entorno 

1. Abrir la terminal de programación y colocar la siguente programación:

```
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 27;   //Pin digital 3 para el Echo del sensor


LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(9600);//iniciailzamos la comunicación
  lcd.init();
  lcd.backlight();
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
}

void loop()
{

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);

  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t / 59;           //escalamos el tiempo a una distancia en cm

  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  delay(1000);          //Hacemos una pausa de 100ms

  lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(d)+"cm ");
  lcd.setCursor(0, 1);
  lcd.print("Wokwi Online IoT");
  delay(1000);
  lcd.setCursor(0,0);
  lcd.print(" Ing. Mecanica  ");
  lcd.setCursor(0,1);
  lcd.print(" Sergio Rivera ");
  delay (1000);
}

```
2. Instalar la libreria de **DHT sensor library for ESPx** como se muestra en la siguente imagen.

![](https://github.com/ser2784/PRACTICA-HC-SR04-CON-LCD/blob/main/CODIGO%20HC-SR04.png)

3. Hacer la conexion de **HC-SR04** Y el **LCD** con la **ESP32** como se muestra en la siguente imagen.

![](https://github.com/ser2784/PRACTICA-HC-SR04-CON-LCD/blob/main/HC-SR04%20DIAGRAMA.png)

### Instrucciónes de operación

1. Iniciar simulador.
2. Visualizar los datos en el monitor serial.
3. Colocar la Distancia  dando *doble click* al sensor **DHT22** 
4. se cloca la carrera y el nombre del alumno.

## Resultados

Cuando haya funcionado, verás los valores el nombre y la carrera del alumno dentro del monitor serial como se muestra en la siguente imagen.

![](https://github.com/ser2784/PRACTICA-HC-SR04-CON-LCD/blob/main/HC-SR04%20DISTANCIA%20EN%20EL%20LCD.png)
![](https://github.com/ser2784/PRACTICA-HC-SR04-CON-LCD/blob/main/HC-SR04%20NOMBRE%20EN%20EL%20LCD.png)



## Evidencias

[por el momrnto no contamos con el video ]


# Créditos

Desarrollado por Ing. Sergio Rivera 

- [GitHub](https://github.com/ser2784)