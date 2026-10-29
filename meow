
#include <Servo.h>

const int trigPin = 9;
const int echoPin = 10;
const int servoPin = 6;

Servo arm;

const int detectionDistance = 20; // centimeters

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);

  arm.attach(servoPin);
  arm.write(100); // Lid closed

  Serial.begin(9600);
}

void loop() {
  // Trigger ultrasonic sensor
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // Measure distance
  long duration = pulseIn(echoPin, HIGH, 30000);

  if (duration > 0) {
    float distance = duration * 0.0343 / 2;

    Serial.print("Distance: ");
    Serial.print(distance);
    Serial.println(" cm");

    if (distance <= detectionDistance) {
      arm.write(0);    // Lid open
    } else {
      arm.write(100);  // Lid closed
    }
  } else {
    Serial.println("No echo detected");
    arm.write(100);    // Close if no echo is received
  }

  delay(100);
}
