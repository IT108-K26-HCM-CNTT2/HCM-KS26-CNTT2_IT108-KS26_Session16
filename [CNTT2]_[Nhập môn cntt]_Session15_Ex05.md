# BÀI TẬP CÁ NHÂN: NGUYÊN TẮC GIAO TIẾP BẤT ĐỒNG BỘ (ASYNC COMMUNICATION) IN TEAMWORK

## I. Phân tích bối cảnh & Múi giờ của Team

Team startup của em gồm có 5 người nằm ở 3 múi giờ khác nhau:
1. **Hà Nội (Việt Nam - UTC+7):** 3 bạn (Dev Front-end, Back-end, UI/UX).
2. **Tokyo (Nhật Bản - UTC+9):** 1 bạn (Sớm hơn Hà Nội 2 tiếng).
3. **California (Mỹ - UTC-7):** 1 bạn (Trễ hơn Hà Nội 14 tiếng - ví dụ 8h sáng ở Hà Nội là 6h tối hôm trước ở Mỹ).

**Vấn đề:** Nếu ai cũng muốn nhắn tin hỏi đáp là có người trả lời ngay (Synchronous) thì người ở Mỹ hoặc Nhật sẽ bị làm phiền lúc nửa đêm, hoặc việc sẽ bị đứt đoạn do chờ phản hồi. 

Do đó, cả nhóm cần áp dụng **Async Communication**: 
- Nhắn tin đầy đủ thông tin ngay từ đầu để người đọc không phải chat qua lại để hỏi thêm.
- Tránh văn hóa "No-Hello" (chỉ nhắn "Alo", "Hi" rồi bắt người ta chờ mình gõ tiếp).

---

## II. Tin nhắn mẫu yêu cầu hỗ trợ Fix Bug (Chuẩn Async)

**Tình huống:** Em (Dev Back-end ở Hà Nội) phát hiện bug tràn bộ nhớ khi xử lý upload ảnh. Bug này liên quan đến phần tối ưu CDN do bạn Dev ở Mỹ đảm nhận.

**Nơi gửi:** Kênh Slack `#tech-support`  
**Đối tượng:** `@John` (Thành viên ở Mỹ)

---

### [MẪU TIN NHẮN SLACK]

**[BUG HIGH] Cần hỗ trợ kiểm tra tràn bộ nhớ khi upload ảnh (> 10MB)**

Chào @John, chúc ông một ngày tốt lành! 

Tối nay bên tớ test thử chức năng upload ảnh đại diện thì phát hiện bị crash server nếu người dùng tải lên file dạng PNG dung lượng trên 10MB. Tớ đã tái hiện được lỗi này 100% trên môi trường Staging.

**1. Chi tiết lỗi & Ngữ cảnh:**
* **Môi trường:** Staging (v1.2.0)
* **API bị ảnh hưởng:** `POST /api/v1/user/avatar`
* **Mô tả:** Server báo lỗi `500 Internal Server Error` và nhả ra log `FATAL ERROR: Ineffective mark-compacts near heap limit Allocation failed - JavaScript heap out of memory`.

**2. Đã kiểm tra & Loại trừ:**
* Phía Back-end tớ đã giới hạn multer stream nhưng hình như đoạn nén ảnh đẩy sang Cloudinary CDN của ông đang giữ buffer quá lâu.
* File log chi tiết tớ đã đính kèm ở dưới.

**3. Link & Tài liệu đính kèm:**
* Link ticket Jira: [PROJ-245: Fix memory leak upload avatar](https://jira.example.com/browse/PROJ-245)
* File log Server: `error_log_20261031.txt` (đã đính kèm trong thread)
* Video màn hình lúc bị lỗi: `demo_bug.mp4`

**4. Hành động mong muốn (Action Items):**
* Nhờ John nghía qua giúp tớ file `services/cdnUploader.js`, đặc biệt là hàm `streamUpload()`.
* Khi nào ông ngủ dậy vào ca làm việc thì xem giúp tớ nhé, không cần gấp ngay đêm nay đâu! Nếu xong trước 12h trưa giờ Mỹ ngày mai thì tốt quá để bên Việt Nam test lại luôn.

Cảm ơn ông nhiều!

---

## III. Lịch trình gửi tin nhắn (Schedule Send)

Để đảm bảo không bắn notification làm phiền đồng đội lúc họ đang ngủ, em thiết lập Schedule Send trên Slack / Gmail như sau:

| Thành viên | Vị trí (Múi giờ) | Giờ sinh hoạt / Làm việc | Thời điểm Schedule Send phù hợp (Giờ Việt Nam) | Mục đích / Giải thích |
| :--- | :--- | :--- | :--- | :--- |
| **3 bạn Hà Nội** | UTC+7 | 08:30 - 17:30 (Khung giờ chuẩn) | **08:30 AM** | Gửi ngay đầu giờ sáng để team VN nắm task trong ngày. |
| **1 bạn Nhật Bản** | UTC+9 (Nhanh hơn 2h) | 08:30 - 17:30 (Tương đương 06:30 - 15:30 giờ VN) | **07:00 AM - 07:30 AM** | Lúc này bên Nhật là 09:00 AM, bạn đó vừa lên công ty, check tin nhắn là hợp lý nhất. |
| **1 bạn Mỹ** | UTC-7 (Chậm hơn 14h) | 08:30 - 17:30 (Tương đương 22:30 - 07:30 giờ VN hôm sau) | **22:00 PM - 22:30 PM** | Lúc 22h đêm ở Việt Nam thì bên Mỹ mới bắt đầu là 08h sáng. Bạn ấy vừa ngủ dậy mở máy làm việc sẽ nhận được ngay, không bị gián đoạn giấc ngủ. |
