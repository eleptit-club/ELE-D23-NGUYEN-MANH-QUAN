# TÌM HIỂU KỸ HƠN VỀ DHT
## DHT11
1.Giới thiệu về cảm biến DHT11

  <img width="713" height="649" alt="image" src="https://github.com/user-attachments/assets/a5ecc8be-aab4-4342-8cf1-e391b3b0cc23" />

- Cảm biến DHT11 là cảm biến tích hợp đo nhiệt độ và độ ẩm với đầu ra tín hiệu kỹ thuật số đã được hiệu chuẩn. Nhờ ứng dụng công nghệ cảm biến độc quyền cùng với vi điều khiển 8-bit tích hợp, DHT11 cung cấp:
  + Độ chính xác cao
  + Khả năng chống nhiễu tốt
  + Phản hồi nhanh
  + Hiệu quả về chi phí

- DHT11 là cảm biến đo nhiệt độ và độ ẩm với tín hiệu đầu ra kỹ thuật số đã được hiệu chuẩn. Cảm biến tích hợp:
  + Một điện trở cảm biến độ ẩm
  + Một nhiệt điện trở NTC đo nhiệt độ
  + Một vi điều khiển 8-bit để xử lý tín hiệu

- Ưu điểm chính
  + Độ chính xác cao, phản hồi nhanh, ổn định lâu dài
  + Giao tiếp một dây dễ lập trình, kết nối
  + Kích thước nhỏ gọn, tiêu thụ năng lượng thấp
  + Truyền tín hiệu xa đến 20 mét
  + 4 chân dễ kết nối, có thể tùy chỉnh đóng gói

- Ứng dụng: Thích hợp cho các hệ thống IoT, thiết bị đo môi trường, nhà thông minh,…

2. Thông số kỹ thuật:
- Thông số chi tiết:
  + Điện áp hoạt động: 3.5V đến 5.5V
  + Dòng hoạt động: 0,3mA (đo) 60uA (chế độ chờ)
  + Đầu ra: Dữ liệu nối tiếp
  + Phạm vi nhiệt độ: 0 ° C đến 50 ° C
  + Phạm vi độ ẩm: 20% đến 90%
  + Độ phân giải: Nhiệt độ và Độ ẩm đều là 16-bit
  + Độ chính xác: ± 1 ° C và ± 1%

- định dạng và sơ đồ chân
No:	Tên ghim	Mô tả
For DHT11 Sensor
  1	Vcc	Nguồn điện 3.5V đến 5.5V
  2	Dữ liệu	Đầu ra cả Nhiệt độ và Độ ẩm thông qua Dữ liệu nối tiếp
  3	NC	Không có kết nối và do đó không được sử dụng
  4	Ground	Kết nối với mặt đất của mạch
  
Đối với mô-đun cảm biến DHT11
  1	Vcc	Nguồn điện 3.5V đến 5.5V
  2	Data	Đầu ra cả Nhiệt độ và Độ ẩm thông qua Dữ liệu nối tiếp
  3	Ground	Kết nối với mặt đất của mạch

## DHT22

<img width="641" height="558" alt="image" src="https://github.com/user-attachments/assets/bb69360f-94a4-45ce-8e4e-acf577968b6d" />

1 Giới thiệu:
-Cả hai loại DHT11 và DHT22 đều là cảm biến đo nhiệt độ và độ ẩm. Đây là các cảm biến cực kỳ phổ biến với các anh em maker khi làm việc với các dự án liên quan đến nhiệt độ, độ ẩm:
Không	Tên ghim	Sự miêu tả
Đối với cảm biến DHT22
  1	Vcc	Nguồn điện 3.5V đến 5.5V
  2	Dữ liệu	Đầu ra cả Nhiệt độ và Độ ẩm thông qua Dữ liệu nối tiếp
  3	NC	Không có kết nối và do đó không được sử dụng
  4	Đất	Kết nối với mặt đất của mạch

Đối với mô-đun DHT22
  1	Vcc	Nguồn điện 3.5V đến 5.5V
  2	Dữ liệu	Đầu ra cả Nhiệt độ và Độ ẩm thông qua Dữ liệu nối tiếp
  3	Đất	Kết nối với mặt đất của mạch
   

- Thông số kỹ thuật DHT22
  + Điện áp hoạt động: 3.5V đến 5.5V
  + Dòng hoạt động: 0,3mA (đo) 60uA (chế độ chờ)
  + Đầu ra: Dữ liệu nối tiếp
  + Phạm vi nhiệt độ: -40 ° C đến 80 ° C
  + Phạm vi độ ẩm: 0% đến 100%
  + Độ phân giải: Nhiệt độ và Độ ẩm đều là 16-bit
  + Độ chính xác: ± 0,5 ° C và ± 1%

## so sánh
- Giống: Trong các cảm biến DHT11 / DHT22 này có sẵn các con chip, giúp chuyển đổi thành tín hiệu kỹ thuật số, cho phép chúng ta dễ dàng sử dụng hơn.
- Khác :
  + Tuy đều là đo nhiệt độ, nhưng cảm biến DHT22 ESP32 sẽ có độ phân giải cũng như phạm vi đo nhiệt độ độ ẩm cao hơn so với DHT11. Tuy nhiên, vì chất lượng tốt hơn nên giá thành của DHT22 sẽ hơi nhỉnh hơn đôi chút, và chúng ta chỉ có thể yêu cầu cảm biến này đọc thông tin trong khoản 2 giây.
  + Ngược lại, cảm biến DHT11 hỗ trợ chúng ta đọc thông tin mỗi giây, và chúng có chi phí rẻ hơn đôi chút.

<img width="912" height="484" alt="image" src="https://github.com/user-attachments/assets/d6c859f0-1f15-4449-a779-263404ac06a9" />

## cách kết nối 
-Chuẩn bị
  + ESP32
  + Cảm biến DHT11 / DHT22
  + Breadboard
  + Dây Jumper
-Kết nối:

<img width="588" height="704" alt="image" src="https://github.com/user-attachments/assets/eeafcf1f-32c8-4feb-9d31-eb378351b261" />

* Cài thư viện
- Bạn hãy truy cập vào Sketch > Include Library > Manage Libraries rồi tải về 2 thư viện sau nhé:
  + DHT library from Adafruit
  + Adafruit Unified Sensor library
* Nạp chương trình vào ESP32 thông qua cổng nạp

## link:
https://mecsu.vn/ho-tro-ky-thuat/dht11-cam-bien-nhiet-do-va-do-am.0j8
https://www.mouser.com/datasheet/2/758/DHT11-Technical-Data-Sheet-Translated-Version-1143054.pdf
https://mecsu.vn/ho-tro-ky-thuat/dht22-cam-bien-nhiet-do-va-do-am.vad

# RTOS
## Khái niệm:
- RTOS là hệ điều hành được thiết kế để xử lý các tác vụ trong thời gian thực, đảm bảo phản hồi nhanh, chính xác, không bị chậm trễ như các hệ điều hành thông thường.
- Hệ điều hành này được dùng trong các môi trường có nhiều sự kiện xảy ra liên tục, yêu cầu xử lý đúng thời hạn, thường chỉ trong phần mười giây hoặc ít hơn. Nếu xử lý không kịp thời, hệ thống có thể gặp lỗi.
- Khác với các OS như Windows hay Android, RTOS được tối ưu cho tác vụ chuyên biệt, đảm bảo thời gian xử lý ổn định, cách ly và xử lý lỗi hiệu quả.

## Cơ chế hoạt động và phân loại RTOS
- RTOS hoạt động dựa trên hai cơ chế là hướng sự kiện (event-driven) hoặc chia sẻ thời gian (time-sharing). Cơ chế hướng sự kiện sẽ giải quyết và điều phối các tác vụ (task) thông qua mức độ ưu tiên của chúng, còn cơ chế chia sẻ thời gian sẽ chuyển đối các tác vụ dựa trên phản ứng ngắt của xung nhịp. Phần lớn các hệ điều hành RTOS đều sử dụng giải thuật pre-emptive scheduling (tạm dịch là lập lịch trước).

## Nguyên lý hoạt động của RTOS
- RTOS hoạt động dựa trên hai cơ chế chính:
  + Hướng sự kiện (Event-driven): Ưu tiên xử lý các tác vụ theo mức độ ưu tiên, khi có sự kiện xảy ra.
  + Chia sẻ thời gian (Time-sharing): Luân phiên xử lý các tác vụ dựa trên ngắt định kỳ từ xung nhịp.

- Hầu hết RTOS hiện nay đều sử dụng thuật toán lập lịch ưu tiên có ngắt (pre-emptive scheduling), cho phép hệ thống ngắt tạm thời một tác vụ để chạy tác vụ có ưu tiên cao hơn.

<img width="769" height="504" alt="image" src="https://github.com/user-attachments/assets/0313f08e-7102-438c-98cb-f4685d45418b" />
 - Hệ điều hành RTOS thường được chia thành ba loại chính là:

1) Hard RTOS (Thời gian thực cứng):
  + Yêu cầu hoàn thành tác vụ đúng thời gian tuyệt đối
  + Nếu vượt quá thời gian → hệ thống lỗi

2) Soft RTOS (Thời gian thực mềm):
  + Cho phép sai số nhỏ trong thời gian xử lý
  + Tác vụ vẫn được chấp nhận nếu hoàn thành gần đúng thời hạn

3) Firm RTOS (Thời gian thực bền vững):
  + Thời gian giới hạn nghiêm ngặt, nhưng hệ thống vẫn đảm bảo tính ổn định, kể cả khi có một số trường hợp trễ nhỏ
  + Sai số không thường xuyên được chấp nhận nếu không ảnh hưởng lớn đến hệ thống
## Chức năng
- 3 Trạng thái mặc định:
  + Ready to run: Trạng thái chuẩn bị của tác vụ khi đã có đủ các tài nguyên để khởi chạy.
  + Running: Trạng thái tác vụ đang thực thi.
  + Blocked: Đây là trạng thái mà các tác vụ không đủ tài nguyên để xử lý sẽ được về trạng thái khóa
## ưu điểm
- Độ ổn định và tin cây cao, nên có thể hoạt động trong thời gian dài mà không cần quá nhiều sự can thiệp của con người.
- Hiệu suất tốt hơn cùng mức tiêu thụ bộ nhớ thấp nên không gây tiêu tốn quá nhiều tài nguyên hoặc RAM.
- RTOS gần như không có lỗi và nếu có xảy ra lỗi cũng dễ dàng phát hiện hơn.
- Có kích thước nhỏ và chi phí thấp.

## link
https://www.thegioididong.com/tin-tuc/he-dieu-hanh-rtos-la-gi-1404888

# Giao thức i2c
## Giới thiệu về giao tiếp I2C
-I2C là tên viết tắt của cụm từ tiếng anh “Inter-Integrated Circuit”. Nó là một giao thức giao tiếp được phát triển bởi Philips Semiconductors để truyền dữ liệu giữa một bộ xử lý trung tâm với nhiều IC trên cùng một board mạch chỉ sử dụng hai đường truyền tín hiệu.
- Do tính đơn giản của nó nên loại giao thức này được sử dụng rộng rãi cho giao tiếp giữa vi điều khiển và mảng cảm biến, các thiết bị hiển thị, thiết bị IoT, EEPROMs, v.v …
- Đây là một loại giao thức giao tiếp nối tiếp đồng bộ. Nó có nghĩa là các bit dữ liệu được truyền từng bit một theo các khoảng thời gian đều đặn được thiết lập bởi một tín hiệu đồng hồ tham chiếu.
