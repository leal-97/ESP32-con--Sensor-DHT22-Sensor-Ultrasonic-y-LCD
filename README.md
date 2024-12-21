# ESP32-con--Sensor-DHT22-Sensor-Ultrasonic-y-LCD
## Práctica de Tarjeta ESP32 con sensor DHT22, Sensor Ultrasonic y Screen LCD para monitoreo de temperatura, humedad y distancia.

En este repositorio muestraré como programar una tarjeta ESP32 utillizando un sensor DHT22 y una Screen LCD para monitorear humedad, temperatura y distancia del entorno que mostrará los resultados cada 2s.
## ESP32
Es un microcontrolador revolucionario que se ha vuelto esencial en la tecnología moderna. Es un sistema en chip (SoC) de bajo costo y bajo consumo de energía con una combinación de capacidades Wi-Fi y Bluetooth. 

1.	**30 Pines de E/S:** Ofrece una amplia variedad de pines para la conexión de sensores, actuadores y otros dispositivos.
2.	**Alimentación:** Puede ser alimentado a través de un puerto MicroUSB o mediante otros métodos de suministro de energía.
3.	**Wi-Fi y Bluetooth Integrados:** Facilita la conectividad inalámbrica para la comunicación y el control remoto.
4.	**Capacidades de Programación:** Se puede programar utilizando el entorno de desarrollo de Arduino o herramientas específicas de Espressif.
Aplicaciones Comunes:
1.	**Proyectos de IoT (Internet de las Cosas):** Ideal para dispositivos conectados a la red que requieren comunicación inalámbrica.
2.	**Sistemas Embebidos:** Puede ser utilizado en sistemas embebidos para controlar y monitorear dispositivos.
3.	**Desarrollo de Prototipos:** Ampliamente utilizado en el desarrollo de prototipos debido a su facilidad de programación y su capacidad de conexión a una variedad de dispositivos.

## Sensor DHT22
El DHT22 es un sensor digital de humedad y temperatura que ofrece mediciones precisas y de alta calidad. Está compuesto por un pequeño circuito integrado y un sensor capacitivo de humedad y temperatura. 
Es ampliamente utilizado en aplicaciones que requieren un monitoreo preciso del entorno.
Características Principales:
-	**Medición de Humedad y Temperatura:** Proporciona mediciones digitales de humedad relativa y temperatura ambiente.
- **Bajo Consumo de Energía:** Opera con un bajo consumo de energía, lo que lo hace adecuado para aplicaciones con restricciones de energía.
- **Tiempo de Respuesta Rápido:** Proporciona mediciones actualizadas en intervalos cortos de tiempo.

 Aplicaciones Comunes:

- Sistemas de monitoreo de clima interior y exterior.
- Proyectos de automatización del hogar.
- Dispositivos de control ambiental y climatización.

## Material
- https://wokwi.com/
- ESP32
- DHT22
- LCD 16x2 ILC
- Sensor HC-SR04
  
## Instrucciones:
- **1.- Entrar al siguiente enlace:** https://wokwi.com/
- **2-. Seleccionar la tarjeta ESP32**

![]( https://github.com/leal-97/ESP32-con-sensor-DHT22/blob/main/esp32kd.jpeg )
  
- **3.- Bajar el cursor hasta starter templates y seleccionar ESP32 una vez más**

![]( https://github.com/leal-97/ESP32-con-sensor-DHT22/blob/main/starter.jpeg )


- **4.- En el cuadro de programación borrar el código default y pegar este:**

```
const int Trigger = 4;     //Pin digital 2 para el Trigger del sensor
const int Echo = 15;      //Pin digital 3 para el Echo del sensor

#include <LiquidCrystal_I2C.h> //Librería
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES); //librería

void setup() 
{
  Serial.begin(9600);                //iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT);         //pin como salida
  pinMode(Echo, INPUT);            //pin como entrada
  digitalWrite(Trigger, LOW);     //Inicializamos el pin con 0  
  lcd.init();                    //Encender LCD
  lcd.backlight();              //Apagar LCD
}

void loop()
{
  lcd.clear();                //Funcion para limpiar pantalla
  
  lcd.setCursor(2, 0);       // Coordenadas para centrar texto
  lcd.print("Diplomado v");
  lcd.setCursor(2, 1);
  lcd.print("Mecatronica");
  delay(2000);              //Retardo en milisegundos

  lcd.clear();             //Funcion para limpiar pantalla

  lcd.setCursor(2, 0);    // Coordenadas para centrar texto
  lcd.print("Eduardo Leal");
  lcd.setCursor(2, 1);
  lcd.print("Ing. Mecanico");
  delay(2000);            //Retardo en milisegundos

  lcd.clear();          //Funcion para limpiar pantalla

  long t;              //tiempo que demora en llegar el eco
  long d;             //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH);      //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");	
  Serial.println();
  delay(1000);       //Retardo en milisegundos

  lcd.clear(); //Funcion para limpiar pantalla
  lcd.setCursor(1, 0); // Coordenadas para centrar texto
  lcd.print("Distancia=" + String (d) + "cm");
  delay(2000);          ////Retardo en milisegundos
}


```

- **5.- En la sección de library manager buscar las siguientes librerías y agregarlas:**
- LiquidCristal IC2
- DHT sensor library for ESPx



- 6.- Seleccionar el sensor en la parte de Simulacion con el botón **+** y buscar **DHT22**, **LCDI2C**, **HC-SR04**, Agregar y conectar de la siguiente manera.



## Instrucción de operación:
- Correr el simulador
- Manipular los valores del sensor para observar los resultados de la medición arrojados en la pantalla LCD

## Resultados
Cuando haya compilado el código y corra la simulación, verás los valores y los textos en la pantalla LCD como se muestran en las siguentes imagenes cada 2s.



## Créditos
Desarrollado por: **Ing. Mecánico Eduardo Leal**

- https://github.com/leal-97
