# BÀI TẬP LỚN SESSION 14: ĐẶC TẢ KHÔNG GIAN CỘNG TÁC DỰ ÁN GREEN-TECH (SMART FARM)

## I. TỔNG QUAN DỰ ÁN GREEN-TECH

Dự án **Green-Tech (Trang trại thông minh)** là dự án tích hợp hệ thống IoT giám sát độ ẩm, nhiệt độ và điều khiển tưới tiêu tự động. 

Để đảm bảo dự án vận hành mượt mà giữa các bên (Đội ngũ Dev, Nhà đầu tư, Đối tác phần cứng), nhóm thiết lập một hệ sinh thái cộng tác tích hợp giữa **GitHub / GitLab (Quản lý Code)**, **Google Workspace / OneDrive (Lưu trữ Báo cáo)** và **Slack / Teams (Enterprise Workspace)**.

---

## II. CẤU TRÚC KHÔNG GIAN CỘNG TÁC (SPECIFICATION)

### 1. Cấu trúc Folder Lưu trữ & Quản lý Phân quyền (Drive / Cloud Storage)

Toàn bộ tài liệu dự án được lưu trữ tập trung tại Root Folder: `[GREEN-TECH_SMART_FARM]`.

```text
[GREEN-TECH_SMART_FARM]
├── 01_SOURCE_CODE/ (Hybrid Workflow Sync)
│   ├── sensors/ (Mã nguồn đọc dữ liệu cảm biến)
│   ├── backend/ (Xử lý dữ liệu & API)
│   └── .gitignore (Cấu hình CHẶN push file .env)
├── 02_REPORTS_INVESTORS/ (Thư mục Báo cáo Investor)
│   ├── Financial_Report_Q1.pdf
│   └── Project_Milestones_2026.docx
├── 03_HARDWARE_SPECS/ (Thư mục Đối tác Thiết bị)
│   ├── Sensor_Datasheet_v2.pdf
│   └── Feedback_Hardware_Vendor.docx
└── 04_CONFIG_PRIVATE/ (Thư mục Bảo mật Admin/Dev Lead)
    └── .env.example (Mẫu cấu hình biến môi trường, KHÔNG chứa mật khẩu thật)
```

#### Ma trận Phân quyền (Permissions Matrix):

| Đối tượng | Thư mục tiếp cận | Quyền hạn (Permission) | Mô tả & Ràng buộc bảo mật |
| :--- | :--- | :--- | :--- |
| **Nhà đầu tư (Investors)** | `02_REPORTS_INVESTORS` | **Viewer** (Chỉ xem) | Tắt tính năng cho phép tải xuống (Download), in (Print) hoặc sao chép (Copy) để bảo mật thông tin tài chính. |
| **Đối tác thiết bị (Vendors)** | `03_HARDWARE_SPECS` | **Commenter** (Bình luận) | Có thể đọc tài liệu và để lại nhận xét/gợi ý ngay trên file mà không có quyền sửa nội dung gốc. |
| **Đội ngũ Dev** | `01_SOURCE_CODE`, `04_CONFIG_PRIVATE` | **Editor / Contributor** | Có quyền đẩy code, chỉnh sửa file. Không có quyền xóa thư mục gốc. |
| **Project Lead (Admin)** | All Folders | **Owner** (Chủ sở hữu) | Phân quyền toàn hệ thống, quản lý khóa bảo mật. |

---

### 2. Cấu trúc Kênh Truyền thông (Enterprise Workspace - Slack/Teams)

Hệ thống channel được phân chia rõ ràng theo mục đích sử dụng để tránh nhiễu thông tin:

* `#announcements` (Chỉ Read-only với Member): Thông báo quan trọng từ Lead.
* `#dev-sensors` (Public trong Dev Team): Trao đổi kỹ thuật, sửa lỗi code cảm biến.
* `#vendor-hardware` (Guest Channel - Shared with Vendors): Trao đổi về thông số kỹ thuật thiết bị với đối tác.
* `#investor-updates` (Private Channel): Cập nhật tiến độ định kỳ cho Nhà đầu tư.

---

## III. QUY TRÌNH KỸ THUẬT & NGHIỆP VỤ (WORKFLOWS)

### 1. Hybrid Workflow cho Đội Dev (Bảo mật Code & File `.env`)

Để đảm bảo mã nguồn và mật khẩu cảm biến không bị rò rỉ hoặc mất mát:

* **Sử dụng Git + Cloud Hybrid:** Mã nguồn chính được quản lý bằng Git (GitHub). File dung lượng lớn hoặc tài liệu thiết kế cứng được đồng bộ qua Cloud Drive.
* **Bảo vệ File `.env` chứa Mật khẩu Cảm biến:**
  1. Thêm `.env` vào file `.gitignore` ngay từ khi khởi tạo Repository.
  2. Không bao giờ commit file `.env` lên GitHub/Drive công khai.
  3. Chỉ lưu file `.env.example` (chứa các biến mẫu như `SENSOR_DB_PASS=your_password_here`) lên kho chứa.
  4. Trưởng nhóm sẽ chuyển giao mật khẩu cảm biến thực tế cho các bạn Dev qua kênh truyền thông mã hóa an toàn (1-on-1 Secret Chat) hoặc Bitwarden/1Password.

---

### 2. Chuyển đổi Thảo luận thành Task có Deadline (Enterprise Communication)

Khi phát hiện sự cố cảm biến trên kênh `#dev-sensors`, quy trình xử lý bất đồng bộ như sau:

```text
[Thảo luận lỗi trên Slack] 
       │
       ▼
[Tích hợp Jira / Trello Action] 
       │
       ▼
[Tạo Task tự động + Set Deadline + Assignee]
```

**Kịch bản thực tế:**
1. **Phát hiện lỗi:** Trên kênh `#dev-sensors`, Dev báo lỗi: *"Cảm biến DHT22 ở khu nhà kính B trả về giá trị -999°C"*.
2. **Thao tác chuyển đổi:** Click vào dấu 3 chấm `...` ở tin nhắn Slack -> Chọn **Create Issue in Jira**.
3. **Cấu hình Task:**
   * **Title:** `[BUG] Fix lỗi đọc sai dữ liệu cảm biến DHT22 - Nhà kính B`
   * **Assignee:** `@Dev_Nam`
   * **Priority:** `High`
   * **Deadline:** `18:00 - 02/11/2026`
4. Hệ thống sẽ tự động gửi một Card thông báo ngược lại channel `#dev-sensors` để cả team nắm tiến độ mà không cần chat qua lại.

---

### 3. Quy trình Transfer Ownership khi Kết thúc Bài tập Nhóm

Khi kết thúc môn học/dự án, để bàn giao lại toàn bộ không gian cộng tác cho GV/Chủ dự án mới:

1. **Chuyển giao Cloud Storage (Google Drive / OneDrive):**
   * Truy cập Cài đặt chia sẻ thư mục gốc `[GREEN-TECH_SMART_FARM]`.
   * Thêm email người nhận bàn giao -> Chọn quyền **Editor**.
   * Sau khi họ chấp nhận, chọn lại menu thả xuống bên cạnh tên họ -> Chọn **Transfer Ownership** (Chuyển quyền sở hữu).
   * Xác nhận chuyển giao.

2. **Chuyển giao Repository (GitHub/GitLab):**
   * Vào `Settings` của Repository -> Tìm mục **Danger Zone**.
   * Chọn **Transfer ownership** -> Nhập tên Username/Organization mới -> Xác nhận tên Repo để hoàn tất.

---

## IV. KỊCH BẢN KIỂM THỬ (TEST CASE): KHÔI PHỤC KHI BỊ XÓA DỮ LIỆU

**Tình huống sự cố:** Một bạn thành viên lỡ tay xóa sạch folder `01_SOURCE_CODE/sensors` trên Google Drive / Cloud Storage chung của nhóm.

### Quy trình Khôi phục Nhanh nhất (Recovery Plan):

```text
Phát hiện mất Folder ──> Kiểm tra Thùng rác (Trash) ──> Khôi phục từ Git Local ──> Kiểm tra Version History
```

* **Cách 1: Khôi phục từ Thùng rác (Cloud Recycle Bin / Trash) - *Nhanh nhất (30 giây)***
  1. Trưởng nhóm (Owner) hoặc người xóa truy cập vào mục **Trash (Thùng rác)** trên Google Drive / OneDrive.
  2. Tìm thư mục `sensors` vừa bị xóa (Cloud vẫn lưu trữ file bị xóa trong 30 ngày).
  3. Click chuột phải -> Chọn **Restore (Khôi phục)**. Thư mục và toàn bộ phân quyền cũ sẽ lập tức xuất hiện lại đúng vị trí ban đầu.

* **Cách 2: Khôi phục từ Git Repository (Nếu thư mục Cloud bị xóa vĩnh viễn)**
  1. Do nhóm sử dụng **Hybrid Workflow**, toàn bộ code trong `sensors` đều đã được commit & push lên GitHub trước đó.
  2. Dev mở Terminal tại máy local và gõ lệnh pulldata/checkout lại nhánh mới nhất:
     ```bash
     git checkout main
     git pull origin main
     ```
  3. Upload lại folder `sensors` từ máy local lên Cloud Drive và thiết lập lại phân quyền trong 2 phút.

