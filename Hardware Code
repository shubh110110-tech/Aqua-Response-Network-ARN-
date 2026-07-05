#include <DHT.h>

#define DHTPIN 3
#define DHTTYPE DHT11

DHT dht(DHTPIN, DHTTYPE);

const int flamePin = 2;
const int smokePin = A0;
const int soilPin = A1;
const int waterPin = A2;

const int relayPin = 7;
const int buzzerPin = 8;
const int redLED = 9;
const int greenLED = 10;

void setup()
{
  Serial.begin(9600);

  pinMode(flamePin, INPUT);

  pinMode(relayPin, OUTPUT);
  pinMode(buzzerPin, OUTPUT);

  pinMode(redLED, OUTPUT);
  pinMode(greenLED, OUTPUT);

  digitalWrite(relayPin, LOW);
  digitalWrite(buzzerPin, LOW);

  dht.begin();

  Serial.println("Aqua Response Network Started");
}

void loop()
{
  int flame = digitalRead(flamePin);
  int smoke = analogRead(smokePin);
  int soil = analogRead(soilPin);
  int water = analogRead(waterPin);

  float temp = dht.readTemperature();
  float humidity = dht.readHumidity();

  Serial.println("---------------------------");
  Serial.print("Temperature: ");
  Serial.print(temp);
  Serial.println(" C");

  Serial.print("Humidity: ");
  Serial.print(humidity);
  Serial.println(" %");

  Serial.print("Smoke Level: ");
  Serial.println(smoke);

  Serial.print("Soil Moisture: ");
  Serial.println(soil);

  Serial.print("Water Level: ");
  Serial.println(water);

  // FIRE DETECTION
  if(flame == LOW || smoke > 400)
  {
      Serial.println("FIRE DETECTED!");

      digitalWrite(redLED,HIGH);
      digitalWrite(greenLED,LOW);

      digitalWrite(buzzerPin,HIGH);
      digitalWrite(relayPin,HIGH);

      delay(5000);

      digitalWrite(relayPin,LOW);
      digitalWrite(buzzerPin,LOW);
  }

  else
  {
      digitalWrite(redLED,LOW);
      digitalWrite(greenLED,HIGH);
  }

  // DROUGHT / IRRIGATION
  if(soil > 700 && water > 300)
  {
      Serial.println("Dry Soil - Irrigation Started");

      digitalWrite(relayPin,HIGH);

      delay(3000);

      digitalWrite(relayPin,LOW);
  }

  if(water < 150)
  {
      Serial.println("Warning: Water Level Low");
  }

  delay(2000);
}
