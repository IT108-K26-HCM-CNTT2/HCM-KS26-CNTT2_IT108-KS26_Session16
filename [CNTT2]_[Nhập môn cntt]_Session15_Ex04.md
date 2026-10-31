# Tối ưu hóa Lưu trữ Dữ liệu Doanh nghiệp

## ***Phần 1:  Giải pháp kỹ thuật thiết lập Files On-Demand & Xử lý "bẫy" mạng trọ***

***1. Thiết lập tính năng Files On-Demand (Tệp theo nhu cầu)***

***Em sẽ sử dụng tính năng Files On-Demand (có sẵn trên OneDrive hoặc tính năng Stream files của Google Drive):***

- ***Cơ chế hoạt động:*** Khi cấu hình, toàn bộ 500GB cấu trúc thư mục và tên file video sẽ hiển thị đầy đủ trên File Explorer của máy tính, nhưng thực chất chúng chỉ là các "bản sao ảo" (chứa metadata, dung lượng thực trên ổ cứng lúc này bằng 0 hoặc chỉ vài KB).

- ***Trạng thái hiển thị:***

  - Icon đám mây: File đang ở trên Cloud, chưa tải về máy.
  - Icon tích xanh lá trong vòng tròn trắng: File đã từng được tải về xem và đang lưu tạm trên máy.
  - Icon tích xanh đặc: File được ghim cố định trên máy (Offline) để xem không cần mạng.

- ***Cách dùng:*** Khi nào cần check lại đoạn video camera nào, bọn em chỉ cần click đúp vào file đó, hệ thống sẽ tự động stream và tải file về máy để mở. Xem xong, có thể click chuột phải chọn "Free up space" (Giải phóng dung lượng) để xóa bản tải về trên máy, đưa file về trạng thái mây như cũ.  

***2. Cách vượt "bẫy" đường truyền nhà trọ và việc gập máy laptop***

**Bẫy nghẽn mạng nhà trọ (Bandwidth Throttling):**

  - **Vấn đề:** Úp nguyên cục 500GB dữ liệu video lên cloud bằng wifi trọ sẽ làm mạng giật lag tung tóe, thể nào cũng bị mấy đứa cùng xóm trọ sang "gõ cửa".

  - **Cách giải quyết:** Vào phần cài đặt (Settings) của ứng dụng đồng bộ, bật tính năng Giới hạn tốc độ tải lên/tải xuống (Network Bandwidth), bóp băng thông ở mức vừa phải (ví dụ tối đa 1-2 MB/s). Tốt nhất là hẹn giờ hoặc cắm máy chạy đồng bộ vào ban đêm lúc mọi người đã đi ngủ.

**Bẫy gập máy laptop bị đứt kết nối:**

- Vấn đề: Đang cho upload video qua đêm, sơ ý gập màn hình laptop lại để đi ngủ thì máy chuyển sang chế độ Sleep, ngắt kết nối Wi-Fi làm tiến trình đồng bộ bị đứt đoạn giữa chừng.

- Cách giải quyết: Vào Control Panel -> Power Options -> chọn Choose what closing the lid does, sau đó chỉnh mục When I close the lid thành "Do nothing" (Không làm gì cả) khi cắm sạc. Nhờ vậy, nhóm có thể gập màn hình laptop lại mà tiến trình upload 500GB dữ liệu vẫn chạy ngầm mượt mà qua đêm mà không lo treo máy hay ngắt mạng.

## ***Phần 2: Báo cáo dung lượng & Chứng minh hiệu quả***

Dạ đây, em xin gửi lại bảng so sánh dung lượng đã được chuyển sang định dạng Markdown cực kỳ gọn gàng và dễ nhìn đây ạ:

| Chỉ tiêu so sánh | Khi đồng bộ toàn bộ (Cách cũ - Lỗi) | Khi áp dụng Files On-Demand (Giải pháp mới) |
| --- | --- | --- |
| **Tổng dung lượng Cloud** | 500 GB | 500 GB |
| **Dung lượng ổ cứng Local SSD** | 256 GB (Thực tế trống khoảng 160 GB sau khi trừ Windows) | 256 GB (Thực tế trống khoảng 160 GB) |
| **Dung lượng chiếm dụng trên SSD** | **500 GB** (Vượt quá giới hạn phần cứng) | **~ 0 GB đến vài GB** (Chỉ chứa file metadata và file đang mở tạm thời) |
| **Trạng thái hoạt động** | **Tràn ổ cứng, sập phần mềm đồng bộ**

 | **Hoạt động ổn định, mượt mà, không lo quá tải** |

