# PHIẾU ĐỀ NGHỊ YÊU CẦU: CẤU HÌNH TỶ LỆ DỰ TOÁN / QUYẾT TOÁN
## MÃ PYC: PYC_SVT_10950_DUTOAN_2026

* **Đơn vị đề nghị:** Khối Nghiệp vụ Sàn Vận Tải (Ranh 1 - Quy trình 6.1.2)  
* **Phân hệ:** Sàn Vận Tải (STMS SVT), tích hợp STMS QLX, vOffice  
* **Trạng thái:** Đã phê duyệt trình ký (Chuyển sang Bước 3 cho BP Nghiệp vụ làm SRS)  

---

## 1. BỐI CẢNH VÀ CĂN CỨ
* Hiện tại trên hệ thống Sàn Vận Tải, khi tạo Dự toán hoặc Quyết toán cho đơn hàng nguyên chuyến, hệ thống chỉ hỗ trợ các biểu mẫu tỷ lệ chi phí cố định (Biểu mẫu công ty LOG, Biểu mẫu Chi nhánh VTP...).
* Do biến động giá thị trường, nhiều loại xe thuê ngoài và đối tác vận chuyển mới có định mức chi phí khác nhau, việc áp dụng tỷ lệ cứng khiến người dùng phải điều chỉnh thủ công ngoài hệ thống, gây khó khăn cho việc kiểm soát lợi nhuận.
* Cần nâng cấp hệ thống để cho phép cấu hình tỷ lệ phân bổ chi phí linh hoạt theo đơn vị, dịch vụ và thời gian áp dụng.

## 2. PHẠM VI (SCOPE BOUNDARY)
* **In-Scope (Phạm vi thực hiện):**
  - Màn hình Quản lý danh sách cấu hình tỷ lệ Dự toán/Quyết toán.
  - Form thêm mới, chỉnh sửa, vô hiệu hóa cấu hình tỷ lệ.
  - Bổ sung trường ngày bắt đầu áp dụng (`Valid From`).
  - Áp dụng tỷ lệ mới cho các Dự toán/Quyết toán tạo mới sau thời điểm hiệu lực.
  - Phân quyền thao tác cấu hình cho cấp quản lý.
* **Out-of-Scope (Tuyệt đối không làm trong đợt này):**
  - Không tính toán lại các Dự toán / Quyết toán đã ở trạng thái `Đã lưu`, `Chờ duyệt` hoặc `Đã duyệt vOffice` trước thời điểm hiệu lực.
  - Không thay đổi luồng xuất hóa đơn và đối soát công nợ trên SAP FICO.

## 3. TIÊU CHÍ NGHIỆM THU (ACCEPTANCE CRITERIA)
* **AC-01 (Kiểm soát tổng tỷ lệ = 100%):**  
  *Given* Người dùng mở màn hình thêm mới cấu hình;  
  *When* Nhập các tỷ lệ thành phần mà tổng khác 100% và bấm Lưu;  
  *Then* Hệ thống chặn lưu và thông báo lỗi: *"Tổng tỷ lệ chi phí và lợi nhuận phải bằng đúng 100%"*.
* **AC-02 (Bảo toàn số liệu cũ):**  
  *Given* Bảng cấu hình mới có hiệu lực từ ngày mai;  
  *When* Người dùng mở lại một Dự toán đã lập từ tuần trước;  
  *Then* Số liệu của Dự toán cũ được giữ nguyên 100%, không bị tự động nhảy theo tỷ lệ mới.
