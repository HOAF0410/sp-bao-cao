# sp-bao-cao
các thành phần trong mạch: 
+ esp32 devkit v1
+ max4466 ( bỏ mic tạo dây kết nối với hydrophone )
+ sd card
+ button
+ hydrophone 
Nguyên lý hoạt động cơ bản:
  + đầu tiên nạp code cho mạch và đảm bảo kết nối đúng
  + ban đầu mạch ở trạng thái chờ
  + khi mạch esp32 được khởi động thì cũng thiết lập một access point( HTTP client )
  + khi ấn nút ( chân D33 ) thì sẽ bắt đầu ghi âm 
  + tín hiệu từ cảm biến đi vào chân D34 của esp32 ( I2S )
  + tín hiệu được đưa vào thẻ sd để lưu trữ ( dạng .wav )
  + truy cập vào IP của esp32 ( 198.162.4.1) sẽ hiển thị danh sách các file được ghi
  + ấn vào file để tải đoạn ghi về thiết bị
