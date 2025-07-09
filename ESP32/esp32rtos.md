# Tìm hiểu về ESP32 RTOS
## 1. Giới thiệu chung

Khái niệm:
  - ESP32 RTOS (Real-Time Operating System) là một nền tảng phần mềm được sử dụng để phát triển các ứng dụng nhúng thời gian thực trên vi điều khiển ESP32 do Espressif Systems phát triển. Dưới đây là phần giới thiệu tổng quan:
  - ESP32 RTOS là gì:ESP32 RTOS thường đề cập đến ESP-IDF (Espressif IoT Development Framework) – bộ SDK chính thức để lập trình ESP32. ESP-IDF sử dụng FreeRTOS làm nhân hệ điều hành thời gian thực (RTOS), cho phép lập trình đa luồng, quản lý tài nguyên hiệu quả và đồng bộ hóa các tác vụ trong các ứng dụng IoT phức tạp.

Đặc điểm:
 
  - Nhân FreRTOS: 
    + Cho phép chạy nhiều tác vụ(tasks) song song
    + Hỗ trợ đồng bộ hóa các primitive như semaphore, mutex, queue.
  
  - Hỗ trợ Wi-fi, blutooth
  
  - Thư viện phong phú
  
  - Tổ chức chương trình theo mô-đun
  
  - Giao tiếp song song

## 2. Các linh kiện
  -esp32: 
  
  ![image](https://github.com/user-attachments/assets/d682cb36-d40f-402d-8548-9a60e64455fb)
  ![image](https://github.com/user-attachments/assets/17ccece8-9c49-41ff-88da-88c304068398)

  -HDT11/HDT22:
    HDT11:
  
  ![image](https://github.com/user-attachments/assets/773db73c-2b86-4c59-bc20-473517af214d)

  
    + Cảm biến DHT11 đã được tích hợp trong một mạch duy nhất, bạn chỉ việc nối dây nguồn (Vcc, GND) và dây tín hiệu (Signal) vào mạch Arduino là xong.
   
    + thông số:
      Nguồn điện 3,5v đến 5v
      Mức tiêu thụ hiện tại 2,5mA
      Tín hiệu đầu ra kỹ thuật số
      Phạm vi nhiệt độ từ 0ºC đến 50ºC
      Độ chính xác để đo nhiệt độ ở 25ºC, dao động khoảng 2ºC
      Độ phân giải để đo nhiệt độ là 8-bit, 1ºC
      Độ ẩm có thể đo từ 20% RH đến 90% RH
      Độ ẩm chính xác 5% RH cho nhiệt độ từ 0-50ºC
      Độ phân giải là 1% RH, nó không thể nhận các biến thể dưới mức đó
    
    + El DHT11 là một cảm biến đơn giản để đo nhiệt độ và độ ẩm, tất cả hợp lại thành một. A) Có bạn sẽ không phải mua hai cảm biến riêng biệt. Giá của nó là khoảng € 2, vì vậy nó khá rẻ, mặc dù bạn cũng có thể tìm thấy nó được gắn trên một mô-đun (gắn trên PCB để dễ sử dụng) như thường thấy trong loại linh kiện điện tử này cho Arduino. Trong trường hợp của bo mạch, nó bao gồm một điện trở kéo lên 5 kilo ohm và một đèn LED cảnh báo chúng tôi về hoạt động.
    
    + DHT11 có độ tin cậy và độ ổn định cao do tín hiệu kỹ thuật số được hiệu chỉnh. Ngoài ra, nếu bạn nhìn vào biểu dữ liệu của nó, bạn sẽ thấy rằng nó có các tính năng thú vị, như bạn sẽ thấy trong các phần sau.
 
   DHT22:
   + Nó cũng là một cảm biến nhiệt độ và độ ẩm tích hợp, nhưng trong trường hợp này, giá của nó cao hơn một chút, khoảng € 4. Độ chính xác để đo nhiệt độ là biến thiên 5% cũng giống như DHT11, nhưng không giống như nó, nó đo ngoài phạm vi độ ẩm từ 20 đến 80%. Do đó, bạn có thể quan tâm đến DHT22 cho các dự án cần đo độ ẩm từ 0 đến 100%.

   ![image](https://github.com/user-attachments/assets/6cb1bd4e-b576-4768-8f02-56731e5190cf)
    * sơ đồ chân:
    ![image](https://github.com/user-attachments/assets/7f21b3fa-6346-426f-9c03-70c3ddae2eec)

    * La tần suất thu thập dữ liệu nó cũng gấp đôi so với DHT11, trong DHT22 2 mẫu được lấy mỗi giây thay vì 1 mẫu mỗi giây của DHT11. Đối với nhiệt độ, nó có thể đo từ -40ºC đến + 125ºC với độ chính xác cao hơn, vì nó có thể đo các phần của độ, đặc biệt nó có thể đánh giá cao các biến thể cộng / trừ 0,5ºC.
- LCD 16x2 + i2c
  LCD 16x2:
  
 ![image](https://github.com/user-attachments/assets/5152961f-ea7d-42ec-82c1-1f1f12f249ee)

  + LCD 16×2 được sử dụng để hiển thị trạng thái hoặc các thông số.

    LCD 16×2 có 16 chân trong đó 8 chân dữ liệu (D0 – D7) và 3 chân điều khiển (RS, RW, EN).
    5 chân còn lại dùng để cấp nguồn và đèn nền cho LCD 16×2.
    Các chân điều khiển giúp ta dễ dàng cấu hình LCD ở chế độ lệnh hoặc chế độ dữ liệu.
    Chúng còn giúp ta cấu hình ở chế độ đọc hoặc ghi.

  + LCD 16×2 có thể sử dụng ở chế độ 4 bit hoặc 8 bit tùy theo ứng dụng ta đang làm.
  I2C:

![image](https://github.com/user-attachments/assets/007c7f39-2eab-4513-847e-a57f174fa6d7)

  giao tiếp i2c lcd
  
  ![image](https://github.com/user-attachments/assets/76e4883a-9513-4af7-a80a-a195e935239f)

## 3. kết hợp đọc nhiệt độ độ ẩm và xuất ra màn hình

![image](https://github.com/user-attachments/assets/e3c97f17-0052-4321-869d-dda89e878e20)

## 4. Khó khăn 
- thời gian gấp nên chưa tìm hiểu sâu, kỹ hơn
- đồ chưa về để có thể thử với mạch
 
