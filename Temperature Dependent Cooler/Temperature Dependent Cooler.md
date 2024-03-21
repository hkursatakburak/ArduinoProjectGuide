# Temperature Dependent Cooler

In this project, We will do Temperature Dependent Cooler

### What we need 

* Led
* Arduino Uno
* Resistance
* Cables
* TMP36
* DC Motor
 
## Diagram

<img src="/Temperature Dependent Cooler/t2.png" alt="diagram">
<img src="/Temperature Dependent Cooler/t1.png" alt="diagram">


## Sorce Code

```c++
// C++ code
const int temPin = A0;
const int motorPin = 11;
const int ledPin = 8;
void setup()
{
  pinMode(ledPin, OUTPUT);
  pinMode(motorPin, OUTPUT);
  Serial.begin(9600);
  
}

void loop()
{
  int tempReading = analogRead(temPin);
  float voltage = tempReading * 5.0 / 1023;
  float temprature = voltage *100;    // lm35 sıcaklık hesaplama
  
  if (temprature > 30){
  	digitalWrite(ledPin, HIGH);
    int motorSpeed = map(temprature, 30, 50, 0, 255); // sıcaklığı temp voltajına göre ayarladık
    analogWrite(motorPin, motorSpeed); // motoru pwm ile sür
    Serial.println(temprature);
  }
  else{
  	digitalWrite(ledPin, LOW);
    analogWrite(motorPin, 0);
    Serial.println(temprature);

  }
  delay(1000); //1sn lik gecikme
}
```