# BẢNG NHẬT KÝ THẨM ĐỊNH VÀ PHẢN BIỆN SRS (SRS REVIEW LOG)
## TÀI LIỆU REVIEW: SRS_QLNVVP_10950_Cấu hình Dự toán_Quyết toán.docx (v1.04)
* **Người thực hiện review:** BA Đơn vị yêu cầu (Hỗ trợ bởi AI Copilot)  
* **Đơn vị nhận giải trình:** Bộ phận Nghiệp vụ / IT BA (Ranh 3 - Quy trình 6.1.2)  
* **Kết luận thẩm định:** ⚠️ **YÊU CẦU SỬA ĐỔI VÀ GIẢI TRÌNH TRƯỚC KHI TRÌNH DUYỆT SẢN XUẤT**  

---

## 1. MA TRẬN PHÁT HIỆN LỖ HỔNG VÀ BẮT LỖI SRS (REVIEW MATRIX)

| STT | Vị trí SRS | Đề xuất trong SRS của IT | Lỗ hổng / Rủi ro thực tế | Mức độ | Yêu cầu BP Nghiệp vụ giải trình & sửa đổi |
|:---:|---|---|---|:---:|---|
| **1** | UC01 - Mục 2.1.2 Luồng xử lý | Form cấu hình tỷ lệ không có trường Ngày bắt đầu hiệu lực (`Valid From`). | **Blocker** (Gây xung đột): Nếu cấu hình có hiệu lực ngay tại thời điểm bấm lưu, các đơn hàng đang được Sales tạo dở dang trong ngày sẽ bị tính toán nhảy loạn xạ. | **Blocker** | Bắt buộc bổ sung trường `Ngày bắt đầu áp dụng` (Mặc định 00:00 ngày hôm sau) và khóa không cho sửa khi đã đến hạn hiệu lực. |
| **2** | UC03 - Mục 2.3.2 Áp dụng tỷ lệ mới | SRS ghi: *"Khi người dùng mở lại màn hình dự toán, hệ thống tự động cập nhật tính lại theo tỷ lệ mới nhất"*. | **Blocker** (Làm gãy luồng cũ): Vi phạm nguyên tắc bất biến số liệu đã trình ký. Dự toán đã duyệt trên vOffice nếu mở lại bị nhảy số mới sẽ lệch hoàn toàn với văn bản pháp lý đã ký! | **Blocker** | Bổ sung rule chặn: Chỉ áp dụng tỷ lệ mới cho Dự toán bấm **Tạo mới**. Dự toán đã lưu/đã duyệt vOffice phải khóa cứng dữ liệu lịch sử. |
| **3** | UC01 - Phân quyền | SRS ghi: *"Người dùng có quyền quản trị được cấu hình"*. | **Major** (Rủi ro bảo mật): Câu từ mơ hồ, không gắn với mã quyền cụ thể của hệ thống STMS. | **Major** | Cần định nghĩa mã quyền chuẩn (Ví dụ: `CN_CONFIG_BUDGET`) và chỉ phân quyền cho cấp Trưởng phòng trở lên. |
| **4** | UC02 - Hiển thị thông báo | Khi tỷ lệ thay đổi chỉ có popup thông báo trên màn hình. | **Minor** (Thiếu luồng tra soát): Nếu người dùng tắt popup thì không xem lại được. | **Minor** | Bổ sung màn hình/tab "Lịch sử thay đổi tỷ lệ cấu hình" để tiện đối soát khi có khiếu nại. |

---

## 2. BẮT BÀI ĐIỂM ĐÙN ĐẨY TRÁCH NHIỆM

* **Trích dẫn trong SRS (Mục 2.3):** *"Đơn vị nghiệp vụ tự chịu trách nhiệm kiểm tra tính chính xác của tỷ lệ khi áp dụng vào dự toán"*.
* 👉 **Ý kiến phản biện của BA (Ranh 1):**  
  *"Đơn vị yêu cầu không đồng ý với điều khoản này. Đơn vị yêu cầu chịu trách nhiệm về số liệu đầu vào, nhưng hệ thống do BP Nghiệp vụ thiết kế BẮT BUỘC phải có hàm kiểm tra tự động: Tổng các tỷ lệ thành phần phải $= 100\%$, nếu $\neq 100\%$ thì hệ thống phải chặn không cho lưu và bôi đỏ trường dữ liệu lỗi, không thể đẩy rủi ro do lỗi hệ thống cho người dùng thao tác."*
