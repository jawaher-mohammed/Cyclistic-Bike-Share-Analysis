# Cyclistic Bike-Share Analysis 🚴‍♀️📊
End-to-end data analysis portfolio project for the Google Data Analytics Professional Certificate.

---

## (1. Phase: Ask)

### 1. Scenario & Background
* **The Company:** Cyclistic is a bike-share company featuring a fleet of over 5,800 geotracked bicycles and 692 docking stations across Chicago.
* **Customer Segments:** Cyclistic offers flexible pricing options, including single-ride passes and full-day passes (categorized as casual riders), alongside annual subscriptions (categorized as member riders).
* **Financial Insight:** Finance analysts have concluded that annual members are much more profitable than casual riders.
* **The Stakeholders:** Lily Moreno (Director of Marketing) believes the company's future growth depends on maximizing the number of annual memberships rather than focusing on attracting all-new customers.

### 2. Business Task
* **Core Objective:** Analyze 12 months of historical Cyclistic trip data to understand how annual members and casual riders use the service differently.
* **Primary Goal:** Design data-driven marketing strategies and actionable recommendations to convert casual riders into annual members, pending approval from executive stakeholders.

---

## (2. Phase: Prepare)
* **Data Source & Privacy:** This analysis utilizes reliable, public historical trip data provided by Cyclistic. The extracted datasets cover a 12-month period, from September 2025 to August 2026. To maintain data ethics and ensure rider privacy, all datasets have been strictly stripped of any Personally Identifiable Information (PII) prior to processing.

---

## (3. Phase: Process)
* **Phase Objective:** To prepare, clean, transform, and validate the consolidated 12-month Cyclistic trip dataset, ensuring high data integrity, eliminating errors and outliers, and engineering key analytical fields required for the upcoming analysis phase.
* **Tools Used:** 
  * SQL (Google BigQuery): Used for data consolidation, auditing, cleaning, and feature engineering.
  * Google Docs / Markdown: Used for project documentation.
* **Data Consolidation:** Merged 12 individual monthly tables (`trip_data_1` through `trip_data_12`) into a unified table named `cyclistic_data.combined_tripdata` using `UNION ALL`.
* **Data Audit & Findings:**
  * **Duplicates Check:** Identified 40 duplicate rows using `ride_id` uniqueness verification.
  * **Missing Values (NULLs) Check:** Core attributes (`ride_id`, `started_at`, `ended_at`, `member_casual`) contained zero missing values. Missing values identified in station details (`start_station_name` and `end_station_name`) due to un-docked electric bike trips.
  * **Decision:** Retained these records to avoid losing valid trip duration and user behavioral data.
* **Data Cleaning & Feature Engineering:** Created the final cleaned table `cyclistic_data.cleaned_tripdata` within a single SQL script implementing:
  * **Deduplication:** Applied `ROW_NUMBER() OVER (PARTITION BY ride_id ORDER BY started_at)` filtering for `row_num = 1` to eliminate all 40 duplicate records.
  * **Outlier Filtering:** Excluded trip durations `<= 0` minutes and trips `> 1,440` minutes (24 hours).
  * **Derived Fields:** `ride_length_minutes`, `day_of_week`, `month`, `year`.
* **Final Validation & Sanity Check:** Duplicate count reduced to 0; trip duration range strictly validated between 1 and 1,440 minutes. Dataset status: 100% verified, cleaned, and ready for Phase 4.

---

## (4. Phase: Analyze)
* **Phase Objective:** To analyze the cleaned Cyclistic trip dataset and identify key differences, behavioral patterns, and usage trends between annual members and casual riders.
* **1. General Usage Statistics:**
  * *Key Insight:* Annual members generate the majority of total demand (64.89% / ~3.9M rides), whereas casual riders account for 35.11% (~2.1M rides). However, casual riders record significantly longer trip durations, averaging 18.18 minutes compared to 12.13 minutes for members.
  * *Business Meaning:* Annual members utilize the service for quick, functional point-to-point transportation, while casual riders use it for longer leisure and exploration trips.
* **2. Day of the Week Analysis:**
  * *Key Insight:* Annual member usage peaks during mid-week working days (Wednesday: ~623K rides, Tuesday: ~622K rides) with short, highly consistent trip durations (~11-12 mins). Conversely, casual ride volume spikes heavily on weekends (Saturday: ~445K rides) with trip lengths exceeding 20 minutes.
  * *Business Meaning:* Confirms two distinct user personas—members rely on Cyclistic for routine daily commutes, while casual riders represent weekend recreational and tourism traffic.
* **3. Monthly & Seasonal Analysis:**
  * *Key Insight:* Casual ride volume is heavily seasonal, peaking in July (~350K rides) during summer holidays and dropping by over 93% in winter (January: ~24K rides). Member usage peaks in August (~514K rides) upon returning to routines and maintains a resilient baseline throughout winter.
  * *Business Meaning:* Casual demand is highly weather and holiday dependent, while member demand is anchored to consistent year-round work and academic schedules.
* **4. Bike Type Preferences Analysis:**
  * *Key Insight:* Electric bikes are the preferred choice across both segments, accounting for 73.18% of casual rides and 67.64% of member rides. Casual riders on classic bikes record the highest overall average duration across the dataset at 28.69 minutes.
  * *Business Meaning:* Highlights strong demand for electric fleet availability, while classic bikes serve extended casual leisure trips.

---

## (5. Phase: Share)
* **Phase Objective:** To build an interactive, executive-level dashboard in Tableau that visually communicates key behavioral differences between annual members and casual riders.
* **Dashboard Preview:**
![Tableau Dashboard](Dashboard%201.png)

* **Design Elements & Architecture:**
  * *Executive Grid Layout:* Structured as a balanced 2x2 grid to maximize readability.
  * *White Card Container Effect:* Applied white sheet backgrounds (`#FFFFFF`) over a light-gray canvas (`#F8F9FA`).
  * *Distinct Color Palette:* Navy Blue (`#2A5C8A`) for Members and Coral Orange (`#E07A5F`) for Casuals.
* **Key Visualizations Included:** User Type Distribution (%), Daily Ride Patterns by User Type, Monthly Ride Trends & Seasonality, Bike Type Preference by User Type.

---

## (6. Phase: Act)
* **Phase Objective:** To translate analytical findings and visual insights into actionable, data-driven marketing strategies and executive recommendations.
* **Executive Recommendations:**
  1. **Targeted Weekend Membership Tier:** Introduce a specialized weekend-only annual pass tailored specifically to recreational casual riders.
  2. **Seasonality-Driven Conversion Campaigns:** Launch targeted digital campaigns and limited-time conversion discounts during early spring (April/May) right before peak summer usage.
  3. **Electric Bike Member Perks:** Provide exclusive member benefits on Electric Bikes (such as priority reservations or discounted per-minute rates) to incentivize annual upgrades.
  4. **In-App Loyalty & Conversion Program:** Implement a gamified rewards system where casual riders earn points based on total ride time, redeemable as credits toward an annual membership.
* **Next Steps & Implementation:**
  * Present dashboard findings and strategic recommendations to executive leadership (Lily Moreno).
  * Collaborate with marketing and product development teams to configure the weekend pass in the mobile app.
  * Establish quarterly tracking dashboards to monitor conversion rates post-launch.

---
*Full detailed report available in [Cyclistic_Bike_Share_Case_Study.pdf](Cyclistic_Bike_Share_Case_Study.pdf).*
