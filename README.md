# PR-CTICA-4

Introduccion
Descripción La ESP32 la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor ultrasonico (HC-SR04) para adquirir la distancia del entorno, asi como tambien un display (LCD16x2(I2C)) donde podremos visualizar los medidas en cm y mi nombre con la carrera que cursé; cabe aclarar que esta practica se usara un simulador llamado WOKWI.

-.Para realizar esta practica necesitas lo siguiente: ° WOKWI °Tarjeta ESP32 °Sensor HC-SR04 °Display LCD16x2(I2C)

.Requisitos previos Para poder usar este repositorio necesitas entrar a la plataforma WOKWI.

Instrucciones de preparación de entorno

1.Abrir la terminal de programación y colocar la siguente programación:
#include "DHTesp.h" #include <LiquidCrystal_I2C.h> #define I2C_ADDR 0x27 #define LCD_COLUMNS 20 #define LCD_LINES 4

const int Trigger = 4; //Pin digital 2 para el Trigger del sensor const int Echo = 15; //Pin digital 3 para el Echo del sensor LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES); void setup() { Serial.begin(9600);//iniciailzamos la comunicación pinMode(Trigger, OUTPUT); //pin como salida pinMode(Echo, INPUT); //pin como entrada digitalWrite(Trigger, LOW);//Inicializamos el pin con 0 lcd.init(); lcd.backlight(); }

void loop() {

long t; //timepo que demora en llegar el eco long d; //distancia en centimetros

digitalWrite(Trigger, HIGH); delayMicroseconds(10); //Enviamos un pulso de 10us digitalWrite(Trigger, LOW);

t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso d = t/59; //escalamos el tiempo a una distancia en cm

Serial.print("Distancia: "); Serial.print(d); //Enviamos serialmente el valor de la distancia Serial.print("cm"); Serial.println(); delay(1000); //Hacemos una pausa de 100ms

lcd.clear(); lcd.setCursor(0, 0); lcd.print("Distancia: " + String(d) +"cm "); delay(1000); lcd.clear(); lcd.setCursor(0, 0); lcd.print("Ing. Mecanico"); lcd.setCursor(0, 1); lcd.print("ROBERTO PATINO"); delay(2000);

} 

-2. Instalar la libreria de DHT sensor library for ESPx como se muestra en la siguente imagen.

![Captura de pantalla 2024-01-19 155144](https://github.com/robertopatino42/PR-CTICA-4/assets/153964688/ae91c55c-f26a-4497-8be9-579e08e78464)


-3. Instalar la libreria de LiquidCrystal I2C como se muestra en la siguente imagen.

![Captura de pantalla 2024-01-19 155144](https://github.com/robertopatino42/PR-CTICA-4/assets/153964688/dbf7f014-b67d-4057-a0ff-c450f8e0993a)


-4. Hacer la conexion de HC-SR04 con la ESP32 como se muestra en la siguente imagen.

![Captura de pantalla 2024-01-19 162350](https://github.com/robertopatino42/PR-CTICA-4/assets/153964688/a924195c-6971-44c6-b802-79a2bbaee73c)


-5.Hacer la conexion de LCD16x2(I2C) con la ESP32 como se muestra en la siguente imagen. 

-6. Instrucciónes de operación Iniciar simulador. Visualizar los datos en el monitor serial. Colocar la distancia dando doble click al sensor HC-SR04

Resultados
Cuando haya funcionado, verás los valores dentro del monitor serial y el display como se muestra en la siguente imagen. 

![Captura de pantalla 2024-01-19 162350](https://github.com/robertopatino42/PR-CTICA-4/assets/153964688/8f1b3549-a537-4e17-8da2-3a72203a6b5a)
