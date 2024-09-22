#include <DHT.h>

#define DHTPIN D1
#define DHTTYPE DHT11

DHT dht(DHTPIN, DHTTYPE);
int relayPin = D2;

void setup() {
  Serial.begin(9600); // Initialize serial communication
  dht.begin();
  pinMode(relayPin, OUTPUT);
}

void loop() {
  float temperature = dht.readTemperature();

  if (isnan(temperature)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }

  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.println(" °C");

  if (temperature < 38) {
    digitalWrite(relayPin, LOW);
  } else {
    digitalWrite(relayPin, HIGH);
  }

  delay(1000);
}
