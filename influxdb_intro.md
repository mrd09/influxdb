# 1. Introduction to the InfluxData Platform

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

# 2. Time-Series Data:
- Time-series Data: 
    - là một chuỗi các điểm dữ liệu, thường bao gồm các phép đo liên tiếp được thực hiện từ cùng một nguồn trong một khoảng thời gian. 
    - Phân tích chuỗi thời gian có mục đích nhận dang và tập hợp lại các yếu tố, những biến đổi theo thời gian mà nó có ảnh hưởng đến giá trị của biến quan sát.
- Trong __Time-series Data, có hai loại chính__.
    - Chuỗi thời gian thông thường (__regular time series__), loại thông thường được gọi là __số liệu__.
    - Chuỗi thời gian bất thường (__events__) là __những sự kiện__.

- Ứng dụng: Time-series data được ứng dụng rất rộng rãi trong các lĩnh vực:
```
    IoT
    DevOps
    Phân tích thời gian thực
    Dự báo kinh tế
    Tính toán doanh số bán hàng
    Phân tích lãi
    Phân tích thị trường
    Kiểm soát quy trình và chất lượng
    Phân tích điều tra
```

# 3. Time-series database
- Time-series database được tối ưu hóa để __thu thập, lưu trữ, truy xuất và xử lý dữ liệu time-series__. Ở đây chúng ta khảo sát ví dụ với InfluxDB    
- __InfluxDB được thiết kế để làm việc với dữ liệu chuỗi thời gian__. __Cơ sở dữ liệu SQL có thể xử lý chuỗi thời gian nhưng không được tạo ra cho mục đích đó__
- Nói tóm lại, __InfluxDB được thực hiện để lưu trữ một khối lượng dữ liệu chuỗi thời gian lớn và thực hiện phân tích theo thời gian về những dữ liệu đó một cách nhanh chóng__.

## 3.1. Thời gian là tất cả.
- Trong InfluxDB, __dấu thời gian xác định một điểm duy nhất trong bất kỳ chuỗi dữ liệu nhất định__.
- Điều này __giống như một bảng cơ sở dữ liệu SQL, nơi khoá chính__ được thiết lập trước bởi hệ thống và luôn luôn là thời gian.
- InfluxDB cũng nhận ra rằng sở thích graph của bạn có thể thay đổi theo thời gian. 
- Trong InfluxDB bạn không phải định nghĩa các lược đồ lên phía trước. Các điểm dữ liệu có thể có một trong các trường trên một phép đo, tất cả các trường trên phép đo hoặc bất kỳ số nào ở giữa. Bạn có thể thêm các trường mới vào một phép đo bằng cách viết một điểm cho trường mới đó.
- __Telegraf là một đại lý__ viết trong Go để __thu thập số liệu và viết chúng vào InfluxDB hoặc các đầu ra có thể khác__.
- __Chronograf là thành phần giao diện người dùng của InfluxData__. or use __Grafana__
- __kapacitor : Là công cụ tạo ra các cảnh báo hệ thống dựa trên một ngưỡng đã được đặt ra trước đó__.