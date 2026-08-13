# Global Airbnb Performance Dashboard | Power BI

## 📊 Project Overview

The **Global Airbnb Performance Dashboard** is an interactive Business Intelligence project developed using **Microsoft Power BI** to analyze Airbnb listings, hosts, room types, pricing, customer ratings, and reviewer behavior.

The project transforms raw Airbnb data into an interactive dashboard designed to identify patterns and compare performance across cities, accommodation types, hosts, ratings, and reviews.

## 🎯 Business Problem

Airbnb data contains large volumes of information about listings, hosts, pricing, locations, room types, ratings, and reviews. The objective of this project was to organize these data points into a clear analytical dashboard to understand:

* Listing and host distribution
* City-level Airbnb performance
* Room-type distribution
* Pricing differences across room types
* Customer rating performance
* Superhost activity
* Reviewer behavior and review frequency
* Cumulative reviewer contribution

## 📁 Dataset

The project uses the **Airbnb Listings & Reviews** dataset provided through the **Maven Analytics Data Playground**.

The dataset contains Airbnb information covering **250,000+ listings across 10 major cities** and **5 million+ historical reviews**.

**Dataset Source:**
[https://mavenanalytics.io/data-playground/airbnb-listings-reviews](https://mavenanalytics.io/data-playground/airbnb-listings-reviews)

**Original Data Source:** Inside Airbnb
**License listed by Maven Analytics:** Public Domain

The original dataset is not included in this repository because of its large file size. It can be accessed through the source link above.

## 🛠️ Tools & Technologies

* Microsoft Power BI
* DAX
* Data Modeling
* Data Transformation
* Data Visualization
* Interactive Dashboard Design

## 📈 Dashboard Analysis

### 1. Overview

The Overview page provides a high-level view of Airbnb performance through KPI cards and visual analysis.

Key areas include:

* Total listings
* Number of cities
* Hosts
* Property types
* Reviews
* Host activity over time
* Listing and market distribution

### 2. Ratings

The Ratings page focuses on customer experience and listing performance.

Analysis includes:

* Accuracy
* Cleanliness
* Communication
* Location
* Value
* City-level rating comparison
* Room-type pricing
* Superhost/listing analysis

### 3. Reviews

The Reviews page analyzes reviewer activity and review frequency.

Analysis includes:

* Unique reviewers
* Reviews per reviewer
* Review frequency
* Cumulative reviewers
* Cumulative percentage of reviewers
* Pareto-style review-frequency analysis

## 🧮 DAX Analysis

The project uses DAX measures and calculated columns for analytical calculations such as:

* Total listings
* Room-type listing counts
* Average rating scores
* City ranking
* Reviews per reviewer
* Unique reviewers
* Cumulative reviewers
* Cumulative review percentage

Important DAX functions used include:

`CALCULATE`, `COUNT`, `DISTINCTCOUNT`, `AVERAGE`, `FILTER`, `ALL`, `ALLEXCEPT`, `REMOVEFILTERS`, `RANKX`, `DIVIDE`, `IF`, `MAX`, and `VAR`.

Detailed DAX calculations are documented in **DAX_Measures.md**.

## 📊 Review Frequency Pareto Analysis

A key analytical component of the project is the **Review Frequency Pareto-style chart**.

The chart combines:

* **Columns:** Number of reviewers at each review-frequency level
* **Line:** Cumulative percentage of total reviewers

This analysis helps understand how reviewer activity accumulates across different review-frequency groups.

## 🔍 Key Analytical Questions

The dashboard was designed to answer questions such as:

* Which cities have the largest Airbnb listing presence?
* How are listings distributed across room types?
* Which room types have higher average prices?
* How do cities compare across customer-rating dimensions?
* How are listings distributed between Superhosts and non-Superhosts?
* How many unique reviewers are present?
* How frequently do reviewers leave reviews?
* How does cumulative reviewer contribution change as review frequency increases?

## 💡 Skills Demonstrated

### Technical Skills

* Power BI
* DAX
* Data Modeling
* Data Visualization
* KPI Development
* Interactive Reporting
* Conditional Formatting
* Calculated Columns
* Measures
* Ranking
* Cumulative Analysis

### Analytical Skills

* Exploratory Data Analysis
* Comparative Analysis
* Trend Analysis
* Segmentation
* Performance Analysis
* Reviewer Behavior Analysis
* Pareto-style Analysis
* Data Storytelling

## 🎯 Project Outcome

The completed dashboard transforms raw Airbnb listing and review data into an interactive analytical reporting solution. It enables users to evaluate listing concentration, room and property-type distribution, pricing patterns, customer ratings, Superhost activity, and reviewer behavior through a unified Power BI dashboard.

The project demonstrates an end-to-end analytics workflow:

**Raw Data → Data Modeling → DAX → Analysis → Visualization → Interactive Dashboard → Business Insights**
