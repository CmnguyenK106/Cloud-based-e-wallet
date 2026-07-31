---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
includeInReport: false
---
# [Case Study Summary] Riot Games: Processing 20 TB Daily Analytics Data with Amazon MSK on AWS

## Document Metadata
* **Domain:** Online Gaming, eSports, Real-Time Streaming Analytics, Big Data Engineering.
* **Target System:** Riot Games Data & Game Infrastructure (League of Legends, VALORANT, TFT).
* **Key Architecture Pattern:** Event-Driven Stream Ingestion + Real-Time Stream Processing + Decoupled Data Lake.
* **AWS Core Stack:** Amazon MSK (Managed Streaming for Apache Kafka), Amazon EMR (Apache Spark), Amazon S3, Amazon EKS, Amazon Athena / OpenSearch.

---

## 1. Business Context & Problem Statement

### 1.1 System Scale
* **User Base:** 180+ million Monthly Active Users (MAU) globally.
* **Data Volume:** ~20 TB of telemetry and analytics data generated daily.
* **Core Downstream Systems:** Matchmaking engines, in-game personalization, anti-cheat & security detection, player behavior systems, and real-time eSports broadcast graphics.

### 1.2 Technical Bottlenecks & Challenges
1. **High Latency (3–6 Hours):** Legacy MapReduce batch pipeline caused a 3-to-6-hour delay between in-game event generation and data availability for querying.
2. **High Operational Overhead & TCO:** Managing legacy batch infrastructure was resource-intensive and expensive.
3. **Inability to Support Real-Time Use Cases:** Batch processing could not support real-time requirements such as instant anti-cheat detection or dynamic matchmaking adjustments.

---

## 2. Technical Architecture Breakdown

### Component Deep-Dive

#### A. Stream Ingestion Layer
* **Amazon MSK (Managed Streaming for Apache Kafka):** Serves as the central messaging backbone. Ingests all game event streams globally, replacing legacy MapReduce pipelines while eliminating Kafka cluster operational maintenance.

#### B. Stream Processing & Data Lake Layer
* **Apache Spark on Amazon EMR:** Processes, filters, and transforms streaming data in near real-time as events flow through MSK.
* **Amazon S3 Data Lake:** Stores structured and processed game events durably, allowing direct queries via Amazon Athena and OpenSearch.

#### C. Compute & Container Orchestration
* **Amazon EKS (Elastic Kubernetes Service):** Containerized infrastructure hosting game server workloads and microservices, scaling automatically based on player traffic.

---

## 3. Key Technical & Business Results

* **Latency Reduction:** Query latency reduced from **6 hours down to 5 minutes**.
* **Real-Time Security & Anti-Cheat:** Enabled immediate toxicity detection and anti-cheat anomaly identification near real-time.
* **Infrastructure Cost Savings:** Migration to Amazon EKS saved **$10 million in annual infrastructure costs**.
* **Global Deployment Speed:** Accelerated new game region deployment speed by **12x**.
* **eSports Analytics:** Real-time match data extraction powers live broadcast statistics for global eSports tournaments (e.g., Worlds, VCT).

---

## 4. Key Engineering Takeaways

1. **Leveraging Managed Kafka (MSK):** Offloading Kafka cluster operations to a managed service frees engineering teams to focus on core data processing and business logic.
2. **Batch to Real-Time Shift:** Converting legacy MapReduce pipelines into real-time Kafka streams unlocks crucial sub-minute analytics for fraud/cheat detection and user experience optimization.

## 5. Post and URL

![Riot](/images/3-BlogsPosted/3.1-Blog1/blog_1.png)

<p style="text-align: center;"><em>Figure 3.3. Blog Post.</em></p>

How Riot Games processes 20 TB of analytics data daily on AWS [Here](https://youtu.be/5L1K_moG-dY?si=UbMtqlufY4SgawjE).

Riot Games Cuts $10M Annual Infrastructure Costs by Migrating to Amazon EKS [Here](https://aws.amazon.com/vi/solutions/case-studies/riot-games-case-study/).

Scaling global game infrastructure using AWS Local Zones with Riot Games [Here](https://aws.amazon.com/vi/solutions/case-studies/riot-games-local-zones-case-study/)