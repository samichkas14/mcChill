# Hardware Design

## Design Goals

Before diving into the hardware, we outlined the following requirements:
- **Low power consumption**: Select components with low operational and quiescent current to achieve a battery life >1 year.
- **BLE compatibility**: Essential for communicating with the LTE gateway.
- **Temperature sensing**: Must sample the temperature of a surrogate vaccine solution.
- **Mechanical integration**: Ensure the temperature sensor interfaces with liquid without compromising device integrity.
- **Cost-effectiveness**: Choose low-cost components and maximize manufacturing yield for scalability.

---

## Architecture Overview

We split the device hardware into:
- A **motherboard (MB)**
- A **daughterboard (DB)**

They interface via a 6-pin SMT pogo connector carrying I²C, alert, power, and ground. This separation keeps the enclosure compact and aligns the daughterboard with the vial for direct sensing.

---

## Key Components

### Microcontroller – nRF52840

- Fits BLE and low-power requirements
- BLE Tx/Rx: ~35 mA; sleep mode: ~1–2 µA
- Handles hardware interrupts from temperature sensors and accelerometer
- Manages I²C communications
- 8 dBm Tx power keeps current consumption low

---

### Coulomb Counter – LTC2959

- Tracks battery life using a 50 mΩ shunt resistor
- Measures voltage drop to calculate current via Ohm's Law
- Operational current: <1 µA
- Sends battery alerts (mAh, voltage, avg. current) to cloud

---

### Temperature Sensor – TMP117

- Replaces TMP119 for cost reasons
- Accuracy: 0.05°C (–20°C to 50°C)
- Identical package/pinout as TMP119
- ⅓ the price in volume while meeting ACP standards

---

### Boost Converter

- Replaces LDO to support 1.5V battery -> 3.3V logic
- Input: 0.5V–5.5V; Output: 3.3V
- Ultra-low quiescent current: 95 nA
- Low ripple (50 mV), integrated protections (short, reverse current, input limiting)

---

### Accelerometer – LIS2DUX12

- For cold chain motion detection
- Power: 2.7 µA sampling, 10 nA power-down
- Offers ambient temperature readings via internal sensor
- Used only when device is stationary for BLE scans

---

### External Flash

- Two 1MB modules for store & forward and OTA updates
- Not populated on final device (would require complex SPI drivers)
- Footprints included for future use
- Reason: sponsor had surplus 1MB chips

---

### LEDs

- Two RGB LEDs (0404 package)
- Low-cost (<$0.01/LED in volume)
- Withstand thermal cycling; used in outdoor displays

---

### Button

- SPST tactile switch
- Matches enclosure design
- GPIO controlled, used for UI purposes
