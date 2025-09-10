# IOT_01
*Chức năng
• Mở khóa cho người được phép vào nhà → Phân biệt được
người được phép/ko được phép vào nhà → Dùng cảm biến
vẫn tay, mã vạch, mã QR, thẻ RFID
• Có thể thêm/bớt người sử dụng → Có nút nhấn thêm/xóa user
• Lưu danh sách người sử dụng > Lưu dữ liệu vô EEPROM
• Khóa/mở khóa tự động → Dùng khóa điện từ (Solenoid)
• Phát hiện rung động mạnh > Cảm biến gia tốc, cảm biến rung
Cảnh báo đột nhập trái phép > Dùng âm thanh, gửi trạng thái
vào/ra/cảnh báo đột nhập về điện thoại qua mạng Internet.

1. Nguồn cấp

12VDC Input: nguồn vào chính 12V.

12V → 5V Regulator: hạ áp từ 12V xuống 5V.

5V → 3.3V Regulator: hạ từ 5V xuống 3.3V cho các module chỉ chạy 3.3V.

Từ đó tạo ra các mức điện áp:

5V: cấp cho ATmega328P và các module 5V.

3.3V: cấp cho RFID RC522, ESP8266, cảm biến I2C.

12V: cấp cho khóa điện tử (solenoid lock), còi báo công suất lớn.

2. Vi điều khiển ATmega328P

Là bộ xử lý trung tâm.

Giao tiếp với nhiều thiết bị qua:

SPI → RFID RC522.

I2C → Cảm biến (module I2C bên trên, ví dụ MPU6050 hoặc RTC).

UART (Hardware & Software) → ESP8266 (WiFi module), CH340 (nạp code và debug).

GPIO → Nút nhấn, LED, buzzer, relay, khóa điện.

3. Các thiết bị ngoại vi

RC522 (RFID): Đọc thẻ RFID (3.3V, SPI).

ESP8266 WiFi Module: Giao tiếp Internet (3.3V, UART).

Cảm biến (I2C): Có thể là MPU6050 (cảm biến gia tốc + con quay) hoặc DS3231 (RTC).

Relay Module (5V): Điều khiển tải công suất (quạt, còi 12V, khóa điện).

Nút nhấn (Xóa / Thêm): Dùng để thêm hoặc xóa thẻ RFID.

LED hai màu (Bicolor LED): Hiển thị trạng thái.

Buzzer: Báo âm thanh.

Còi + Khóa điện 12V: Thiết bị chấp hành.

4. Giao tiếp với máy tính

CH340 USB-UART: Cổng USB mini để nạp code cho ATmega328P và ESP8266

Switch: Chuyển đổi UART giữa ESP8266 và USB để nạp code/ giao tiếp.

5. Chức năng tổng thể của bo mạch

👉 Đây là một bo mạch điều khiển hệ thống khóa cửa thông minh qua RFID + WiFi:

Người dùng quét thẻ RFID (RC522).

ATmega328P kiểm tra thẻ trong bộ nhớ.

Nếu hợp lệ → kích relay mở khóa điện tử 12V, đồng thời phát tín hiệu LED/buzzer.

Nếu không hợp lệ → còi hú báo động.

ESP8266 có thể gửi dữ liệu mở cửa lên server/web để giám sát.

Có nút nhấn Thêm/Xóa để quản lý thẻ RFID trực tiếp trên mạch.
<img width="871" height="624" alt="image" src="https://github.com/user-attachments/assets/1090b46f-5fb3-4a0e-9181-fb71622d9ae0" />
