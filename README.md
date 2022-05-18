# Medidor-de-temperatura
#include <LiquidCrystal_I2C.h>
LiquidCrystal_I2C lcd(0x27,16,2);
float volt_analog; //Voltaje analogico leido por el arduino
float volt_analog_v; //Valores analogicos trasnformados a voltaje
float temperatura; //Temperatura resultante 
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600); //Activacion de puerto serial 
  pinMode(A0,INPUT); //Pin analogico activado para ingresar datos
  lcd.init(); //Activacion de la pantalla
  lcd.backlight(); //Prende la luz del fondo
  lcd.clear(); //Limpia cualquier texto que pueda estar impreso 
  lcd.setCursor(1,1); //Coloca el cursor en el primer recuadro 
  lcd.print("La temperatura"); //Imprime el texto en la primera fila
}
void loop() {
  // put your main code here, to run repeatedly:
  volt_analog=analogRead(A0); //Lectura de voltaje de tatermocupla
  volt_analog_v=(volt_analog*5)/1023; //Trasnformacion a voltaje
  temperatura=volt_analog_v*20; //Trasnformacion de voltaje a temperatura
  lcd.setCursor(1,1); //Se coloca en la segunda fila de la pantalla
  lcd.print(temperatura,2); //Imprime la temperatura con dos decimales
  delay(1000); //Realiza una nueva lectura cada segundo
}
