# LAB-3---10125

// c++

//

const int trigPin = 9;
const int echoPin = 10;

long duration;
int distance;
bool objectPresent = false;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  Serial.begin(9600);
}

void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  if (distance > 0 && distance < 20) {
    if (!objectPresent) {
      Serial.println("Object Detected & Present");
      objectPresent = true;
    }
  } else {
    if (objectPresent) {
      Serial.println("Detected Object Is Gone");
      objectPresent = false;
    } else {
      Serial.println("Waiting To Detect An Object");
    }
  }

  delay(300);
}
