# Quản lý Quyền truy cập Báo cáo Tài chính

## ***PHẦN 1: Bản thiết kế phân quyền bảo mật***

Để bảo vệ thông tin nhạy cảm như SĐT và mức lương kỳ vọng của ứng viên, chúng ta áp dụng Quy tắc Cờ Đỏ Bảo mật (tuyệt đối không dùng Anyone with the link kết hợp với Editor), thiết lập bảng phân quyền an toàn nhất như sau:

Dưới đây là bản thiết kế phân quyền bảo mật cho danh sách CV ứng viên ở Phần 1 được định dạng thành bảng Markdown chuẩn chỉnh:

| Đối tượng người dùng | Mức quyền đề xuất | Phạm vi chia sẻ | Ghi chú vận hành & Chống lỗi

 |
| --- | --- | --- | --- |
| **Các Trưởng bộ phận (Hiring Managers)** | **Commenter** (hoặc Editor nội bộ khi thực sự cần)

 | **Restricted** (Chỉ thêm đích danh email công ty của các trưởng bộ phận)

 | Cho phép các trưởng bộ phận xem và để lại nhận xét, góp ý. Khuyến khích bật chế độ **Suggesting Mode** (Gợi ý) nếu dùng Google Docs để không làm thay đổi trực tiếp dữ liệu gốc khi chưa được HR duyệt.

 |
| **Nhân sự nội bộ tuyển dụng (HR Team)** | **Editor**

 | **Restricted** (Chỉ thêm email nội bộ của team HR)

 | Toàn quyền cập nhật, bổ sung thông tin ứng viên mới vào danh sách chung trong môi trường nội bộ an toàn.

 |
| **Ứng viên bên ngoài / Người không liên quan** | **No Access** (Không có quyền)

 | **Restricted** (Tuyệt đối không cấp quyền mở công khai)

 | Ngăn chặn hoàn toàn việc rò rỉ dữ liệu cá nhân nhạy cảm ra bên ngoài tổ chức.

 |



