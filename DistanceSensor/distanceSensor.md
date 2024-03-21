## DistanceSensor

In this project, We will do DistanceSensor


## Diagram

<img src="/DistanceSensor/e1.png" alt="diagram">
<img src="/DistanceSensor/e2.png" alt="diagram">



## Source Code

```c++
// C++ code
#include <LiquidCrystal.h>

//HC-SR04 Pinleri
const int trigPin = 9;
const int echoPin = 10;

// LCD Pinleri
const int Rs = 12, E = 11, D4 = 5, D5 = 4,D6 = 3, D7 = 2;
LiquidCrystal lcd(Rs, E, D4, D5, D6, D7);

//Buzzer Pin
const int buzzerPin = 8;
  
void setup()
{
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(buzzerPin, OUTPUT);
  
  // LCD Başlatma
  lcd.begin(16,2);
}

void loop()
{
  //Mesafe Ölçme
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW); 
  long duration = pulseIn(echoPin, HIGH);
  float distance = duration * 0.034 / 2 ; 
  
  // LCD Ekran Güncellemesi
  lcd.clear();
  lcd.print("Mesafe:");
  lcd.print(distance);
  lcd.print("cm");
  
  // Buzzer Kontrolü
  if (distance < 10){
  	//obje çok yakın
    tone(buzzerPin, 1000); // Yüksek Frekansta ses 
  }
  
  else if (distance < 70) {
    tone(buzzerPin, 500); // Düşük Frekansta ses 

  }
  
  else {
  	noTone(buzzerPin); // kapat
  }
  delay(100);

}
```
