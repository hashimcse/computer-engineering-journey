# computer-engineering-journey
learning computer programming and also trying to gain a little knowledge of git & github 
<br>
let me upload a simple arduino code to control electrical appliances from your phone.
<br>
#include <SoftwareSerial.h>

// Pins for Bluetooth module
const int rxPin = 10;
const int txPin = 11;

SoftwareSerial bluetooth(rxPin, txPin); // RX, TX

// Relay control pins
const int relay1 = 7;
const int relay2 = 8;

void setup() {
  pinMode(relay1, OUTPUT);
  pinMode(relay2, OUTPUT);

  // Start with both relays OFF (HIGH for active LOW relays)
  digitalWrite(relay1, HIGH);
  digitalWrite(relay2, HIGH);

  bluetooth.begin(9600);
  Serial.begin(9600);
  Serial.println("Bluetooth Light Control Started");
}

void loop() {
  if (bluetooth.available()) {
    char command = bluetooth.read();
    Serial.print("Received: ");
    Serial.println(command);

    // Control Light 1
    if (command == 'A') {
      digitalWrite(relay1, LOW);  // Turn ON Light 1
      Serial.println("Light 1 ON");
    }
    else if (command == 'a') {
      digitalWrite(relay1, HIGH); // Turn OFF Light 1
      Serial.println("Light 1 OFF");
    }
    // Control Light 2
    else if (command == 'B') {
      digitalWrite(relay2, LOW);  // Turn ON Light 2
      Serial.println("Light 2 ON");
    }
    else if (command == 'b') {
      digitalWrite(relay2, HIGH); // Turn OFF Light 2
      Serial.println("Light 2 OFF");
    }
    else {
      Serial.println("Invalid command");
    }
  }
}

