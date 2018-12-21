# Introduction to the InfluxData Platform

- The InfluxData Platform is the leading modern **time series platform** designed from the ground up for **metrics and events**. 
- It is comprised of **four core components: Telegraf, InfluxDB, Chronograf, and Kapacitor** (often referred to as the TICK stack). 
- Each fulfills a specific role in managing your time-series data: 
	+ ***Telegraf*** 	- *Data collection*
	+ ***InfluxDB*** 	- *Data storage*
	+ ***Chronograf*** 	- *Data visualization*
	+ ***Kapacitor*** 	- *Data processing and events*

- Enterprise versions of InfluxDB and Kapacitor provide clustering, access control, and incremental backup functionality for production infrastructures at scale.

## What is time series data?
- ***Time series data is a series of data points each associated with a specific time***. Examples include:
```
    + Server performance metrics
    + Financial averages over time
    + Sensor data, such as temperature, barometric pressure, wind speeds, etc.
```

## Why shouldn’t I just use a relational database?
- Relational databases can be used to store and analyze time series data, but depending on the precision of your data, a query can involve potentially millions of rows. 
- InfluxDB is purpose-built to store and query data by time, providing out-of-the-box functionality that optionally downsamples data after a specific age and a query engine optimized for time-based data.

## The TICK stack - Open Source Components

- Each fulfills a specific role in managing your time-series data: 
	+ ***Telegraf*** 	- *Data collection*
	+ ***InfluxDB*** 	- *Data storage*
	+ ***Chronograf*** 	- *Data visualization*
	+ ***Kapacitor*** 	- *Data processing and events*

**Telegraf - Data Collection**
Telegraf is a data collection agent that captures data from a growing list of sources and translates it into Line Protocol data format for storage in InfluxDB. It’s “pluggable”, extensible architecture makes it easy to create plugins that both pull and push data from and to different sources and endpoints.

**InfluxDB - Data Storage**
InfluxDB stores data for any use case **involving large amounts of timestamped data**, including DevOps monitoring, log data, application metrics, IoT sensor data, and real-time analytics. It provides functionality that allows you to conserve space on your machine by keeping data for a defined length of time, then automatically downsampling or expiring and deleting unneeded data from the system.

**Chronograf - Data Visuzalization**
Chronograf is the user interface for the TICK stack that provides customizable dashboards, data visualizations, and data exploration. It also allows you to view and manage Kapacitor tasks.

**Kapacitor - Data Processing & Events**
Kapacitor is a data processing framework that enables you to process and act on data as it is written to InfluxDB. This includes detecting anomalies, creating alerts based on user-defined logic, and running ETL jobs.