# Threat Model - Lab 6 AES-CBC Socket

## Thông tin nhóm

- Thành viên 1: Ma Huy Vũ
- Thành viên 2: Phạm Huy Hoàng

## Assets

Các tài sản cần bảo vệ gồm:
- Plaintext
- AES key
- AES IV
- Ciphertext
- File input/output
- Log hệ thống

## Attacker model

Kẻ tấn công có thể nghe lén mạng LAN, bắt gói tin TCP, sửa ciphertext, replay packet cũ hoặc đọc file log nếu hệ thống lưu log không an toàn.

## Threats

- Key disclosure do key và IV được gửi plaintext qua key channel.
- Tampering do ciphertext có thể bị sửa khi truyền.
- Replay attack do packet cũ có thể được gửi lại nhiều lần.
- Log leakage nếu AES key bị ghi vào log.
- Receiver không xác thực danh tính Sender.

## Mitigations

- Không gửi key plaintext trong hệ thống thật.
- Sử dụng TLS hoặc giao thức trao đổi khóa an toàn.
- Dùng AES-GCM để xác thực dữ liệu.
- Không ghi key thật vào log production.
- Thêm nonce hoặc timestamp để chống replay.
- Thêm cơ chế xác thực Sender.

## Residual risks

Hệ thống vẫn chưa hoàn toàn an toàn vì key channel chỉ là mô phỏng học tập. Chưa có TLS, chưa có xác thực hai chiều và chưa chống replay hoàn chỉnh.