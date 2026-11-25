---
name: soan-pyc
description: Khởi tạo Phiếu đề nghị yêu cầu (PYC) chuẩn form Viettel Post cho các tính năng trên Sàn Vận Tải. Tự động viết tiêu chí nghiệm thu Acceptance Criteria chuẩn BDD (Given-When-Then) và lưu vào thư mục PYC.
---

# KỸ NĂNG: SOẠN THẢO PHIẾU ĐỀ NGHỊ YÊU CẦU (SOAN-PYC)

Kỹ năng này giúp BA nhanh chóng tạo ra một bản Phiếu Yêu Cầu (PYC) chuẩn mực, chặt chẽ để trình ký Lãnh đạo đơn vị và chuyển giao sang BP Kế hoạch & BP Nghiệp vụ (Bước 1 & Bước 4 trên Quy trình 6.1.2).

## Cơ chế hoạt động:
Khi người dùng gõ `/soan-pyc` hoặc yêu cầu làm PYC cho một tính năng:

1. **Thu thập thông tin:**
   - Tiếp nhận nhu cầu thô từ người dùng (tên tính năng, bài toán kinh doanh, mong muốn của user).
   - Tham chiếu kiến trúc và quy tắc liên quan trong `System-Docs/`.
   - Áp dụng biểu mẫu chuẩn tại `BA_AI_COPILOT/04_Mau_PYC_Chuan_ViettelPost.md`.

2. **Xây dựng cấu trúc PYC chuẩn hóa:**
   - **Bối cảnh & Căn cứ:** Thực trạng vận hành, khó khăn của chi nhánh/sales/kế toán.
   - **Mục tiêu định tính & định lượng:** Đo lường hiệu quả cụ thể.
   - **Ranh giới In-Scope & Out-of-Scope (Chốt chặn quan trọng):** Khóa cứng những gì làm và KHÔNG làm để bảo vệ BA khỏi việc bị phình phạm vi.
   - **Đặc tả nghiệp vụ & Acceptance Criteria (AC):** Viết theo chuẩn BDD:
     * *Given (Khi trạng thái ban đầu...)*
     * *When (Khi người dùng thực hiện hành động...)*
     * *Then (Hệ thống phải phản hồi/xử lý...)*
   - **Phạm vi ảnh hưởng & Yêu cầu tích hợp:** FICO, QLX, NOC, SAP ZBMS, vOffice.

3. **Lưu trữ chuẩn quy cách:**
   - Khởi tạo thư mục: `PYC/<mã-pyc>-<tên-ngắn-gọn>/`
   - Ghi nội dung vào file: `PYC/<mã-pyc>-<tên-ngắn-gọn>/01-phieu-yeu-cau-pyc.md`.
