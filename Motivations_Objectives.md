## Market Opportunity

We see a market for a low-cost, reliable alternative to current vaccine temperature monitoring solutions. Wireless competitor products currently on the market are wildly expensive, with a low temperature sampling rate and poor battery life.

The high cost can be attributed to a **thermocouple-based design**. While thermocouples are accurate, they require costly ADC circuitry—where resolution (in bits) directly affects accuracy. Additionally, thermocouples involve manual manufacturing and calibration processes, significantly increasing the final product cost.

Each of these wireless devices includes **independent cloud connectivity**. Communicating with a cell tower from inside a sealed magnetic fridge is challenging, so these devices include a transmission power amplifier, which **dramatically increases power consumption**. 

Battery life for current solutions typically ranges around **2 years**, with no warning system for low battery. When the battery dies, **replacement or recharging is not possible**—pharmacies must purchase a completely new device. Sampling rate is often limited to **1 measurement per hour** to conserve battery. Due to power-inefficient ADCs and lack of embedded low-power optimization, batteries are **bulky**, making the devices **large** and inconvenient to store in compact refrigeration environments.

## Limitations of Manual Measurement

Manual measurement systems also fail to meet expectations:
- **No temperature history tracking** without manual spreadsheet recording
- **No alert logging** for threshold violations
- **No cloud access**
- **Poor robustness**: Devices tend to fail within 1–2 years, even when batteries are replaced

## Our Solution

Competitors approach the problem incorrectly by assuming one device must handle both **temperature sampling** and **cloud forwarding**. We restructure the solution to keep costs **an order of magnitude lower** than existing products by **separating these two roles**:

- A **Temperature Sampling Device**
- An **LTE Gateway**

These two components work together to deliver a complete, low-cost, and reliable solution.

### Temperature Sampling Device

- Always remains with the vaccines—even during transportation
- Uses a **NIST-traceable digital temperature sensor**
  - Replaces thermocouples
  - Provides **low-power**, **high-accuracy** measurement
  - Comes **pre-calibrated**, within ACP specifications
- Communicates via **Bluetooth Low Energy (BLE)** to the LTE gateway
- Sends data to the **mcThings cloud service** for secure viewing in **tabular or graphical format**

### LTE Gateway

- Acts as a **proxy** to the cloud (BLE cannot directly reach cell towers)
- Receives data from the sensor device and **forwards it to the cloud**
- Located **outside** the fridge/freezer, plugged into a **wall outlet**
- If sensor is out of range (e.g., during transit), it **stores data in flash memory**
- Upon reconnection, **all stored data is transmitted**
- If connected, **temperature alerts** are sent **immediately** via **email or SMS** to healthcare authorities
