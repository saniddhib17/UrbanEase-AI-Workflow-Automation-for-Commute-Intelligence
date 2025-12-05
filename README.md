# 🛣️ Urban Calm Index – Smart Commute Stress Automation (n8n + TomTom + OpenWeather + AI)

> This project automates the end-to-end evaluation of daily commute stress by combining real-time traffic, live weather metrics, and lightweight AI summarization inside an **n8n workflow**. The goal is to provide commuters with actionable, personalized travel forecasts that minimize uncertainty and improve planning.

## 🚀 Project Overview

The Urban Calm Index is a fully automated, scheduled **n8n pipeline** designed to simplify the daily commute decision-making process.

The pipeline performs the following steps autonomously:

* Fetches **real-time traffic data** from the TomTom Routing API.
* Retrieves **live weather information** (temperature, humidity, description) via OpenWeatherMap.
* Computes a custom **Commute Stress Index (CSI)** based on a weighted combination of traffic delay, travel duration, and environmental factors.
* Generates AI-powered, concise travel advisories using **Google Gemini**.
* Sends a daily email alert summarizing travel conditions, expected delays, and personalized recommendations.

---

## ⚙️ Key Features

### 1. Automated Multi-Source Data Collection
| Source | Data Collected | Purpose |
| :--- | :--- | :--- |
| **TomTom Routing API** | Travel time, Traffic delay, Route summary | Real-time congestion and route metrics. |
| **OpenWeatherMap API** | Temperature (°C), Humidity (%), Weather description | Environmental impact on the commute. |

### 2. Commute Stress Index (CSI)
A custom, weighted score is calculated and categorized to allow users to quickly interpret travel conditions:

* **Weighting Factors:** Travel time normalization, traffic delay severity, temperature deviation from a comfort zone, and humidity impact.
* **Categories:** **Low**, **Moderate**, **High**, **Very High**.

### 3. 🤖 AI-Generated Summary
Google Gemini creates a single, concise, and user-friendly advisory, making the alert instantly digestible.

> **Example Summary:** "Expect moderate delays today due to higher-than-usual congestion; consider leaving a few minutes earlier for a calmer commute."

### 4. 📧 Daily Email Delivery
The system automatically sends a formatted email alert containing all crucial information:

* Route name and expected travel time
* Delay in minutes
* Temperature & humidity
* Stress score and category (CSI)
* AI-generated advice and recommendations

---

## 🧩 Workflow Architecture

The entire process is orchestrated within a single n8n workflow, utilizing a modular, maintainable design.



The workflow is composed of the following n8n nodes:

1.  **Schedule Trigger:** Executes the workflow daily at a configured time.
2.  **Custom Route Builder (Code Node):** Defines the start/end points.
3.  **Weather API Call (HTTP Request):** Fetches OpenWeather data.
4.  **TomTom Traffic API Call:** Fetches real-time routing data.
5.  **Merge Node:** Combines weather and traffic data payloads.
6.  **Stress Score Calculation (Code Node):** Computes the CSI.
7.  **AI Summary (Google Gemini):** Generates the advisory text.
8.  **Email Delivery (Gmail Node):** Sends the final alert.

---

## 📊 Commute Stress Index (CSI) Formula Breakdown

The CSI is a weighted average of normalized factors, providing a quantitative measure of commute difficulty.

### Formula
$$\text{stress} = 0.7 \cdot \text{travelNorm} + 0.2 \cdot \text{tempNorm} + 0.1 \cdot \text{humNorm}$$

| Variable | Description |
| :--- | :--- |
| $\text{travelNorm}$ | Travel time normalized against a defined limit (e.g., 45 minutes). |
| $\text{tempNorm}$ | Weather temperature normalized (comfort range: 18–35°C). |
| $\text{humNorm}$ | Humidity normalized to a 0–1 scale. |

### Stress Buckets
| CSI Score | Stress Category |
| :--- | :--- |
| $< 0.40$ | **Low** |
| $0.40 – 0.59$ | **Moderate** |
| $0.60 – 0.74$ | **High** |
| $\ge 0.75$ | **Very High** |

---

## 🛠️ Tech Stack

| Technology | Role |
| :--- | :--- |
| **n8n** | Primary workflow automation and orchestration engine. |
| **TomTom Routing API** | Source for real-time traffic and routing data. |
| **OpenWeatherMap API** | Source for real-time weather metrics. |
| **Google Gemini (LLM)** | Natural-language summarization and advice generation. |
| **Gmail API** | Sending automated email notifications. |
| **JavaScript** | Custom business logic within n8n Code Nodes. |

---

## 🧪 Example Use Cases

* **Daily Commute Planning:** Personalized alerts for individual commuters.
* **Office Operations:** Providing travel advisories for staff to optimize arrival times.
* **Predictive Congestion Monitoring:** Identifying trends in traffic and environmental stress.
* **Logistics & Field Teams:** Automated notifications for field agents to plan their routes efficiently.

---

## 🏁 Results

By automating data synthesis and leveraging AI, the Urban Calm Index workflow successfully:

* Reduces commuter **uncertainty**.
* Provides **data-driven** travel insights.
* Enhances productivity by helping users **avoid peak congestion**.
* Combines multi-source API data into a single, **actionable alert**.
