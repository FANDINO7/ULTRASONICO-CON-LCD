**ULTRASONICOCONLCD**



**Descripción**
En este repo se muestra como podemos programar la pantalla LCD con lo anteriormente programado con el ESP32, un Ultrasonic Distance Sensor y una pantalla LCD, se actualiza cada 2 segundos, y se tienen que agregar la librería de la pantalla de liquid crystal y también en el código se tiene que iniciar la pantalla, se sige utilizando la herramienta de simulacion woki para efectos practicos 



**Material Necesario**
-wokwi
-ESP32
-Ultrasonic Distance Sensor
-lcd1602

**Codigo en para la programacion**
```
const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
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
  Serial.print("cm");
  Serial.println();
  delay(2000);          //Hacemos una pausa de 100ms
  
  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("DIPLOMADO V");
  lcd.setCursor(2, 1);
  lcd.print("Mecatronica");
  delay(2000);

  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("ALBERTO FANDIÑO ");
  lcd.setCursor(2, 1);
  lcd.print("Ing Electrico");
  delay(2000);

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Distancia:"+ String(d)+ "cm");
  delay(2000); 
}
```

**resultados**
!![](https://github.com/FANDINO7/ULTRASONICO-CON-LCD/blob/main/lcd%20con%20ultrasonico.png?raw=true)


**realizado por **

Alberto Fandiño
