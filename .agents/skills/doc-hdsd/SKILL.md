---
name: doc-hdsd
description: Bóc tách tài liệu HDSD hoặc Slide đào tạo hệ thống Sàn Vận Tải (As-Is) thành bảng Luật Nghiệp vụ, Ma trận trạng thái, và Điểm chạm tích hợp FICO/NOC/SAP để cập nhật vào System-Docs.
---

# KỸ NĂNG: BÓC TÁCH & HIỂU NHANH HIỆN TRẠNG (DOC-HDSD)

Kỹ năng này giúp BA đọc hiểu nhanh bất kỳ tài liệu Hướng dẫn sử dụng (HDSD), Slide đào tạo hay văn bản mô tả thao tác nào của hệ thống Sàn Vận Tải mà không bị ngợp.

## Hướng dẫn thực hiện cho AI:

Khi người dùng yêu cầu bóc tách tài liệu HDSD (hoặc gõ `/doc-hdsd` kèm đường dẫn file / đoạn text):

1. **Đọc và phân tích:**
   - Đọc trực tiếp file tài liệu được chỉ định (từ thư mục `HDSD/` hoặc đoạn văn bản người dùng cung cấp).
   - Xác định phân hệ nghiệp vụ thuộc bước nào trong **Chu trình 10 bước** (`System-Docs/00-tong-quan-chu-trinh-10-buoc.md`).

2. **Trích xuất 4 thành phần cốt lõi:**
   - **Vòng đời đối tượng (State Lifecycle):** Trạng thái bắt đầu, điều kiện chuyển trạng thái, trạng thái kết thúc, vai trò thao tác.
   - **Quy tắc nghiệp vụ ngầm (Business Rules):** Các công thức tính toán (Doanh thu, Chi phí, Tỷ lệ), điều kiện validate, trường bắt buộc.
   - **Điểm chạm tích hợp:** Gửi nhận dữ liệu với hệ thống nào (STMS QLX, SAP FICO, NOC, SAP ERP ZBMS, vOffice).
   - **Rủi ro chí mạng:** Các hành động không thể hoàn tác (Ví dụ: BBNTKH đã sang FICO không được hủy trực tiếp).

3. **Cập nhật tri thức (Living Knowledge):**
   - Đề xuất hoặc tự động cập nhật tri thức này vào tài liệu tương ứng trong thư mục `System-Docs/` để các lần làm việc sau không phải đọc lại file gốc cồng kềnh.
