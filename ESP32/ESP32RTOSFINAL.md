# Đề tài ESP32 RTOS

## 1. Giới thiệu
### 1.1 Tên bài tập
- Hệ thống thông minh sử dụng ESP32 và RTOS với 3 tác vụ đọc DHT, hiển thị lên LCD, Đọc độ ẩm đất
### 1.2 Mục tiêu
- Thiết kế và xây dựng một hệ thống nhúng có khả năng đo lường và giám sát độ ẩm đất cùng với nhiệt độ, độ ẩm không khí một cách tự động.
- Ứng dụng vi điều khiển ESP32 với khả năng Wi-Fi để xử lý dữ liệu từ cảm biến.
- Sử dụng hệ điều hành thời gian thực RTOS (Real-Time Operating System) để quản lý các tác vụ một cách hiệu quả, đảm bảo tính ổn định và phản hồi nhanh của hệ thống.
### 1.3 Các linh kiện
   #### ESP32 
<img width="224" height="251" alt="image" src="https://github.com/user-attachments/assets/38394e0f-0984-49ab-8e82-6b52c8041830" />
<img width="344" height="251" alt="image" src="https://github.com/user-attachments/assets/80a668db-9cd9-4249-bd00-30693eb7fb9b" />
<img width="338" height="251" alt="image" src="https://github.com/user-attachments/assets/79743009-104a-4943-bcd4-91a461456f27" />



 - ESP32 là một vi điều khiển (microcontroller) thế hệ mới của hãng Espressif Systems (Trung Quốc), được phát triển sau dòng ESP8266. Đây là một SoC (System on Chip) rất mạnh mẽ, tích hợp cả Wi-Fi và Bluetooth, nên được ứng dụng rộng rãi trong các dự án IoT, tự động hóa, robot, và hệ thống nhúng.

Cấu tạo: 
<img width="900" height="600" alt="image" src="https://github.com/user-attachments/assets/d0be59f4-cdd2-48de-81a5-b959686a6d7e" />
<img width="358" height="251" alt="image" src="https://github.com/user-attachments/assets/0abb6dda-1270-4ede-8859-8eecbc7d0d38" />


Tổng quan thông số:
- Kết nối không dây :
  - WiFi: Tốc độ dữ liệu lên đến 150Mbps với HT40
  - Bluetooth: Hỗ trợ BLE (Bluetooth Low Energy – Bluetooth năng lượng thấp) và Bluetooth Classic
  - Bộ xử lý: Chip vi xử lý LX6 32-bit Tensilica Xtensa Dual-Core, hoạt động ở tốc độ 160MHz hoặc 240MHz
- Bộ nhớ:
  - ROM:  448 KB (phục vụ cho việc khởi động và chạy các chức năng cốt lõi)
  - SRAM:  520 KB (dùng cho dữ liệu và hướng dẫn)
- Công suất: ESP32 cho phép bạn vẫn có thể sử dụng bộ chuyển đổi ADC, kể cả khi đang trong chế độ Deep Sleep.
  
- Hỗ trợ ngoại vi
  - Giao diện ngoại vi với DMA bao gồm cảm ứng điện dung
  - ADC (Bộ chuyển đổi Analog thành Digital, tên đây đủ là Analog to Digital Converter)
  - DACs (Bộ chuyển đổi Digital thành Analog, tên đây đủ là Digital to Analog Converter)
  - I2C (Inter Integrated Circuit)
  - UART (Universal Asynchronous Receiver/Transmitter)
  - SPI (Serial Peripheral Interface)
  - I2S (Integrated Interchip Sound)
  - RMII (Reduced Media-Independent Interface)
  - PWM (Pulse-Width Modulation)
- Bảo mật: Bộ tăng tốc phần cứng dành cho SSL/TLS và AES.
  
Ứng dụng thực tế
- Hệ thống nhà thông minh (điều khiển đèn, quạt, cảm biến môi trường).
- IoT Gateway: trung gian kết nối cảm biến → cloud (MQTT, HTTP, Firebase...).
- Các dự án điều khiển robot, drone.
- Thiết bị đo lường: nhiệt độ, độ ẩm, ánh sáng, đất (như trong đồ án bạn làm).
-  Wearable devices nhờ khả năng kết nối BLE.

####  Rtos 

- Định nghĩa: RTOS là viết tắt của cụm từ Real-time operating system hay hệ điều hành thời gian thực thường được nhúng trong các dòng vi điều khiển dùng để điều khiển thiết bị một cách nhanh chóng và đa nhiệm (multi tasking). Để hiểu rõ ràng nó là gì trước hết hãy làm rõ khái niệm về hệ điều hành đã.
- Cách hoạt động: RTOS là một phân đoạn hoặc một phần của chương trình, trong đó nó giải quyết việc điều phối các task, lập lịch và phân mức ưu tiên cho task, nắm bắt các thông điệp gửi đi từ task.
  
<img width="1400" height="637" alt="image" src="https://github.com/user-attachments/assets/8aa7a988-96b2-4802-9b58-1f85900b0f18" />
<img width="605" height="340" alt="image" src="https://github.com/user-attachments/assets/c7877624-7b8d-47e4-9313-21bc98239b8c" />
  - RUNNING: đang thực thi
  - READY: sẵn sàng để thực hiện
  - WAITING: chờ sự kiện
  - INACTIVE: không được kích hoạt
    
#### Cảm biến độ ẩm đất
<img width="292" height="251" alt="image" src="https://github.com/user-attachments/assets/83636022-7a41-4d3c-b7ff-454319860708" />
<img width="259" height="259" alt="image" src="https://github.com/user-attachments/assets/d656be15-1842-436a-9a8f-d62f541f8ba8" />


- cách hoạt động: Nguyên lý cảm biến độ ẩm đất dựa trên sự tương tác giữa đất và điện trở. Khi đất ẩm, nước trong đất sẽ làm tăng khả năng dẫn điện của đất. Cảm biến độ ẩm đất sử dụng hai đầu cảm biến hoặc điện cực để đo điện trở của môi trường đất.
<img width="323" height="346" alt="image" src="https://github.com/user-attachments/assets/e6add904-6a9e-4bdd-8422-818d76b6f404" />

- Tổng quan:
 - Đầu cảm biến: Đầu cảm biến là phần tiếp xúc trực tiếp với đất để đo độ ẩm. Thường là hai đầu kim loại không rỉ như thép không gỉ hoặc đồng được chìm vào đất. Hai đầu kim loại này tạo ra một không gian tiếp xúc với đất, cho phép nước trong đất tương tác với chúng.
   <img width="392" height="117" alt="image" src="https://github.com/user-attachments/assets/d9266713-c74d-4568-9c89-9f7abfdb39ee" />

  - Module: Module cảm biến độ ẩm đất sử dụng một mạch so sánh LM393 để so sánh tín hiệu đầu ra từ bộ điện cực với một ngưỡng (threshold). Khi độ ẩm của đất vượt qua ngưỡng đã được cài đặt, mạch so sánh sẽ tạo ra tín hiệu đầu ra để biểu thị trạng thái độ ẩm của đất.
    <img width="309" height="216" alt="image" src="https://github.com/user-attachments/assets/4046f2e7-e5cc-4215-8675-d86fdd226ca3" />

  - Để module hoạt động, thông thường nó sẽ được cung cấp nguồn điện DC từ 3.3V đến 5V. Có thể lấy trực tiếp từ board Arduino
    
- Sơ đồ chân:
<img width="366" height="475" alt="image" src="https://github.com/user-attachments/assets/1b63e9c1-77ee-4608-901a-f77d193972a4" />

  - VCC: Chân cung cấp nguồn cho cảm biến (thường là 3.3V hoặc 5V).
  - GND: Chân đất (Ground).
  - AO (Analog Output): Chân đầu ra analog, cung cấp tín hiệu analog tương ứng với độ ẩm của đất.
  - DO (Digital Output): Chân đầu ra Digital, tạo ra tín hiệu số để biểu thị trạng thái độ ẩm của đất.

#### DHT11
<img width="576" height="576" alt="image" src="https://github.com/user-attachments/assets/87f27b57-b4f9-4e94-b29b-53db2c15f8b8" />
https://dientutuonglai.com/uploads/product/module-va-cam-bien-/cam-bien-cac-loai-/6102--cam-bien-do-am/ha-6102---014.jpg
- Tính năng: Cảm Biến Nhiệt Độ Và Độ Ẩm DHT11 là cảm biến rất thông dụng hiện nay vì chi phí rẻ và rất dễ lấy dữ liệu thông qua giao tiếp 1 wire (giao tiếp digital 1 dây truyền dữ liệu duy nhất). Bộ tiền xử lý tín hiệu tích hợp trong cảm biến giúp bạn có được dữ liệu chính xác mà không phải qua bất kỳ tính toán nào. So với cảm biến đời mới hơn là DHT22 thì DHT11 cho khoảng đo và độ chính xác kém hơn rất nhiều.
- sơ đồ chân:
  
- Thông số:
  - Điện áp hoạt động: 3V - 5V DC
  - Dòng điện tiêu thụ: 2.5mA
  - Phạm vi cảm biến độ ẩm: 20% - 90% RH, sai số ±5%RH
  - Phạm vi cảm biến nhiệt độ: 0°C ~ 50°C, sai số ±2°C
  - Tần số lấy mẫu tối đa: 1Hz (1 giây 1 lần)
  - Kích thước: 23 * 12 * 5 mm
- Ứng dụng:
  - Đo nhiệt độ và độ ẩm
  - Trạm thời tiết cục bộ
  - Kiểm soát khí hậu tự động
  - Giám sát môi trường
  - 
#### LCD + I2C
 LCD 6x2	
<img width="1024" height="768" alt="image" src="https://github.com/user-attachments/assets/c4b77fad-e8c4-49b1-885b-5c4947096016" />

- Thông số:
  - LCD 16×2 có 16 chân trong đó 8 chân dữ liệu (D0 – D7) và 3 chân điều khiển (RS, RW, EN).
  - 5 chân còn lại dùng để cấp nguồn và đèn nền cho LCD 16×2.
  - Các chân điều khiển giúp ta dễ dàng cấu hình LCD ở chế độ lệnh hoặc chế độ dữ liệu.
  - Chúng còn giúp ta cấu hình ở chế độ đọc hoặc ghi.
    
Module I2C Arduinp
<img width="640" height="476" alt="image" src="https://github.com/user-attachments/assets/bb8c4345-02e9-409b-a331-46aa0231ad6c" />

- Thay vì phải mất 6 chân vi điều khiển để kết nối với LCD 16×2 (RS, EN, D7, D6, D5 và D4) thì module IC2 bạn chỉ cần tốn 2 chân (SCL, SDA) để kết nối.
- Module I2C hỗ trợ các loại LCD sử dụng driver HD44780(LCD 16×2, LCD 20×4, …) và tương thích với hầu hết các vi điều khiển hiện nay.
  
## 2. Phần cứng và Phần mềm

### 2.1 Sơ đồ khối hệ thống
- Bộ xử lý trung tâm (Central Processing Unit): Mạch phát triển ESP32, đóng vai trò là "bộ não" của hệ thống, xử lý tất cả các tác vụ.
- Cảm biến (Sensors):
  - Cảm biến độ ẩm đất: Đo lường mức nước trong đất.
   - Cảm biến DHT11: Đo nhiệt độ và độ ẩm không khí.
- Mô-đun giao tiếp (Communication Module): Wi-Fi tích hợp trên ESP32, cho phép truyền dữ liệu.
- 
### 2.2 Danh sách linh kiện
- 1 x Mạch phát triển ESP32
- 1 x Cảm biến độ ẩm đất (loại analog)
- 1 x Cảm biến DHT11
- Dây nối (jumper wires)
- Mạch test board (breadboard)
- 1 x Cáp micro USB
  
## 3. Lắp ráp và Lập trình

### 3.1 Sơ đồ kết nối phần cứng

- Kết nối ESP32 với Boat:
  <img width="1536" height="2048" alt="image" src="https://github.com/user-attachments/assets/462ddae9-f44f-42c9-9826-e8c3c660d882" />

- Kết Nối LCD I2C → ESP32:
  <img width="1536" height="2048" alt="image" src="https://github.com/user-attachments/assets/89faea35-c9e5-48fb-8888-638bcd3206f4" />

  - VCC  → 5V
  - GND  → GND
  - SDA  → GPIO21
  - SCL  → GPIO22
- Kết nối Cảm biến Độ ẩm đất  → ESP32:
  <img width="1536" height="2048" alt="image" src="https://github.com/user-attachments/assets/83eda2ab-b00d-4738-a441-81740adf8724" />

  - VCC   → 5V
  - GND   → GND
  - AOUT  → GPIO34 (ADC)
  - DOUT  → Không nối (nếu không dùng ngưỡng cảnh báo)
- Kết nối Cảm biến DHT11 → ESP32:
 <img width="1536" height="2048" alt="image" src="https://github.com/user-attachments/assets/c5cf8979-5143-4071-97df-bf2933873980" />

  - Chân 1 (GND)  → GND ESP32
  - Chân 2 (DATA) → GPIO4
  - Chân 3 (NC)   → Không nối
  - Chân 4 (VCC)  → 3.3V
Tổng kết
<img width="1536" height="2048" alt="image" src="https://github.com/user-attachments/assets/a7a4d6c4-6290-4d60-87f0-1138edcdb2fe" />

### 3.2 Lập trình với RTOS
- Sử dụng FreeRTOS, một hệ điều hành thời gian thực được tích hợp sẵn trong ESP-IDF (môi trường lập trình cho ESP32), để quản lý các tác vụ.
#### 3.2.1 Giải thích code 
- Khởi tạo đối tượng
  - DHT dht(DHTPIN, DHTTYPE);
  - LiquidCrystal_I2C lcd(LCD_ADDR, 16, 2);
  - // khởi tạo để đọc cảm biến dht và lcd

  -  typedef struct {
    - float temperature;
    - float humidity;
    -  int soilMoisture; 
  - } SensorData_t;
  - // khai báo 3 giá trị hiểm thị sau là 
    - T nhiệt độ không khí
    - H là độ ẩm không khí
    - Soil là độ ẩm đất
      
- Task 1: đọc DHT11
  - Đọc nhiệt độ và độ ẩm từ DHT11.
  - Nếu dữ liệu hợp lệ (!isnan), gửi vào Queue.
  - Chờ 2 giây rồi lặp lại.
<img width="585" height="429" alt="image" src="https://github.com/user-attachments/assets/d32a7b93-b4ef-4dd6-8b9a-578d56f3071d" />

- Task 2: Đọc cảm biến đất
  - Đọc giá trị ADC từ chân soil (0–4095).
  - Dùng map() để chuyển đổi thành % độ ẩm đất.
  - Cập nhật dữ liệu vào Queue.
  - Chạy lại sau 1 giây.
<img width="737" height="341" alt="image" src="https://github.com/user-attachments/assets/ceeaaf73-a098-4cd8-8308-8ee5a5a0a858" />

- Task 3: hiển thị LCD
  - Lấy dữ liệu từ Queue.
  - Xóa màn hình và in:
    - Dòng 1: nhiệt độ (°C) và độ ẩm không khí (%)
    - Dòng 2: độ ẩm đất (%)
  - Cập nhật lại mỗi 1 giây.
<img width="588" height="509" alt="image" src="https://github.com/user-attachments/assets/9d5c23cf-f496-4a6a-90c6-c636578e6be6" />

## 4. Kết quả và Đánh giá
### 4.1 Kết quả đạt được
- Hệ thống hoạt động ổn định, có khả năng đo lường chính xác các thông số môi trường.
- Dữ liệu được cập nhật định kỳ trên màn hình Serial, chứng tỏ các tác vụ đang chạy song song hiệu quả.
### 4.2 Đánh giá
- Ưu điểm: Việc sử dụng RTOS giúp hệ thống có tính phản hồi nhanh và xử lý đa tác vụ hiệu quả, tránh được hiện tượng treo khi một tác vụ bị tắc nghẽn. Chi phí thấp, dễ dàng mở rộng.
- Nhược điểm: DHT11 có độ chính xác không cao, có thể thay thế bằng DHT22. Phiên bản hiện tại chưa có giao diện người dùng trực quan.
  
## 5. Tài liệu tham khảo
- https://chotroihn.vn/cam-bien-do-am-dat-bang-dien-dung-dau-ra-analog
- https://arduinokit.vn/su-dung-cam-bien-do-am-dat-soil-moisture-sensor-voi-arduino/
- https://arduinokit.vn/giao-tiep-i2c-lcd-arduino/
- https://www.iotzone.vn/esp32/esp32-co-ban/gioi-thieu-esp32-la-gi/
- https://dientutuonglai.com/cam-bien-nhiet-do-va-do-am-dht11.html
- https://khuenguyencreator.com/tong-quan-ve-he-dieu-hanh-thoi-gian-thuc-rtos/
- ChatGPT+ Copilot
