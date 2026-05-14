# Report 1 page - Lab 6 AES-CBC Socket

## Thông tin nhóm

- Thành viên 1: Ma Huy Vũ
- Thành viên 2: Phạm Huy Hoàng

## Mục tiêu

Bài lab giúp sinh viên hiểu cách gửi và nhận dữ liệu mã hóa AES-CBC qua TCP socket. Hệ thống được chia thành hai kênh gồm key channel và data channel để mô phỏng quá trình truyền khóa và truyền ciphertext riêng biệt. Ngoài ra bài lab còn giúp hiểu về PKCS#7 padding, AES key, IV và cách xử lý dữ liệu nhị phân qua socket bằng Python. Sinh viên cũng được thực hành viết test và phân tích các điểm yếu bảo mật của hệ thống.

## Phân công thực hiện

- Thành viên 1 phụ trách Sender, AES encryption và logging.
- Thành viên 2 phụ trách Receiver, socket communication và decrypt.
- Cả hai cùng thực hiện testing, threat model và report.

## Cách làm

Hệ thống gồm hai chương trình là Sender và Receiver. Sender tạo AES key và IV ngẫu nhiên, sau đó mã hóa plaintext bằng AES-CBC với PKCS#7 padding. Key và IV được gửi qua KEY_PORT, còn ciphertext được gửi qua DATA_PORT.

Receiver lắng nghe hai cổng TCP riêng biệt để nhận key/IV và ciphertext. Sau khi nhận đầy đủ dữ liệu, Receiver giải mã ciphertext và ghi plaintext ra file output.

Dữ liệu truyền qua socket đều sử dụng length header 4 byte để đảm bảo đọc đúng số byte cần thiết.

## Kết quả

Chương trình chạy thành công trên môi trường local bằng Python. Sender gửi được ciphertext qua socket và Receiver giải mã chính xác plaintext ban đầu.

Các test đã thực hiện gồm:
- AES encrypt/decrypt test
- PKCS#7 padding test
- Socket transfer test
- Wrong key test
- Tampered ciphertext test

Log sender và receiver được lưu trong thư mục logs để minh chứng hoạt động của hệ thống.

## Kết luận

Bài lab giúp hiểu rõ quy trình truyền dữ liệu mã hóa AES-CBC qua socket TCP và cách xử lý dữ liệu nhị phân bằng Python.

Ngoài ra bài lab cũng cho thấy việc gửi key plaintext là không an toàn trong hệ thống thực tế. Trong tương lai có thể cải tiến bằng TLS, AES-GCM và cơ chế xác thực hai chiều.