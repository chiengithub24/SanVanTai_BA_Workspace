---
name: review-srs
description: Thẩm định và rà soát tài liệu đặc tả chức năng (SRS) từ BP Nghiệp vụ / Đội IT gửi sang. Tự động đối chiếu với System-Docs và Checklist Sàn Vận Tải để phát hiện lỗi gãy luồng cũ, thiếu sót và bắt bài các điểm đùn đẩy trách nhiệm.
---

# KỸ NĂNG: RÀ SOÁT & PHẢN BIỆN SRS (REVIEW-SRS)

Kỹ năng này đóng vai trò là "Thẩm định viên giải pháp độc lập", bảo vệ quyền lợi của Đơn vị yêu cầu (Ranh 1) theo Quy trình 6.1.2.

## Cơ chế hoạt động:
Khi người dùng gõ `/review-srs` hoặc yêu cầu rà soát một tài liệu SRS:

1. **Nạp ngữ cảnh tự động (Không cần BA copy-paste thủ công):**
   - Đọc các quy tắc hiện trạng tương ứng trong thư mục `System-Docs/`.
   - Đọc bộ tiêu chí kiểm định chuyên sâu tại `BA_AI_COPILOT/03_Checklist_Review_SRS_SanVanTai.md`.
   - Đọc nội dung file SRS mà người dùng cung cấp (ví dụ trong thư mục `PYC/<mã-pyc>/raw/`).

2. **Thực hiện rà soát 5 chiều:**
   - **Tính đúng đắn (Correctness):** SRS có giải quyết đúng bài toán nghiệp vụ của User không?
   - **Tương thích ngược (Backward Compatibility):** Tính năng mới có làm hỏng các đơn hàng/dự toán dở dang trong quá khứ không? Có ảnh hưởng luồng xuất HĐ FICO không?
   - **Bắt bài đùn đẩy (Push-back Detection):** Phát hiện các câu từ mập mờ kiểu: *"Nghiệp vụ tự kiểm tra"*, *"Hệ thống sẽ cập nhật sau"*, *"Theo thỏa thuận miệng"* để chuyển giao lại trách nhiệm cho BP Nghiệp vụ.
   - **Độ phủ luồng ngoại lệ (Exceptions):** Kiểm tra xem có luồng hủy, từ chối, timeout API FICO/QLX không.
   - **Phân quyền & Dữ liệu:** Phân quyền theo chức năng và phạm vi dữ liệu có rõ ràng theo mã quyền STMS không.

3. **Xuất kết quả & Tự động lưu trữ:**
   - Trả về Bảng Nhật Ký Review SRS (SRS Review Matrix) phân loại rõ **Blocker / Major / Minor**.
   - Tự động lưu báo cáo này vào file `PYC/<mã-pyc>/02-nhat-ky-review-srs-phan-bien.md`.
