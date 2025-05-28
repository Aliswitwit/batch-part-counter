# batch-part-counter
PLC-based batch counter using CTU logic to track parts. Triggers output after 5 parts are detected, with manual reset to restart. Built in RSLogix 500 with real-world I/O mapping and latch/reset safety logic.

### 🎯 System Objective

Detect incoming parts using a digital sensor

Count up to a preset value (5 parts)

Trigger a batch output signal when the batch is full

Wait for a reset to begin the next batch

### 🛠 Tools Used

RSLogix Micro Starter Lite

RSLogix Emulate 500

RSLinx Classic

## 🧾 Ladder Logic Breakdown

### 🔁 Rung 0 – Start System

XIC B3:0/0   (Start Button)
ONS B3:0/1   (One-Shot Start)
OTE B3:0/2   (Start Trigger / System On)

### 🔁 Rung 1 – Part Detection

XIC B3:0/10  (Part Sensor)
ONS B3:0/11  (One-Shot Filter)
OTE B3:0/3   (Part Detected Pulse)

### 🔁 Rung 2 – Part Counting Logic

XIC B3:0/2   (System Trigger)
XIC B3:0/3   (Part Detected)
ONS B3:0/4   (Count One-Shot)
CTU C5:0     (Parts Counter)
Preset = 5, Acc = 0

### 🔁 Rung 3 – Batch Complete Output Trigger

XIC C5:0/DN  (Counter Done)
OTE B3:0/5   (Batch Output Trigger)

### 🔁 Rung 4 – Output Latching Logic

XIC B3:0/5   (Batch Output Trigger)
XIC B3:0/9   (Latch Hold)
XIO B3:0/8   (System Reset)
OTE B3:0/9   (Batch Output Latch)

### 🔁 Rung 5 – Reset Button

XIC B3:0/6   (Reset Button)
ONS B3:0/7   (Reset Pulse)
RES C5:0     (Reset Counter)

### 📸 Screenshots

Resting State: Before part detection, counter = 0

I/O Configuration: Clear mapping of inputs & outputs for real hardware use

### 💡 Real-World Applications

Robotic or automated part feeders

Conveyor batch systems

Bottle filling stations

High-volume inspection processes

### 🔍 Project Highlights

Edge detection via ONS to avoid bounce or overcounting

Conditional latching with reset-interrupt

Clean structure for real-world deployment
