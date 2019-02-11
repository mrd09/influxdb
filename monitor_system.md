# Monitoring System (Phần 1)
## Khái niệm
- Monitoring system là một hệ thống theo dõi, ghi lại các trạng thái, hoạt động của máy tính hay ứng dụng một cách liên tục.

## Tại sao chúng ta cần Monitoring system?
- Dựa vào kết quả của hệ thống monitoring chúng ta có thể điêù chỉnh việc sử dụng tài nguyên (cpu, ram, disk, ...) sao cho phù hợp
- Ngăn chặn các sự cố có thể xảy ra, nếu có xảy ra chúng ta cũng có thể phát hiện sớm hơn
- Giảm thiểu thời gian quản lý hệ thống

## Các đặc điểm của một hệ thống monitoring
- Xử lí real time
- Có hệ thống cảnh báo
- Visualization
- Có khả năng tạo reports
- Có khả năng cài cắm các plugins

### Thành phần
- Thông thường một hệ thống monitoring thường có 4 thành phần chính:
```
Collector1             --> Visualizer
             ---> DB 
Collector2             --> Alerter
                                       --> Gateway
```

- __Collector__: Được __cài trên các máy agent (các máy muốn monitor)__, có nhiệm vụ __collect metrics của host và gửi về database__. Ví dụ: Cadvisor, Telegraf, Beat..
- __Database__: __Lưu trữ các metrics mà colletor thu thập được__, thường thì chúng ta sẽ __sử dụng các time series database__. Ví dụ ElasticSearch, InfluxDB, Prometheus, Graphite (Whisper)
- __Visualizer__: Có nhiệm vụ trực quan hóa các metrics thu thập được qua các biểu đồ, bảng, .... Ví dụ: Kibana, Grafana, Chronograf
- __Alerter__: __Gửi thống báo đến cho sysadmin khi có sự cố__ xảy ra
- Có rất nhiều stack phổ biến như:
```
• Logstash - Elasticsearch - Kibana
• Prometheus - Node Exporter - Grafana
• Telegraf - InfluxDB - Grafana
```

### Telegraf va Influxdb
- Telegraf và Influxdb đều là sản phẩm của InfluxData, cả hai đều mà mã nguồn mở và được viết bởi Go. 
- Mặc dù InfluxData cung cấp một stack hoàn chỉnh để monitor với Chronograf để visualize và Kapacitor để alerting (TICK stack) nhưng __chúng ta có thể sử dụng Grafana để thay thế cho cả Chronograf lẫn Kapacitor__.

#### Telegraf
https://www.influxdata.com/time-series-platform/telegraf/

- __Telegraf__ là một __agent để collecting và reporting metrics__ và data được viết bởi Go.
- Nó có thể tích hợp để collect nhiều loại nguồn dữ liệu khác nhau của metrics, events, và logs trực tiếp từ containers và system mà nó chạy trên đó. 
    - Nó cũng có thể pull metrics từ các third-party APIs, Kafka. 
    - Nó cũng có nhiều output plugin để gửi metrics thu thập được tới nhiều dạng datastores, services, message queues khác nhau như  InfluxDB, Graphite, OpenTSDB, Datadog, Librato, Kafka, ...

#### InfluxDB

https://www.influxdata.com/time-series-platform/influxdb/

- InfluxDB là một __Time Series Database__ (là __database được tối ưu hóa để xử lý dữ liệu chuỗi thời gian__, các __dãy số được lập chỉ mục theo thời gian__.)
- InfluxDB được sử dụng để lưu các dữ liệu cho các trường hợp liên quan đến một lượng lớn __time-stamped data__, bao gồm __DevOps monitoring, log data, application metrics, IoT sensor data, và real-time analytics__. 
- Nó có thể tự động xóa các dữ liệu cũ, không cần thiết và cung cấp một ngôn ngữ giống SQL để tương tác với dữ liệu.
- Data trong InfluxDB được tổ chức dưới dạng time series. Time series có thể có một hoặc nhiều points, mỗi __point là một mẫu rời rạc các số liệu__. Point gồm:
    • __Time__ (timestamp)
    • Một __measurement (ví dụ "cpu_load")__
    • Ít nhất một __key-value field (giá trị đo được, ví dụ "value=0.64", hoặc "temperature=21.2")__
    • __Không hoặc nhiều key-value tags chứa metadata của value (ví dụ “host=server01”, “region=EMEA”, “dc=Frankfurt”)__

    - Chúng ta có thể xem __measurement như là table trong sql có primary index luôn là time. tags và field là columns của table, tags được index còn field thì không__. 
    - Điểm khác biệt ở đây là __InfluxDB có thể có hàng triệu measurements, chúng ta không cần định nghĩa schemas trước__ và giá trị null không được lưu trữ.