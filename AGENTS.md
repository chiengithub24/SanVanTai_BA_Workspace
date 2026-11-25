# NGUYÊN TẮC VẬN HÀNH & TỰ ĐỘNG CẬP NHẬT (AGENTS.MD)
## DỰ ÁN SÀN VẬN TẢI (SMART TMS) - VIETTEL POST

Tài liệu này là chỉ dẫn bắt buộc dành cho AI (Antigravity) và thành viên dự án khi tương tác trong workspace `SanVanTai_BA_Workspace`.

---

## 📌 1. NGUYÊN TẮC TỰ ĐỘNG LƯU TRỮ VÀ CẬP NHẬT TRI THỨC (LIVING KNOWLEDGE BASE)

Hệ thống Sàn Vận Tải liên tục phát triển theo vòng tròn lặp:  
**`System-Docs (Hiện trạng) ➔ Yêu cầu mới ➔ PYC ➔ SRS Review ➔ Triển khai/UAT ➔ CẬP NHẬT SYSTEM-DOCS`**

Khi làm việc trong workspace, AI và người dùng bắt buộc tuân thủ:

1. **Kiến thức nền tảng & Luồng hệ thống chung:**
   - Mọi quy tắc nghiệp vụ, luồng trạng thái, điểm chạm FICO/NOC/SAP mới phát hiện hoặc được cập nhật sau khi tính năng golive **BẮT BUỘC ĐƯỢC CẬP NHẬT VÀO THƯ MỤC `System-Docs/`**.
   - Tuyệt đối không để kiến thức bị trôi mất trong các đoạn chat. Lần làm việc sau sẽ đọc trực tiếp từ `System-Docs/` thay vì phải bơi lại trong các file HDSD cũ.

2. **Quản lý nhiệm vụ theo từng PYC:**
   - Mọi yêu cầu phát triển/nâng cấp đều được quản lý theo thư mục riêng biệt tại:  
     `PYC/<mã-pyc>-<tên-ngắn-gọn>/`
   - Cấu trúc chuẩn bên trong thư mục mỗi PYC:
     * `raw/`: Lưu các file gốc nhận từ nghiệp vụ hoặc BP phát triển (`.docx`, `.pdf`, `.xlsx`...).
     * `01-phieu-yeu-cau-pyc.md`: Bản Phiếu Đề Nghị Yêu Cầu chuẩn form Viettel Post để trình ký.
     * `02-nhat-ky-review-srs-phan-bien.md`: Bảng đối chiếu, bắt lỗi SRS và câu hỏi chất vấn BP Nghiệp vụ.
     * `03-kich-ban-nghiem-thu-uat.md`: Danh sách kịch bản kiểm thử Acceptance Criteria (Given-When-Then) dùng khi nghiệm thu Bước 9.

---

## 📌 2. NGUYÊN TẮC BẢO VỆ RANH GIỚI THEO QUY TRÌNH 6.1.2

1. **Ranh 1 (Đơn vị yêu cầu - BA của team):** Chỉ chịu trách nhiệm về Bài toán kinh doanh, Mục tiêu, Phạm vi và Tiêu chí chấp nhận (WHAT & WHY).
2. **Ranh 3 (BP Nghiệp vụ / Đội IT):** Bắt buộc phải chịu trách nhiệm khảo sát CSDL, thiết kế API, viết luồng chi tiết (HOW).
3. Khi phát hiện BP Nghiệp vụ cài cắm câu từ mơ hồ hoặc đùn đẩy việc thiết kế kỹ thuật sang cho BA, AI có nhiệm vụ cảnh báo và kích hoạt kỹ năng `phan-bien-ba` để bảo vệ BA.
