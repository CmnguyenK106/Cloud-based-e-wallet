# [Case Study Summary] Formula 1 (F1 Insights): Real-Time Telemetry Processing & ML Predictions on AWS

## 📌 Document Metadata
* **Domain:** Professional Sports, Media & Entertainment, IoT, Real-Time Analytics, Predictive ML.
* **Target System:** Formula 1 (F1 Insights Live Broadcast System).
* **Key Architecture Pattern:** Event Stream Processing + Low-Latency ML Inference + Feature Store Pattern + Decoupled Ingestion.
* **AWS Core Stack:** Amazon Kinesis Data Streams, Amazon SageMaker, Amazon DynamoDB, AWS Lambda, Amazon Managed Service for Apache Flink, Amazon S3.

---

## 1. Business Context & Problem Statement

### 1.1 System Scale
* **Sensors per Car:** Over 300 IoT sensors per F1 car measuring tire temperature, brake force, ERS pressure, G-force, throttle, and aerodynamics.
* **Data Volume:** 1.1 million telemetry data points per second generated across 20 cars.
* **Historical Context:** 3 GB of telemetry data per car per race weekend, combined with 70+ years of historical race data dating back to 1950.
* **Global Audience:** 1.5+ billion TV viewers worldwide expecting live, interactive broadcast stats.

### 1.2 Technical Bottlenecks & Challenges
1. **Ultra-Low Latency Constraint (< 100ms):** Telemetry data must travel from car sensors to trackside servers, over the cloud for ML inference, and back to broadcast graphics engines in under 100–200ms to stay synchronized with live TV footage.
2. **Lossy Network Environment:** Vehicles moving at 350 km/h cause intermittent RF signal drops, requiring robust stream buffering and handling of out-of-order data.
3. **Real-Time Feature Engineering:** Blending live telemetry streams with decades of historical data on S3 to assess driver style, track conditions, and strategy windows instantly.

---

## 2. Technical Architecture Breakdown

### Component Deep-Dive

#### A. Ingestion Layer
* **Trackside Edge Processing:** RF wireless receiver trackside ingests raw telemetry from cars and applies initial filtering.
* **Amazon Kinesis Data Streams:** Serves as a high-throughput, auto-scaling event buffer to handle millions of streaming events per second with zero data loss.

#### B. Stream Processing & Feature Store Layer
* **AWS Lambda & Apache Flink:** Performs stream transformation, noise filtering, and real-time aggregations (e.g., sector average speeds).
* **Amazon DynamoDB:** Serves as an ultra-low latency (<10ms) state store/feature store to maintain real-time vehicle state (tire wear, position, gap to cars ahead/behind).

#### C. Machine Learning Inference Layer
* **Amazon S3 Data Lake:** Stores 70+ years of historical race data used to train predictive ML models.
* **Amazon SageMaker:** Trains complex predictive models offline and hosts them on **SageMaker Real-Time Inference Endpoints**, executing sub-20ms ML inference per request.

---

## 3. Machine Learning Predictive Use Cases (F1 Insights)

| F1 Insight Graphic | Machine Learning Model / Technique | Value Delivered |
| :--- | :--- | :--- |
| **Overtake Probability** | Analyzes car distance, speed delta, tire degradation, aerodynamic drag, and upcoming DRS zones. | Predicts exact % probability of a pass at the next corner. |
| **Tire Performance & Life** | Predicts degradation using G-forces, track surface temp, brake pressure, and historical driver style. | Shows real-time tire wear % without waiting for pit stops. |
| **Pit Strategy Battle** | Compares undercut/overcut pace analysis and gap windows in traffic. | Forecasts optimal pit stop timing and post-pit track position. |
| **Corner Analysis** | Compares telemetry between drivers at specific apexes (braking point, apex speed, throttle timing). | Explains driver time deltas per sector visually. |

---

## 4. Key Engineering Takeaways

1. **Decoupled Stream Architecture:** Separating ingestion (Kinesis) from inference (SageMaker) prevents broadcast rendering bottlenecks from impacting upstream data processing.
2. **In-Memory & Low-Latency Feature Store:** Sub-10ms state store access (DynamoDB) is essential for real-time ML inference engines to make instantaneous decisions.
3. **Edge-Cloud Hybrid Pattern:** Filtering noise at the trackside edge before transmitting to AWS Cloud optimizes expensive bandwidth.