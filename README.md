# smart-garden-system
Smart Garden System is an Arduino-based project that monitors soil moisture and temperature using sensors. A 16×2 LCD displays the readings, and LED indicators show when the soil is dry or wet. The project is simulated using Tinkercad Circuits.

Smart Garden System 🌱

# 1. Project Title and Introduction

Project Title: Smart Garden System Using Arduino

Name: D. Madhoolika

Branch: Electronics and Communication Engineering (ECE)

College: RGUKT Ongole

Project Goal

The Smart Garden System monitors soil moisture using a soil moisture sensor and displays the information on a 16×2 LCD. It helps identify when plants need watering and demonstrates how sensors and a microcontroller can be used for basic plant monitoring.

# 2. Hardware and Components

Main Components Used

- Arduino Uno
- Soil Moisture Sensor
- 16×2 LCD Display
- Potentiometer (for LCD contrast)
- Connecting Wires

System Diagram / Wiring

The soil moisture sensor is connected to the Arduino to read soil moisture levels. The 16×2 LCD displays the sensor readings and system status.

Circuit Diagram: Add your Tinkercad circuit screenshot here.

# 3. Core Implementation

3.1 Key Concepts Applied

- Analog-to-Digital Conversion (ADC)
- Sensor Interfacing
- Digital Input/Output
- LCD Interfacing
- Conditional Logic
- Arduino Programming in C++

3.2 Program Logic Flow

1. Initialize the Arduino pins and LCD display.
2. Read the soil moisture sensor value.
3. Process the sensor reading to determine the soil moisture condition.
4. Display the moisture reading and status on the LCD.
5. Repeat the process continuously.

3.3 Code

#include <LiquidCrystal.h>

// LCD: RS, E, D4, D5, D6, D7
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

const int soilPin = A0;
const int tempPin = A1;
const int pumpLED = 7;
const int stopLED = 8;
const int dryThreshold = 600;

void setup() {
  pinMode(pumpLED, OUTPUT);
  pinMode(stopLED, OUTPUT);
  lcd.begin(16, 2);
  Serial.begin(9600);
  lcd.setCursor(0, 0);
  lcd.print("Smart Garden");
  lcd.setCursor(0, 1);
  lcd.print("Starting...");
  delay(1500);
  lcd.clear();
}

void loop() {
  int soilValue = analogRead(soilPin);
  int tempReading = analogRead(tempPin);
  float voltage = tempReading * (5.0 / 1023.0);
  float temperature = (voltage - 0.5) * 100.0;
  bool soilDry = (soilValue > dryThreshold);

  if (soilDry) {
    digitalWrite(pumpLED, HIGH);
    digitalWrite(stopLED, LOW);
  } else {
    digitalWrite(pumpLED, LOW);
    digitalWrite(stopLED, HIGH);
  }

  lcd.setCursor(0, 0);
  lcd.print("Soil:");
  lcd.print(soilDry ? "DRY " : "WET ");
  lcd.print("V:");
  lcd.print(soilValue);
  lcd.print("   ");
  lcd.setCursor(0, 1);
  lcd.print("T:");
  lcd.print(temperature, 1);
  lcd.print("C P:");
  lcd.print(soilDry ? "ON " : "OFF");
  
  Serial.print("Soil value: ");
  Serial.print(soilValue);
  Serial.print(" | Temperature: ");
  Serial.print(temperature, 1);
  Serial.print(" C | Pump: ");
  Serial.println(soilDry ? "ON" : "OFF");
  delay(1000);
}

# 4. Results and Demonstration

Testing Method

The system was tested using Tinkercad Circuits by changing the soil moisture sensor conditions and observing the corresponding LCD output.

Evidence

- Add a screenshot of the complete circuit.
- Add a screenshot of the LCD displaying the sensor readings.

Functionality Statement

The Smart Garden System demonstrates soil moisture monitoring using an Arduino and a 16×2 LCD. The simulation helps understand sensor interfacing and real-time display of sensor data.

#5. Conclusion and Learning

What I Learned

Through this project, I learned how to interface a soil moisture sensor with an Arduino and display sensor readings on an LCD. I also gained practical experience with analog input, conditional logic, and circuit simulation using Tinkercad.

Challenges

One challenge was configuring the LCD connections and ensuring that the display worked correctly. I addressed this by checking the wiring, LCD contrast connection, and Arduino code.

Future Improvements

- Add automatic plant watering using a relay and water pump.
- Integrate temperature and humidity sensors.
- Add Wi-Fi-based monitoring using an ESP32.
- Display clearer soil condition messages such as "DRY" and "WET".

---

Project Type: Embedded Systems
Platform: Tinkercad Circuits
Controller: Arduino Uno
Display: 16×2 LCD
