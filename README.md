# sp-bao-cao
Các thành phần trong mạch: 
+ esp32 devkit v1
+ max4466 ( bỏ mic tạo dây kết nối với hydrophone )
+ sd card
+ button
+ hydrophone


Tổng Quan Luồng Tín Hiệu:
Hydrophone ➔ Bộ khuếch đại ➔ ESP32 ADC (qua I2S) ➔ Bộ nhớ SD/Truyền qua Web

Nguyên lý hoạt động cơ bản:
  + đầu tiên nạp code cho mạch và đảm bảo kết nối đúng
  + ban đầu mạch ở trạng thái chờ
  + khi mạch esp32 được khởi động thì cũng thiết lập một access point( HTTP client )
  + khi ấn nút ( chân D33 ) thì sẽ bắt đầu ghi âm 
  + tín hiệu từ cảm biến đi vào chân D34 của esp32 ( I2S )
  + tín hiệu được đưa vào thẻ sd để lưu trữ ( dạng .wav )
  + truy cập vào IP của esp32 ( 192.168.4.1) sẽ hiển thị danh sách các file được ghi
  + ấn vào file để tải đoạn ghi về thiết bị
# XỬ LÝ NHIỄU TÍN HIỆU ĐẢM BẢO ÂM THANH CHÂN THỰC TỪ MÔI TRƯỜNG
  + Dùng Max4466 để khuyếch đại từ eps32 đảm bảo tín hiệu không quá bé ( lưu ý chỉnh chiết áp cho phù hợp ) 
  + Điều chỉnh điện áp đầu vào  : ADC của ESP32 hoạt động với điện áp đầu vào từ 0 đến 3.3V, 
  cần đảm bảo rằng tín hiệu từ hydrophone được điều chỉnh trong khoảng này. Bộ khuếch đại có thể thêm điện áp "offset" để tín hiệu luôn nằm trong giới hạn này.
  + giới hạn tần số : giới hạn lại phạm vi cần thu âm để đảm bảo hiệu quả thu 
  + Tăng tần số lấy mẫu ít nhất trên 44,1 kHz
  + thêm một tụ lọc nhiễu dòng ở giữa chân 3,3 và 0 V ( cỡ 100 microF ), tách riêng nguồn và GND độc lập tránh nhiễu do nguồn
