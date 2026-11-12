<div align="center">

<img src="assets/logo.png" alt="PRITHVI-AI Logo" width="160" height="160" />

# PRITHVI-AI (पृथ्वी-AI / পৃথিবী-AI)

### Open-LLM Powered Multilingual Environmental Intelligence, Meteorological Nowcasting & Multi-Hazard Climate Resilience Platform for India

[![Architecture](https://img.shields.io/badge/System-Multi--Tier%20Prototype-0284c7.svg?style=for-the-badge)](#system-architecture)
[![Web UI](https://img.shields.io/badge/Web%20UI-Next.js%2014%20%7C%20Tailwind-0ea5e9.svg?style=for-the-badge)](#1-web-ui-prototype-specification)
[![Mobile App](https://img.shields.io/badge/Mobile%20App-React%20Native%20%7C%20Expo-6366f1.svg?style=for-the-badge)](#2-mobile-application-prototype-specification)
[![Edge IoT](https://img.shields.io/badge/Edge%20Hardware-ESP32%20I2S%20Weather%20Box-10b981.svg?style=for-the-badge)](#3-esp32-iot-weather-box-hardware-edge-device)
[![Nowcast Research](https://img.shields.io/badge/Research-Kalman%20%7C%20VERA--MoE%20Nowcast-f59e0b.svg?style=for-the-badge)](#4-prithvi-ai-meteorological-nowcast-research)

<p align="center">
  <b>A unified, zero-hallucination climate decision ecosystem engineered for the micro-climates, monsoon patterns, and vulnerable agrarian ecosystems of the Indian subcontinent.</b>
</p>

<img src="assets/sih_reference.png" alt="PRITHVI-AI Platform Showcase" width="100%" />

</div>

---

## Executive Summary & Mission

**PRITHVI-AI** is a comprehensive meteorological nowcasting, agro-climatic intelligence, and multi-hazard early warning prototype. Designed from the ground up for the Indian subcontinent, the platform synthesizes geostationary satellite telemetry, atmospheric numerical models, hydrological river gauges, seismological feeds, and real-time ground sensors into actionable, vernacular guidance.

The core platform answers four fundamental questions across three distinct client surfaces without hallucination:
1. **What is happening?** — Real-time atmospheric state, precipitation rates, soil moisture profiles, CPCB air quality indices, and active disaster alerts.
2. **Why is it happening?** — Climatological baseline anomalies, synoptic convective patterns, and thermodynamic diagnostic stories.
3. **What is likely next?** — 0–6 hour sub-kilometer Kalman nowcasts, 7-day dual-model atmospheric projections, and 15–60 minute convective lightning threat windows.
4. **What should we do now?** — Deterministic agro-advisory rule engines (crop-specific irrigation schedules, field trafficability, pump-set operations, and disaster safety protocols).

The platform presents these insights across three synchronized client paradigms:
- **Web UI**: A high-density diagnostic dashboard built with Next.js 14, Tailwind CSS, Leaflet GIS, and interactive Recharts data canvases.
- **Mobile App**: An offline-resilient, low-bandwidth React Native / Expo application with a 2000ms fallback cache and sandboxed vector map engine.
- **ESP32 Weather Box**: A low-cost ambient IoT hardware device delivering push-to-talk voice turns and live display updates in rural villages without smartphone dependency.

---

## System Architecture

```mermaid
flowchart TD
    subgraph DataIngestion["1. Environmental Telemetry & Satellite Ingestion Layer"]
        INSAT["ISRO INSAT-3D / 3DS<br/>(Asia-Sector IR1 & VIS)"]
        IMD["IMD CAP RSS &<br/>Cyclone Bulletins"]
        OM["Open-Meteo High-Res<br/>(Weather & Soil)"]
        GloFAS["Copernicus GloFAS<br/>(River Discharge)"]
        CPCB["CPCB / Data.gov.in<br/>(Ambient Air Quality)"]
        USGS["USGS FDSN & INCOIS<br/>(Seismic & Tsunami)"]
        WBIT["Weatherbit Lightning<br/>(Observed VHF Flashes)"]
    end

    subgraph CoreEngine["2. PRITHVI-AI Computational & Research Core"]
        KalmanFilter["Between-Scene Kalman<br/>Rain-Rate Smoother"]
        VERABlend["VERA-MoE Hybrid<br/>Ensemble Blender"]
        AdlerNegri["Adler-Negri IR<br/>Convective Cell Tracker"]
        AgroRules["Deterministic Agronomic<br/>Prescription Engine"]
        IndicLLM["Open-LLM Advisory Core<br/>(Ollama Qwen2.5 Multilingual)"]
    end

    subgraph ClientSurfaces["3. Synchronized Client Surfaces"]
        WebUI["Web UI Dashboard<br/>(Next.js 14 / Tailwind / Leaflet)"]
        MobileApp["Mobile Application<br/>(React Native / Expo SDK 57)"]
        ESP32Box["ESP32 IoT Weather Box<br/>(NodeMCU-32 / I2S / OLED)"]
    end

    INSAT --> AdlerNegri
    OM --> KalmanFilter
    OM --> VERABlend
    GloFAS --> AgroRules
    CPCB --> AgroRules
    USGS --> WebUI & MobileApp
    WBIT --> AdlerNegri

    AdlerNegri --> KalmanFilter
    KalmanFilter --> VERABlend
    VERABlend --> IndicLLM
    AgroRules --> IndicLLM

    CoreEngine -->|"REST / JSON APIs"| WebUI
    CoreEngine -->|"Offline-Resilient HTTP"| MobileApp
    CoreEngine -->|"Compact JSON & Audio I2S"| ESP32Box
```

---

## 1. Web UI Prototype Specification

The **PRITHVI-AI Web UI** is an analytical command center engineered for agronomists, regional disaster management authorities, and field researchers. Built using **Next.js 14 App Router**, **Tailwind CSS**, and **Zustand**, it presents eight specialized diagnostic lenses.

<div align="center">
  <img src="assets/prithvi_3d_bot.png" alt="PRITHVI-AI 3D Assistant" width="220" />
  <p><i>PRITHVI-AI Multilingual Diagnostic Assistant Mascot</i></p>
</div>

### Architectural Lenses & Functional Tabs

1. **Overview Dashboard**:
   - Executive decision chips summarizing immediate operational posture (e.g., *Irrigation Hold*, *High Wind Gust Alert*, *Field Safe*).
   - Real-time sky state, hourly precipitation barometers, 0–6 hour locked nowcast trajectory, and 7-day glanceable weather cards.
   - 16-point interactive wind rose diagram computing micro-climate vector shears.
2. **Nowcasting Studio**:
   - 1 Hz interactive simulation playhead stepping through 15-minute Kalman-interpolated rain-rate surfaces.
   - Physiography-gated estuarine tidal modeling (e.g., Haldia port Hugli tidal curve vs. storm runoff ponding).
   - Dynamic catchment water retention gauge calculating localized waterlogging depth ($mm$).
3. **Multi-Hazard Alert Center**:
   - Real-time Common Alerting Protocol (CAP) RSS ingestion categorized into severe weather, thunderstorm, cyclone, and heatwave vectors.
   - National CPCB air quality index monitoring ($PM_{2.5}$, $PM_{10}$, $NO_2$, $SO_2$, $CO$) with health advisories.
   - Global seismic monitors (USGS FDSN) and Indian Ocean tsunami watch bulletins (INCOIS ITEWS).
4. **All-India Convective Storm Map**:
   - High-performance Leaflet / MapLibre canvas rendering georeferenced INSAT-3D/3DS Asia-sector thermal infrared clouds.
   - Live lightning strike overlay displaying observed VHF discharges within a 75 km radius.
   - 15-to-60 minute convective strike threat polygons categorized by flash intensity and cloud-top brightness depression.
5. **Predictive Models & Verification**:
   - Comparative evaluation between raw Open-Meteo forecasts and PRITHVI-AI's VERA-MoE hybrid ensemble.
   - 24-hour hourly verification plots tracking Mean Absolute Error (MAE) and agreement index against historical baselines.
6. **Agro-Ecological & Mandi Intelligence**:
   - Real-time mandi commodity prices from Agmarknet (data.gov.in) mapped across regional agricultural markets.
   - Daily FAO-56 Penman-Monteith reference evapotranspiration ($ET_0$) curves and root-zone soil saturation percentages.
7. **Multilingual Open-LLM Advisor**:
   - Trilingual voice/text chat interface supporting English, Hindi (हिंदी), and Bengali (বাংলা).
   - Strict zero-hallucination orchestration: queries are mapped to deterministic `data()` toolpacks; unbounded numerical generation is strictly prohibited.

### Web UI Sample Prototype Code

```typescript
// frontend/src/components/NowcastPlayhead.tsx
import React, { useState, useEffect } from 'react';

interface NowcastKnot {
  timestamp: string;
  rainRateMmHr: number;
  confidenceScore: number;
  source: 'kalman-interpolated' | 'insat-ir-proxy' | 'observed';
}

export const NowcastPlayhead: React.FC<{ knots: NowcastKnot[] }> = ({ knots }) => {
  const [activeStep, setActiveStep] = useState<number>(0);
  const [isPlaying, setIsPlaying] = useState<boolean>(false);

  useEffect(() => {
    if (!isPlaying) return;
    const interval = setInterval(() => {
      setActiveStep((prev) => (prev + 1) % knots.length);
    }, 1000); // 1 Hz playhead step
    return () => clearInterval(interval);
  }, [isPlaying, knots.length]);

  const current = knots[activeStep] || { rainRateMmHr: 0, confidenceScore: 0, source: 'observed' };

  return (
    <div className="p-4 bg-slate-900 border border-slate-800 rounded-xl text-white shadow-xl">
      <div className="flex items-center justify-between mb-3">
        <h4 className="text-sm font-semibold tracking-wide uppercase text-cyan-400">
          0–6h High-Resolution Nowcast Playhead (1 Hz)
        </h4>
        <span className="px-2.5 py-1 text-xs font-mono bg-cyan-950 text-cyan-300 rounded border border-cyan-800">
          T+{activeStep * 15} min [{current.source}]
        </span>
      </div>

      <div className="grid grid-cols-2 gap-4 my-3">
        <div className="p-3 bg-slate-800/80 rounded-lg">
          <p className="text-xs text-slate-400">Smoothed Rain-Rate</p>
          <p className="text-2xl font-bold font-mono text-cyan-200">
            {current.rainRateMmHr.toFixed(2)} <span className="text-sm font-normal">mm/h</span>
          </p>
        </div>
        <div className="p-3 bg-slate-800/80 rounded-lg">
          <p className="text-xs text-slate-400">Kalman State Confidence</p>
          <p className="text-2xl font-bold font-mono text-emerald-400">
            {(current.confidenceScore * 100).toFixed(0)}%
          </p>
        </div>
      </div>

      <div className="flex items-center gap-3 mt-4">
        <button
          onClick={() => setIsPlaying(!isPlaying)}
          className="px-4 py-1.5 text-xs font-semibold bg-cyan-600 hover:bg-cyan-500 rounded transition"
        >
          {isPlaying ? 'PAUSE PLAYHEAD' : 'PLAY 1 Hz SIM'}
        </button>
        <input
          type="range"
          min="0"
          max={knots.length - 1}
          value={activeStep}
          onChange={(e) => setActiveStep(Number(e.target.value))}
          className="w-full h-1.5 bg-slate-700 rounded-lg accent-cyan-400 cursor-pointer"
        />
      </div>
    </div>
  );
};
```

---

## 2. Mobile Application Prototype Specification

The **PRITHVI-AI Mobile App** is a cross-platform Android and iOS application architected with **React Native** and **Expo SDK 57**. Built specifically for rural deployment with intermittent cellular connectivity, it features a fault-tolerant offline synchronization engine.

<div align="center">
  <img src="assets/mobile_splash.png" alt="PRITHVI-AI Mobile Splash Screen" width="240" />
  <p><i>PRITHVI-AI Native Mobile App Splash & Branding</i></p>
</div>

### Mobile Architectural Highlights

- **Three-Tier Offline Resilient Cache**:
  - Implements **TanStack Query (v5)** backed by persistent `AsyncStorage`.
  - Every network call is gated by a 2000ms latency budget. If the cellular handshake drops or timeouts, the client instantly serves the last validated snapshot with an amber freshness badge without blocking UI transitions.
- **Sandboxed Leaflet.js Vector Map Engine**:
  - Eliminates proprietary Google Maps API keys and platform-dependent native crash loops by embedding a sandboxed HTML5/Leaflet vector canvas inside a React Native `WebView`.
  - Smoothly renders RainViewer Doppler radar tiles, ISRO Bhuvan geomorphological boundaries, and district AWS nodes.
- **Multilingual Vernacular Interaction**:
  - Full native localization across English, Hindi (`हिंदी`), and Bengali (`বাংলা`).
  - Integrated speech-to-text input with native audio playback of AI Advisor hazard warnings.
- **Low-Bandwidth Binary Payloads**:
  - Compact JSON payloads and lightweight telemetry snapshots (< 15 KB per full district refresh) to minimize data consumption for agrarian users.

### Mobile Offline Cache Sequence

```mermaid
sequenceDiagram
    autonumber
    actor Farmer as Agronomist / Field User
    participant App as React Native UI
    participant Query as TanStack Query Cache
    participant Storage as AsyncStorage Local DB
    participant API as PRITHVI Cloud Gateway

    Farmer->>App: Launch App / Request Current Forecast
    App->>Query: Query Snapshot (key: ['district-nowcast', id])
    Query->>API: HTTP GET /api/nowcast/live (Timeout: 2000ms)
    alt Network 200 OK (< 2000ms)
        API-->>Query: Return Fresh Telemetry & Rain-Rate
        Query->>Storage: Persist Fresh Snapshot to Flash
        Query-->>App: Render Live State [Green Badge]
    else Cellular Timeout / Offline Mode
        API--xQuery: Network Failure / Connection Dropped
        Query->>Storage: Read Last Validated Snapshot
        Storage-->>Query: Return Cached Snapshot (< 2h old)
        Query-->>App: Render Cached State [Amber Warning Banner]
    end
```

### Mobile Prototype Sample Code

```typescript
// app/hooks/useResilientNowcast.ts
import { useQuery } from '@tanstack/react-query';
import AsyncStorage from '@react-native-async-storage/async-storage';

interface TelemetrySnapshot {
  temperatureC: number;
  precipitationMmHr: number;
  aqiValue: number;
  severeWarning: string | null;
  fetchedAt: string;
}

const CACHE_KEY = '@prithvi_last_snapshot';

async function fetchWithHardTimeout(endpoint: string, timeoutMs = 2000): Promise<TelemetrySnapshot> {
  const controller = new AbortController();
  const timer = setTimeout(() => controller.abort(), timeoutMs);

  try {
    const res = await fetch(endpoint, { signal: controller.signal });
    if (!res.ok) throw new Error(`HTTP ${res.status}`);
    const data = await res.json();
    await AsyncStorage.setItem(CACHE_KEY, JSON.stringify(data));
    return data;
  } finally {
    clearTimeout(timer);
  }
}

export function useResilientNowcast(apiUrl: string) {
  return useQuery<TelemetrySnapshot>({
    queryKey: ['nowcast-telemetry'],
    queryFn: async () => {
      try {
        return await fetchWithHardTimeout(`${apiUrl}/api/nowcast/live`);
      } catch (err) {
        // Fallback to flash cache on 2G drop or timeout
        const cached = await AsyncStorage.getItem(CACHE_KEY);
        if (cached) {
          return { ...JSON.parse(cached), isStaleFallback: true };
        }
        throw new Error('Offline and no cached telemetry found.');
      }
    },
    staleTime: 5 * 60 * 1000, // 5 min fresh window
    refetchInterval: 60 * 1000,
  });
}
```

---

## 3. ESP32 IoT Weather Box (Hardware Edge Device)

The **PRITHVI-AI Weather Box** is an ambient edge device engineered for rural panchayats, community centers, and agrarian households lacking access to personal smartphones. Running on the **Robocraze NodeMCU-32 (ESP32-WROOM-32, 4MB Flash, 520KB SRAM)**, it provides zero-maintenance push-to-talk voice turns and live display updates.

```
+----------------------------------------------------------------------------+
|                       PRITHVI-AI AMBIENT WEATHER BOX                       |
+----------------------------------------------------------------------------+
|                                                                            |
|   +--------------------------+         [ BOOT BUTTON ]                     |
|   |  HALDIA        28.4 C    |         Short Press: Push-to-Talk (6s max)  |
|   |  RAIN: 4.2mm   AQI: 72   |         Hold 3s: Re-enter Wi-Fi Setup       |
|   |  >> STATUS: MONSOON SURGE|                                             |
|   +--------------------------+         [ STATUS LEDS ]                     |
|     128x64 I2C OLED Display            - Link (GPIO18)    : Solid / Blink  |
|                                        - Activity (GPIO19): Voice Sampling |
|   [ INMP441 I2S MIC ]                  - Alert (GPIO23)   : Hazard Warning |
|   16 kHz / 24-bit Audio Capture                                            |
|                                        [ MAX98357A I2S 3W DAC ]            |
|                                        Wired Speaker + Bluetooth A2DP Sink |
+----------------------------------------------------------------------------+
```

### Hardware Functional Highlights

- **Push-to-Talk Conversational Loop**:
  - The user presses and holds the onboard `BOOT` button to record up to 6 seconds of ambient speech.
  - The INMP441 MEMS microphone samples 16 kHz mono audio via the I2S peripheral into a DMA ping-pong buffer.
  - On release, the recorded PCM stream is packaged into a standard WAV container and uploaded via `POST /api/device/turn` to the PRITHVI backend.
  - The server transcribes speech using `faster-whisper`, interprets the query through the zero-hallucination `data()` engine, synthesizes localized audio using FastSpeech2 / Vexyl TTS, and returns audio directly to the ESP32.
  - The ESP32 streams the synthesized audio to the 3W speaker via the MAX98357A I2S DAC or paired Bluetooth A2DP speaker.
- **Zero-Cloud Provisioning (Captive Portal)**:
  - On first boot or when `BOOT` is held for 3 seconds, the ESP32 initiates an access point named `PRITHVI-SETUP` at `192.168.4.1`.
  - A mobile device joins the portal to configure local Wi-Fi credentials and device registration codes. Network tokens are secured in Non-Volatile Storage (NVS).
- **Ambient Telemetry Polling**:
  - While idle, the ESP32 polls `GET /api/device/face` every 60 seconds to refresh ambient temperature, rainfall accumulation, air quality, and disaster warnings on the SSD1306 OLED screen.

### Hardware Bill of Materials (BOM) & Wiring Pinout

| Peripheral Component | Module Model | ESP32 GPIO Pin | Electrical Function & Notes |
| :--- | :--- | :--- | :--- |
| **Microcontroller** | NodeMCU-32 (CP2102) | Onboard | Dual-core Tensilica LX6, 240 MHz, 4MB Flash, 520KB SRAM |
| **I2S Microphone** | INMP441 Omnidirectional | `GPIO32` (SCK)<br/>`GPIO33` (WS)<br/>`GPIO35` (SD) | VDD to 3.3V, GND and L/R to GND. 16 kHz mono digital audio sampling. |
| **I2S Audio Amplifier** | MAX98357A Class D 3W | `GPIO27` (BCLK)<br/>`GPIO26` (LRC)<br/>`GPIO14` (DIN) | VIN to 5V (470 µF buffer capacitor to GND). Drives 4Ω 2W speaker. |
| **OLED Display** | SSD1306 0.96" 128x64 | `GPIO21` (SDA)<br/>`GPIO22` (SCL) | I2C communication. VCC to 3.3V, GND to GND. Renders ASCII face. |
| **Link Status LED** | 3mm Green LED | `GPIO18` | Blinks during Wi-Fi handshake; solid when idle; 200Ω resistor to GND. |
| **Activity LED** | 3mm Yellow LED | `GPIO19` | Illuminates during push-to-talk microphone recording; 200Ω resistor. |
| **Alert LED** | 3mm Red LED | `GPIO23` | Strobes rapidly when an active IMD / CAP disaster alert is issued. |
| **Physical Button** | Onboard BOOT Button | `GPIO00` | Active-low. Press to talk; hold 3s to enter captive portal mode. |

### ESP32 Firmware Sample Code

```c
// main/device_turn.c - Push-to-Talk HTTP Dispatcher
#include <stdio.h>
#include <string.h>
#include "esp_http_client.h"
#include "esp_log.h"
#include "driver/i2s.h"

#define SERVER_TURN_URL "http://192.168.1.100:8000/api/device/turn"
#define MAX_AUDIO_BYTES (16000 * 2 * 6) // 6 seconds 16kHz 16-bit mono

static const char *TAG = "PRITHVI_EDGE";

esp_err_t upload_audio_turn(const uint8_t *wav_data, size_t wav_len) {
    esp_http_client_config_t config = {
        .url = SERVER_TURN_URL,
        .method = HTTP_METHOD_POST,
        .timeout_ms = 8000,
    };
    esp_http_client_handle_t client = esp_http_client_init(&config);
    if (!client) {
        ESP_LOGE(TAG, "Failed to initialize HTTP client");
        return ESP_FAIL;
    }

    esp_http_client_set_header(client, "Content-Type", "audio/wav");
    esp_http_client_set_header(client, "X-Device-Id", "esp32-node-haldia-01");

    esp_err_t err = esp_http_client_open(client, wav_len);
    if (err == ESP_OK) {
        esp_http_client_write(client, (const char *)wav_data, wav_len);
        int status_code = esp_http_client_fetch_headers(client);
        ESP_LOGI(TAG, "Server responded with HTTP %d", status_code);

        // Stream synthesized speech response directly to I2S speaker buffer
        char rx_buf[1024];
        int read_bytes = 0;
        size_t bytes_written = 0;
        while ((read_bytes = esp_http_client_read(client, rx_buf, sizeof(rx_buf))) > 0) {
            i2s_write(I2S_NUM_0, rx_buf, read_bytes, &bytes_written, portMAX_DELAY);
        }
    } else {
        ESP_LOGE(TAG, "HTTP POST failed: %s", esp_err_to_name(err));
    }

    esp_http_client_cleanup(client);
    return err;
}
```

---

## 4. PRITHVI-AI Meteorological Nowcast Research

The core scientific contribution of PRITHVI-AI is its **0–6 Hour Sub-Kilometer Meteorological Nowcasting Engine**. Traditional Numerical Weather Prediction (NWP) models (such as GFS or ECMWF) run on 6-to-12 hour update cycles, often failing to predict severe, localized convective storms common in the tropics (e.g., *Kalbaishakhi* / Nor'westers in Eastern India or localized monsoon cloudbursts).

PRITHVI-AI formulates a multi-sensor assimilation model specifically tailored for rapid-onset convective phenomena.

### Formulation 1: Between-Scene Kalman Rain-Rate Smoothing Filter

Geostationary satellite scans (ISRO INSAT-3D/3DS) arrive at discrete 15-minute intervals. Ground AWS rain-gauges report every 15 to 60 minutes. To bridge the latency between consecutive observations without artificial stepped discontinuities, PRITHVI-AI implements a discrete **Linear Kalman Filter** modeling localized precipitation dynamics:

$$\mathbf{x}_k = \mathbf{F} \mathbf{x}_{k-1} + \mathbf{w}_{k-1}, \quad \mathbf{w} \sim \mathcal{N}(0, \mathbf{Q})$$

$$\mathbf{z}_k = \mathbf{H} \mathbf{x}_k + \mathbf{v}_k, \quad \mathbf{v} \sim \mathcal{N}(0, \mathbf{R})$$

Where:
- $\mathbf{x}_k = \begin{bmatrix} R_k \\ \dot{R}_k \end{bmatrix}$ is the atmospheric state vector composed of the instantaneous rain-rate $R_k$ ($mm/h$) and rain-rate acceleration $\dot{R}_k$ ($mm/h^2$).
- $\mathbf{F} = \begin{bmatrix} 1 & \Delta t \\ 0 & 1 \end{bmatrix}$ represents the state transition matrix for time step $\Delta t = 60\text{ s}$.
- $\mathbf{H} = \begin{bmatrix} 1 & 0 \end{bmatrix}$ maps the true latent state to the observed sensor/proxy rain-rate measurement $z_k$.
- $\mathbf{Q}$ is the process noise covariance modeling cloud microphysical volatility.
- $\mathbf{R}$ is the measurement noise covariance dynamically adjusted based on observation source reliability:
  $$R_{\text{gauge}} < R_{\text{radar}} < R_{\text{satellite\_proxy}} < R_{\text{model\_analysis}}$$

The predictive update steps compute:

$$\hat{\mathbf{x}}_{k|k-1} = \mathbf{F} \hat{\mathbf{x}}_{k-1|k-1}$$

$$\mathbf{P}_{k|k-1} = \mathbf{F} \mathbf{P}_{k-1|k-1} \mathbf{F}^T + \mathbf{Q}$$

The measurement correction updates the state via the optimal Kalman Gain $\mathbf{K}_k$:

$$\mathbf{K}_k = \mathbf{P}_{k|k-1} \mathbf{H}^T \left( \mathbf{H} \mathbf{P}_{k|k-1} \mathbf{H}^T + \mathbf{R}_k \right)^{-1}$$

$$\hat{\mathbf{x}}_{k|k} = \hat{\mathbf{x}}_{k|k-1} + \mathbf{K}_k \left( z_k - \mathbf{H} \hat{\mathbf{x}}_{k|k-1} \right)$$

$$\mathbf{P}_{k|k} = (\mathbf{I} - \mathbf{K}_k \mathbf{H}) \mathbf{P}_{k|k-1}$$

This formulation guarantees that the 1 Hz nowcast playhead maintains physical smoothness across observation transitions while adapting instantly to incoming satellite or ground telemetry.

---

### Formulation 2: VERA-MoE Hybrid Ensemble Blending

PRITHVI-AI integrates a **Variational Ensemble Rain Assimilation with Mixture of Experts (VERA-MoE)** framework. The final precipitation estimate $\hat{y}_t$ at forecast horizon $t$ is computed as a dynamically gated mixture across diverse meteorological candidates:

$$\hat{y}_t = \sum_{m=1}^{M} g_m(\mathbf{c}_t) \cdot f_m(\mathbf{x}_t)$$

Where:
- $f_m(\mathbf{x}_t)$ represents individual member predictors:
  1. $f_1$: Satellite thermal infrared brightness temperature proxy ($T_b$).
  2. $f_2$: Micro-physics advection extrapolated radar field.
  3. $f_3$: High-resolution Open-Meteo numerical analysis.
  4. $f_4$: Climatological diurnal background (NASA POWER baseline).
- $g_m(\mathbf{c}_t)$ are the gating weights computed through a softmax function conditioned on environmental contextual vector $\mathbf{c}_t$ (including convective available potential energy (CAPE), surface relative humidity, and solar zenith angle):
  $$g_m(\mathbf{c}_t) = \frac{\exp(\mathbf{w}_m^T \mathbf{c}_t)}{\sum_{j=1}^{M} \exp(\mathbf{w}_j^T \mathbf{c}_t)}, \quad \sum_{m=1}^{M} g_m(\mathbf{c}_t) = 1$$

---

### Formulation 3: Georeferenced INSAT-3D/3DS IR Convective Cell Proxy

High-resolution Doppler Weather Radar (DWR) coverage is incomplete across certain inland and coastal tracts of India. PRITHVI-AI establishes a fallback convective cell detection algorithm using the public Asia-sector georeferenced **INSAT-3D/3DS IR1 (10.8 µm)** infrared imagery.

Convective rain-rate is inferred using an adapted **Adler-Negri Convective Stratiform Technique (CST)** relating cloud-top brightness temperature $T_b$ (Kelvin) to convective rainfall intensity:

$$R(T_b) = \begin{cases} 
  a_0 + a_1 T_b + a_2 T_b^2 & \text{if } T_b < T_{\text{threshold}} \\
  0 & \text{otherwise}
\end{cases}$$

Where:
- $T_{\text{threshold}} = 235\text{ K}$ defines the convective cloud threshold.
- Deep convective cores with $T_b < 210\text{ K}$ indicate overshooting cloud tops and trigger high-priority lightning and squall warnings.
- The spatial coordinates are bounded to the IMD SATMET SOP Asia sector ($40^{\circ}\text{E} - 110^{\circ}\text{E}$, $10^{\circ}\text{S} - 45^{\circ}\text{N}$) and masked strictly within the Indian landmass ($68.0^{\circ}\text{E} - 97.5^{\circ}\text{E}$, $6.5^{\circ}\text{N} - 37.5^{\circ}\text{N}$) to eliminate non-territorial false alarms.

---

### Formulation 4: Lightning Strike Probability Nowcast

Convective lightning strikes represent one of the deadliest meteorological threats in South Asia. PRITHVI-AI formulates a real-time strike probability index ($P_{\text{strike}} \in [0, 1]$) evaluated across a 75 km regional radius:

$$P_{\text{strike}} = \sigma \left( \beta_0 + \beta_1 N_{\text{flash}} + \beta_2 \left( \frac{\text{CAPE}}{1000} \right) + \beta_3 \Delta T_b \right)$$

Where:
- $\sigma(z) = \frac{1}{1 + e^{-z}}$ is the standard sigmoid activation.
- $N_{\text{flash}}$ is the number of VHF lightning strokes detected by Weatherbit within the preceding 45-minute moving window.
- $\text{CAPE}$ is the convective available potential energy ($J/kg$).
- $\Delta T_b = \max(0, T_{\text{anvil}} - T_{\text{core}})$ represents the brightness temperature gradient across the convective cloud anvil.
- Threat windows are classified into:
  - **No Threat** ($P_{\text{strike}} < 0.20$)
  - **Elevated Watch** ($0.20 \le P_{\text{strike}} < 0.60$)
  - **Imminent Convective Strike Warning** ($P_{\text{strike}} \ge 0.60$, 15–60 min lookahead).

---

### Nowcasting Research Sample Code

```python
# science/kalman_nowcast.py
import numpy as np

class KalmanRainRateFilter:
    """
    Between-scene Kalman filter for continuous 1 Hz rain-rate estimation
    smoothing satellite infrared proxies and ground automatic weather station telemetry.
    """
    def __init__(self, dt: float = 60.0):
        self.dt = dt
        # State: [rain_rate (mm/h), rain_rate_derivative (mm/h^2)]
        self.x = np.array([[0.0], [0.0]], dtype=np.float64)
        # State transition matrix F
        self.F = np.array([[1.0, dt],
                           [0.0, 1.0]], dtype=np.float64)
        # Measurement matrix H (we observe only rain-rate)
        self.H = np.array([[1.0, 0.0]], dtype=np.float64)
        # Process covariance Q
        self.Q = np.array([[0.05 * (dt**3)/3, 0.05 * (dt**2)/2],
                           [0.05 * (dt**2)/2, 0.05 * dt]], dtype=np.float64)
        # State estimation error covariance P
        self.P = np.eye(2, dtype=np.float64) * 1.0

    def predict(self) -> float:
        """Propagate state forward by dt seconds."""
        self.x = self.F @ self.x
        self.x[0, 0] = max(0.0, self.x[0, 0]) # Non-negative precipitation constraint
        self.P = self.F @ self.P @ self.F.T + self.Q
        return float(self.x[0, 0])

    def update(self, measured_rate: float, source_type: str = "satellite-proxy") -> float:
        """
        Incorporate new measurement with adaptive sensor noise covariance R.
        """
        # Dynamic measurement variance R based on sensor characteristics
        r_table = {
            "rain_gauge": 0.1,
            "doppler_radar": 0.5,
            "satellite_proxy": 2.0,
            "model_analysis": 4.0
        }
        R = np.array([[r_table.get(source_type, 2.0)]], dtype=np.float64)

        z = np.array([[measured_rate]], dtype=np.float64)
        y = z - (self.H @ self.x) # Innovation
        S = self.H @ self.P @ self.H.T + R # Innovation covariance
        K = self.P @ self.H.T @ np.linalg.inv(S) # Optimal Kalman gain

        self.x = self.x + (K @ y)
        self.x[0, 0] = max(0.0, self.x[0, 0])
        I = np.eye(2, dtype=np.float64)
        self.P = (I - K @ self.H) @ self.P
        return float(self.x[0, 0])


def adler_negri_rain_proxy(tb_kelvin: float) -> float:
    """
    Computes Adler-Negri convective rainfall rate proxy from
    INSAT-3D/3DS IR1 (10.8 um) brightness temperature.
    """
    if tb_kelvin >= 235.0:
        return 0.0 # Non-convective or clear sky
    if tb_kelvin <= 200.0:
        return 45.0 # Extreme convective overshooting core ceiling

    # Polynomial fit: R = a0 + a1*Tb + a2*Tb^2
    a0 = 112.5
    a1 = -0.72
    a2 = 0.00115
    rate = a0 + a1 * tb_kelvin + a2 * (tb_kelvin ** 2)
    return float(np.clip(rate, 0.0, 45.0))
```

---

## 5. Visual Prototype Gallery

<div align="center">

| Prototype Visual Asset | Functional Description |
| :---: | :---: |
| <img src="assets/sih_reference.png" alt="Smart India Hackathon Poster" width="400" /> | **Smart India Hackathon Reference Poster**: Comprehensive multi-hazard early warning and agro-advisory operational architecture. |
| <img src="assets/prithvi_3d_bot.png" alt="PRITHVI-AI 3D Bot" width="280" /> | **PRITHVI-AI Multilingual Diagnostic Mascot**: Embedded in the Web UI and mobile application for interactive speech and text advisory. |
| <img src="assets/mobile_splash.png" alt="Mobile App UI" width="280" /> | **Native Android / iOS Application Interface**: React Native Expo splash screen and mobile brand identity. |
| <img src="assets/logo.png" alt="PRITHVI-AI Logo" width="240" /> | **Official PRITHVI-AI Insignia**: Symbolizing meteorological observation, earth observation satellites, and agrarian protection. |

</div>

---

## 6. Repository Structure & Specifications

This repository serves strictly as a **prototype, specification, and architectural documentation repository**. To inspect in-depth hardware schematics, mobile blueprints, web designs, and mathematical derivations, explore the `docs/` catalog:

```
.
├── assets/
│   ├── icon.svg                     # Vector brand symbol
│   ├── logo.png                     # Official high-resolution platform logo
│   ├── mobile_splash.png            # Mobile application splash screen asset
│   ├── prithvi_3d_bot.png           # 3D interactive AI assistant mascot
│   └── sih_reference.png            # SIH comprehensive platform reference poster
├── docs/
│   ├── ESP32_DEVICE.md              # Hardware schematics, I2S wiring & captive portal specs
│   ├── MOBILE_APP.md                # React Native Expo architecture, offline cache & sandboxed Leaflet
│   ├── NOWCAST_RESEARCH.md          # Full mathematical derivations of Kalman & VERA-MoE models
│   └── WEB_UI.md                    # Next.js 14 Web UI lenses, state models & responsive layouts
└── README.md                        # Master prototype blueprint and research overview
```

---

<div align="center">
  <sub>Developed for India's Climate Resilience, Farmers & Disaster Management Authorities.</sub><br/>
  <sub>PRITHVI-AI • Built with Open Science, Open Models & Zero-Hallucination Design.</sub>
</div>
