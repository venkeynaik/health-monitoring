# venkatesh
smart parking system
#include <SoftwareSerial.h>

#define trigPin 9
#define echoPin 10
#define ledPin 13

SoftwareSerial BTserial(11, 12); // RX | TX

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(ledPin, OUTPUT);
  
  BTserial.begin(9600);
  Serial.begin(9600);
}

void loop() {
  long duration, distance;
  
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  
  duration = pulseIn(echoPin, HIGH);
  
  distance = (duration / 2) / 29.1;
  
  if (distance <= 5) { // Adjust this value based on your specific setup
    digitalWrite(ledPin, HIGH);
    BTserial.println("Parking space occupied");
  } else {
    digitalWrite(ledPin, LOW);
    BTserial.println("Parking space available");
  }
  
  delay(500);
}
