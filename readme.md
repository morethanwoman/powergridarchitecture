# Hybrid Renewable Power Plant Architecture (Solar PV + OPV + BESS)

An interactive, web-based industrial network architecture diagram built in accordance with the **Purdue Model for Industrial Control Systems (ICS)** and **IEC 62443** defense-in-depth cybersecurity standards.

![Architecture Diagram](https://img.shields.io/badge/Purdue_Model-Level_0_to_4-blue)
![Standards](https://img.shields.io/badge/Security-IEC_62443_SL--2-emerald)
![Deployment](https://img.shields.io/badge/Deployment-GitHub_Pages-brightgreen)

---

## ⚡ Power Plant & Infrastructure Scope

This architecture models a utility-scale hybrid power plant combining:
* **Solar PV:** Utility-scale silicon bifacial solar strings and central/string inverters.
* **Organic Photovoltaics (OPV):** Flexible, thin-film organic PV modules with dedicated wide-range MPPT string inverters.
* **Battery Energy Storage System (BESS):** 1500V DC LFP battery containers, Master BMS, and 4-quadrant Power Conversion System (PCS) bi-directional inverters.
* **High-Voltage Substation:** Step-Up Transformer (33 kV / 110–400 kV), HV Switchgear, Protection Relays & IEDs, and POI Revenue Metering.

---

## 🏗️ Purdue Model Classification Hierarchy

```
+-----------------------------------------------------------------------------------+
|                        LEVEL 4: ENTERPRISE & GRID INTERFACE                       |
|   * TSO / DSO Control Center (IEC 60870-5-104 / DNP3)                              |
|   * Aggregator EMS / Market Interface (REST API / MQTT over HTTPS)                |
|   * Enterprise IT Headquarters (Encrypted WAN / IPsec)                            |
+-----------------------------------------------------------------------------------+
                                         |
     [Level 3.5 Industrial DMZ: WALLIX PAM / MFA / Jump Hosts / Reverse Proxy]
                                         |
+-----------------------------------------------------------------------------------+
|               LEVEL 3: OPERATIONAL CONTROL & SHARED MANAGEMENT SERVICES           |
|   * Redundant SCADA Masters (Active/Standby)                                      |
|   * Bazefield RES Performance Analytics Platform                                  |
|   * Enterprise Plant Historian (OSIsoft PI)                                       |
|   * Log Collector Server / SIEM (Syslog-ng / Audit Collector)                     |
|   * GNSS Hardware NTP/PTP Master Clock                                            |
|   * WSUS / Firmware Update Server                                                 |
|   * Antivirus / EDR Console                                                       |
+-----------------------------------------------------------------------------------+
                                         |
         [Plant Network Backbone: Modbus TCP / IEC 61850 MMS / OPC UA / PRP]
                                         |
+-----------------------------------------------------------------------------------+
|               LEVEL 2: PLANT CONTROLLER & SUBSTATION AUTOMATION                   |
|   * Redundant Power Plant Controller (PPC Master A & B, <100ms failover)           |
|   * Substation Automation System (SAS) & RTU Gateway                              |
|   * Protection Relays & Intelligent Electronic Devices (IEC 61850 GOOSE/MMS)      |
|   * Point of Interconnection (POI) Class 0.2S Revenue Power Meter                 |
+-----------------------------------------------------------------------------------+
                                         |
       [Collector Bus: Modbus TCP / SunSpec / CANopen / RS485 Serial Loops]
                                         |
+-----------------------------------------------------------------------------------+
|                  LEVEL 1: LOCAL AUTOMATION & UNIT CONTROLLERS                     |
|   * Solar PV Central / String Inverters                                           |
|   * Organic PV (OPV) MPPT String Inverters                                        |
|   * PVH Single-Axis Tracker Controllers (MBox & TBox Units)                       |
|   * BESS Power Conversion System (PCS Inverters)                                  |
|   * BESS Container Master BMS                                                     |
+-----------------------------------------------------------------------------------+
                                         |
                  [Direct Power / Hardwired Signal / Sensor Loops]
                                         |
+-----------------------------------------------------------------------------------+
|           LEVEL 0: PHYSICAL PROCESS EQUIPMENT, HIGH VOLTAGE & ACTUATORS           |
|   * HV Main Step-Up Power Transformer (e.g., 33kV / 110-400kV)                    |
|   * HV Switchgear, SF6 Circuit Breakers & Earth Disconnectors                     |
|   * Solar PV & Flexible OPV Module Strings                                        |
|   * PVH Tracker Actuators, Motors (DBox) & Inclinometers                          |
|   * BESS Battery Racks, Cells & Tray BMS                                          |
|   * Weather Sensors & Pyranometers                                                |
+-----------------------------------------------------------------------------------+
```

---

## 🚀 Deployment to GitHub Pages

1. **Fork or Push to GitHub:**
   Push these files directly to your GitHub repository:
   ```bash
   git init
   git add .
   git commit -m "Initial commit of Hybrid Power Plant Architecture"
   git branch -M main
   git remote add origin https://github.com/<YOUR-USERNAME>/<YOUR-REPO-NAME>.git
   git push -u origin main
   ```

2. **Enable GitHub Pages:**
   * Go to **Settings > Pages** in your GitHub repository.
   * Under **Build and deployment**, select **GitHub Actions** as the source (or set **Source** to `Deploy from a branch` and choose `main` / root).
   * Save settings. Your site will automatically build and publish!

---

## 🛡️ Cyber Security Compliance (IEC 62443)

* **Perimeter DMZ Zone (L3.5):** All external access routes must pass through Privileged Access Management (PAM) with Multi-Factor Authentication (MFA) and continuous session recording.
* **Network Segmentation:** Physical and VLAN isolation between control buses (Level 2/1) and management networks (Level 3).
* **Zero Trust Logging:** All event logs, SCADA alarms, firewall traps, and PAM sessions stream centrally to the **Log Collector Server (SIEM)** over encrypted Syslog/TLS links.