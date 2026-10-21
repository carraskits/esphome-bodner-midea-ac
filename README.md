# esphome-bodner-midea-ac

Integration of Bodner / Midea air conditioning into Home Assistant using ESPHome and an ESP8266 / ESP-12F module.

## ESPHome Integration for Bodner / Midea Air Conditioner

This repository contains the ESPHome configuration to integrate Bodner air conditioning units into Home Assistant using an ESP8266 / ESP-12F microcontroller.

> **Note:** Bodner air conditioners utilize Midea hardware and protocols internally, making them fully compatible with the ESPHome `midea` climate platform.

---

## 📋 Home Assistant Prerequisites

To use the **Follow Me** feature properly, this setup relies on a **Combine State (Mean)** Helper created within Home Assistant:

* **Target Entity:** `sensor.temperatura_media_salon`
* **Source Temperature Entities:**
  * `sensor.termostato_grande_temperature`
  * `sensor.termostato_hogar_temperature`

*(Optional)* You can also monitor room humidity using a similar Helper (`sensor.humedad_media_salon`) aggregating:
* `sensor.termostato_grande_humidity`
* `sensor.termostato_hogar_humidity`

---

## ⚙️ How "Follow Me" Works

The ESP8266 retrieves the arithmetic mean temperature from the living room thermostats and forwards it periodically to the Bodner AC unit via the `midea_ac.follow_me` action. 

* **Debounce Filter (2s):** Delays the initial reading to prevent boot loops on startup.
* **Delta Filter (0.5°C):** Only transmits update signals when the mean temperature shifts by at least 0.5°C to reduce unnecessary serial bus chatter.

---

## 🛡️ Security Note

Make sure to replace placeholder strings like `YOUR_API_ENCRYPTION_KEY` and `YOUR_FALLBACK_AP_PASSWORD` or utilize an ESPHome `secrets.yaml` file to store sensitive Wi-Fi and API credentials safely.
