#  Xây dựng Không gian Cộng tác Doanh nghiệp

## ***Phần 1: Sơ đồ kiến trúc kênh 

***Để chia rõ từng mục đích sử dụng và không bị lẫn lộn giữa công việc với giải trí, bọn em phân chia thành các Channel cụ thể sau:***

- #01_general (Chung):

  - Quy định nội dung: Dùng để thông báo các tin tức chung của cả nhóm, các mốc milestone lớn hoặc lịch họp cố định hàng tuần. Cấm spam chat linh tinh ở đây.

- #02_dev_hardware (Kỹ thuật & Cảm biến):  
   
   - Quy định nội dung: Chuyên thảo luận về code, phần cứng, sơ đồ mạch của cảm biến bãi đỗ xe, API hoặc lỗi phần mềm. Mọi trao đổi phải dùng tính năng Reply in Thread (Trả lời trong luồng) cho từng vấn đề riêng biệt để tránh trôi tin.

- #03_deadline_task (Tiến độ & Deadline):

  - Quy định nội dung: Nơi cập nhật tiến độ công việc, ai đang làm phần nào, nhắc nhở deadline và bàn giao task. Tránh việc dùng chung chỗ chat linh tinh để không ai bị quên việc.

- #04_random_meme (Góc giải trí):

   - Quy định nội dung: Nơi cho anh em xả stress, gửi ảnh mèo, sticker hài hước, rủ đi uống trà sữa hay bàn chuyện ăn uống. Thích quẩy gì thì quẩy ở đây, tuyệt đối không đưa thông tin kỹ thuật vào kênh này.

## ***Phần 2: Bản quy ước giao tiếp***

***Để giải quyết triệt để vấn đề mất tập trung khi code và chống trôi tin, nhóm em đặt ra 3 quy tắc vàng sau:***

**1. Quy tắc chống "No-Hello Trap" và ép rep ngay lập tức**

- Vấn đề: Lập trình viên đang ngồi gõ code mà có đứa nhắn "Ê", "Alo", "Có việc này chút" rồi đứng chờ rep thì mất hết mạch tư duy.

- Cách giải quyết: Áp dụng thông điệp đầy đủ ngay từ đầu (Context + Vấn đề + Câu hỏi cụ thể). Ví dụ không nhắn: "Ê mày ơi", mà phải nhắn luôn: "Lỗi cảm biến slot 3 đang bị NullPointerException ở hàm check slot, tao đang fix ở nhánh dev-sensors, ai rảnh ngó hộ tao đoạn này với [kèm ảnh/snippet code]". Ai thấy thì phản hồi lúc rảnh theo kiểu bất đồng bộ (Asynchronous), không bắt buộc phải rep sau 1 giây.

**2. Quy tắc sử dụng Thread (Reply in Thread) triệt để**

- Vấn đề: Một vấn đề kỹ thuật tranh luận dài dòng làm trôi hết các thông tin khác trên màn hình chính.

- Cách giải quyết: Khi bắt đầu một câu hỏi hoặc báo lỗi cảm biến, mọi người phải thảo luận sâu vào nút Reply in Thread của tin nhắn đó. Khung chat chính sẽ cực kỳ sạch sẽ, ai cần theo dõi phần nào thì bấm vào thread đó đọc lại.

**3. Quy tắc cấm lạm dụng @all / @channel vô tội vạ**
- Vấn đề: Cả ngày cứ nghe tiếng thông báo réo tên vì mấy chuyện không đâu làm ae cáu và mất tập trung.

- Cách giải quyết: Chỉ được phép dùng @all hoặc @channel khi thực sự có sự cố khẩn cấp sập server, trễ deadline gấp trong vòng 2 tiếng hoặc thông báo họp khẩn. Còn lại các vấn đề cá nhân hoặc hỏi ai thì tag thẳng tên người đó (@tên_thành_viên), người được tag sẽ chủ động check khi xong việc của mình.