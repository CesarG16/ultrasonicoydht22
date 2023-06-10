## CESAR AUGUSTO GONZALEZ INFANTE
# Práctica Sensor ultrasonico con LCD y DHT22

## Programación

```
#include <LiquidCrystal_I2C.h>
#include "DHTesp.h"
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int Trigger = 14;   //Pin digital 2 para el Trigger del sensor
const int Echo = 26;   //Pin digital 3 para el Echo del sensor

const int DHT_PIN = 15;

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);
void setup() {
 Serial.begin(9600);
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
    dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
    lcd.init();
  lcd.backlight();
}

void loop()
{

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print(" Cm");
  Serial.println();
  delay(1000);          //Hacemos una pausa de 100ms

  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
   delay(1000); 

  lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(d) +"Cm ");
   lcd.setCursor(0, 1);
  lcd.print("CESAR GONZALEZ ");
  delay(1000);          //Hacemos una pausa de 100ms
  
  lcd.setCursor(0, 0);
  lcd.println("  Temp: " + String(data.temperature, 1) + " C ");
  lcd.setCursor(0, 1);
  lcd.println("  Humidity: " + String(data.humidity, 1) + "%");
  lcd.println("---");
   delay(1000);  
}

```

## Librerías

1. **DHT sensor library for ESPx**
2. **LiquidCrystal I2C**
![](https://github.com/CesarG16/ultrasonicoydht22/blob/main/eje13.png?raw=true)
## Conexión

![](https://github.com/CesarG16/ultrasonicoydht22/blob/main/eje16.png?raw=true)

## Funcionamiento del programa

![](https://github.com/CesarG16/ultrasonicoydht22/blob/main/eje14.png?raw=true)
![](https://github.com/CesarG16/ultrasonicoydht22/blob/main/eje15.png?raw=true)

## Evidencias

[Página](https://wokwi.com/projects/367191861520219137)


# Créditos

Desarrollado por Ing. Cesar Augusto Gonzalez Infante

- [GitHub](https://github.com/CesarG16)