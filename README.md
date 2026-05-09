# IOT-with-AIML-Argoai_XGboost-Version-1
Testing Project 
# 🌾 AgroAI - IoT with AIML | XGBoost Version 1.0

[![ESP32](https://img.shields.io/badge/ESP32-Platform-blue)](https://www.espressif.com)
[![XGBoost](https://img.shields.io/badge/XGBoost-ML-orange)](https://xgboost.ai)
[![Python](https://img.shields.io/badge/Python-3.8+-green)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-yellow)](LICENSE)
[![Wokwi](https://img.shields.io/badge/Wokwi-Simulation-red)](https://wokwi.com)
[![ThingSpeak](https://img.shields.io/badge/ThingSpeak-IoT-purple)](https://thingspeak.com)

---

<img width="1429" height="953" alt="image" src="https://github.com/user-attachments/assets/c78ea731-8946-4169-8bac-5af6931e281c" />

## 📋 Project Overview

**AgroAI** is an intelligent irrigation system that combines IoT sensors with Machine Learning to make smart watering decisions. This project demonstrates the complete pipeline from data collection (ESP32 simulation) to ML model deployment (XGBoost) with a web interface (Gradio).

### 🎯 Key Features

| Feature | Description |
|---------|-------------|
| 📡 IoT Data Collection | ESP32 simulation with multiple sensors via Wokwi |
| ☁️ Cloud Integration | ThingSpeak API for data storage |
| 🤖 ML Model | XGBoost classifier/regressor for irrigation prediction |
| 🌐 Web Interface | Gradio dashboard for real-time predictions |
| 📊 Data Pipeline | Complete ETL + Model training workflow |
| 🔄 Real-time Updates | 15-minute interval sensor readings |

---

## 🏗️ System Architecture
┌─────────────────────────────────────────────────────────────────┐
│ DATA FLOW PIPELINE │
├─────────────┬─────────────┬─────────────┬─────────────┬─────────┤
│ Wokwi │ ESP32 │ ThingSpeak │ Python │ Gradio │
│ Simulation │ Sensors │ Cloud │ XGBoost │ Web │
│ │ │ │ │ UI │
└─────────────┴─────────────┴─────────────┴─────────────┴─────────┘
↓ ↓ ↓ ↓ ↓
Fake/Synth Real-time Storage Training Demo
Data Reading & API & Prediction App


---

## 🚀 Getting Started

### Prerequisites

```bash
# Python 3.8 or higher
python --version

# Install required packages
pip install -r requirements.txt

requirements.txt:


pandas>=2.0.0
numpy>=1.24.0
scikit-learn>=1.3.0
xgboost>=2.0.0
joblib>=1.3.0
gradio>=4.0.0
requests>=2.31.0
matplotlib>=3.7.0
seaborn>=0.12.0
thingspeak>=1.0.0
python-dotenv>=1.0.0
```

### Installation Steps
```bash

# 1. Clone repository
git clone https://github.com/bigganbiggan/IOT-with-AIML-Argoai_XGboost-Version-1.git
cd IOT-with-AIML-Argoai_XGboost-Version-1

# 2. Create virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Set up environment variables
cp .env.example .env
# Edit .env with your ThingSpeak API keys

# 5. Run synthetic data generation
python src/generate_synthetic.py --samples 600

# 6. Train the model
python src/train_model.py

# 7. Launch web interface
python app/app.py

```
🔌 Hardware Configuration (Wokwi Simulation)
```bash
Components Used
Component	Pin	Reading Range	Unit
Soil Moisture Sensor	GPIO34 (Analog)	0-4095 → 0-100%	%
DHT22 (Temp/Humidity)	GPIO15 (Digital)	-40 to 80°C / 0-100%	°C / %
pH Sensor	GPIO35 (Analog)	0-4095 → 0-14	pH
Light Sensor (LDR)	GPIO32 (Analog)	0-1000	lux
Water Pump Relay	GPIO26 (Digital)	ON/OFF	-
```

## ESP32 Arduino Code Snippet
```bash
// firmware/agroai_sensors.ino

#include <WiFi.h>
#include <ThingSpeak.h>
#include <DHT.h>

// WiFi Credentials
const char* ssid = "YOUR_SSID";
const char* password = "YOUR_PASSWORD";

// ThingSpeak Configuration
unsigned long channelID = your channel ID ;
const char* apiKey = "YOUR_API_KEY";

// Sensors
#define SOIL_PIN 34
#define PH_PIN 35
#define LIGHT_PIN 32
#define DHT_PIN 15
DHT dht(DHT_PIN, DHT22);

void setup() {
  Serial.begin(115200);
  WiFi.begin(ssid, password);
  ThingSpeak.begin(client);
  dht.begin();
}

void loop() {
  // Read sensors
  int soilRaw = analogRead(SOIL_PIN);
  float soilMoisture = map(soilRaw, 0, 4095, 0, 100);
  
  float temperature = dht.readTemperature();
  float humidity = dht.readHumidity();
  
  int phRaw = analogRead(PH_PIN);
  float phValue = map(phRaw, 0, 4095, 0, 1400) / 100.0;
  
  int lightValue = analogRead(LIGHT_PIN);
  
  // Send to ThingSpeak
  ThingSpeak.setField(1, temperature);
  ThingSpeak.setField(2, humidity);
  ThingSpeak.setField(3, soilMoisture);
  ThingSpeak.setField(4, phValue);
  ThingSpeak.setField(5, lightValue);
  ThingSpeak.writeFields(channelID, apiKey);
  
  delay(15000); // 15 second interval
}
```
## Features Used
```bash

Feature	Type	Range	Importance
Temperature	Continuous	0-50°C	0.25
Humidity	Continuous	0-100%	0.20
Soil Moisture	Continuous	0-100%	0.35
pH Value	Continuous	0-14	0.10
Light Intensity	Continuous	0-1000 lux	0.07
Battery Level	Continuous	0-100%	0.03
```

🌐 Web Interface (Gradio)
Features
📊 Real-time prediction dashboard

🎚️ Interactive sliders for sensor inputs

📈 Historical data visualization

💾 Model download option

📱 Mobile responsive design

# Acknowledgments
Resource	Purpose
Wokwi	ESP32 simulation platform
ThingSpeak	IoT cloud data storage
XGBoost	Machine learning library
Gradio	Web interface framework
Hugging Face	Model hosting & Spaces


👨‍💻 Author
G.M. Biggan

GitHub: https://github.com/Biggan2003
Project: AgroAI - Smart Farming Ecosystem
Email: gmbiggan@gmail.com
Youtube: 
https://www.youtube.com/@G.M-Biggan/videos



