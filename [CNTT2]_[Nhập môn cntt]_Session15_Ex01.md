#  Hệ thống Quản lý Tài liệu Dự án Doanh nghiệp

## ***PHẦN 1: Báo cáo phân tích luồng dữ liệu & Xử lý xung đột phiên bản***

***1. Sơ đồ luồng dữ liệu từ Local SSD lên Cloud (Hybrid Workflow)***

- Khi bạn A thực hiện thiết kế 3D và tiến hành lưu file, luồng dữ liệu diễn ra qua các bước cốt lõi sau:

  - Bước 1 (Ghi local): Bạn A nhấn Ctrl + S trong phần mềm thiết kế, hệ điều hành ngay lập tức ghi đè dữ liệu mới nhất xuống ổ cứng SSD cục bộ (Local Storage) để đảm bảo tốc độ render và thao tác mượt mà không bị giật lag.

  - Bước 2 (Kiểm trạm ngầm): Tiến trình ngầm của ứng dụng đồng bộ đám mây (như Google Drive, OneDrive) liên tục quét (watch) sự thay đổi của thư mục dự án. Ngay khi phát hiện file có thời gian chỉnh sửa mới, nó sẽ tự động đưa vào hàng đợi.

  ***2. Cách hệ thống xử lý khi có xung đột phiên bản (File Version Conflict)***

  - Nguyên nhân: Xảy ra khi bạn A và một thành viên khác trong nhóm cùng sửa một file thiết kế 3D trong lúc mất mạng, sau đó đồng thời đẩy lên Cloud.

  - Hệ thống xử lý: Để tránh việc ghi đè làm mất sạch công sức của một trong hai người, hệ thống Cloud sẽ giữ nguyên bản gốc và tự động sinh ra một bản sao lưu phụ mang tên xung đột (ví dụ: model_conflict_copy.obj).

  - Cách giải quyết: Hệ thống gửi thông báo cảnh báo. Designer chỉ cần mở cả hai file lên đối chiếu, gộp các chi tiết chuẩn rồi lưu lại một bản duy nhất.

  ## ***PHẦN 2: Giải quyết "Bẫy dữ liệu" (Mất kết nối Internet hoặc sập nguồn đột ngột)***

  - Bẫy dữ liệu: Đang thiết kế dở thì máy tính bị sập nguồn đột ngột hoặc mất Wi-Fi, liệu dữ liệu có bị đứt đoạt đồng bộ không?

  - Cách phòng thủ và xử lý:

    - Khi máy mất mạng hoặc sập nguồn giữa chừng, tiến trình đồng bộ lên mây sẽ tạm thời bị ngưng trệ, biểu tượng file sẽ chuyển sang vòng xoay hoặc chấm than lỗi đồng bộ.

    - Tuy nhiên, nhờ đã nhấn Ctrl + S từ trước, toàn bộ phần việc vừa làm đã nằm chắc chắn trên ổ cứng Local SSD của máy. Ngay khi máy khởi động lại và kết nối lại Internet, ứng dụng Cloud sẽ tự động tiếp tục tiến trình đồng bộ phần dữ liệu đang dở dang đó lên mây mà không hề bị mất mát gì cả.

## ***PHẦN 3: Quy trình thực thi chuẩn dành cho Designer***

***Bước 1: Cài đặt ứng dụng đồng bộ đám mây và bật Files On-Demand***

- Tải phần mềm Cloud (Google Drive for Desktop/OneDrive). Kích hoạt ngay tính năng Files On-Demand để các file thiết kế 3D nặng hàng GB chỉ chiếm dung lượng ảo trên máy, giúp tiết kiệm tối đa ổ cứng SSD mà vẫn mở dựng hình ngon lành.

***Bước 2: Đưa thư mục dự án vào không gian đồng bộ***

- Toàn bộ thư mục chứa source file 3D của dự án "Số hóa Bảo tàng PTIT" phải được đặt nằm gọn bên trong thư mục quản lý của đám mây. Đồng thời loại trừ các file cache render nặng để tránh nghẽn mạng.

***Bước 3: Tạo thói quen check "Tích xanh" và dùng Version History***

- Tập thói quen nhìn xuống khay hệ thống kiểm tra chữ Up to date hoặc icon tích xanh trước khi gập máy ra về.

- Nếu lỡ tay xóa nhầm chi tiết hoặc file bị lỗi, tuyệt đối không hoảng loạn; chỉ cần chuột phải vào file trên Cloud, chọn Version History (Lịch sử phiên bản) và chọn mốc thời gian hôm qua để khôi phục lại bản vẽ ổn định nhất chỉ trong 1-click.