# VÍ DỤ THỰC CHIẾN (CASE STUDY MINH HỌA)
## PHÂN HỆ: CẤU HÌNH TỶ LỆ DỰ TOÁN / QUYẾT TOÁN TRÊN SÀN VẬN TẢI

> **Mục tiêu:** Minh họa thực tế kết quả đầu ra khi áp dụng Bộ công cụ AI 4 bước trên chính dữ liệu tài liệu thực tế của dự án (`HDSD hệ thống Sàn Vận tải.docx`, `SLIDE_HDSD...` và `SRS_QLNVVP_10950_Cấu hình Dự toán_Quyết toán.docx`).

---

## 🎬 TÌNH HUỐNG THỰC TẾ
* **Yêu cầu từ Giám đốc / Phòng Kinh doanh:** Trước đây trên Sàn Vận Tải, khi tạo Dự toán hoặc Quyết toán cho đơn hàng nguyên chuyến, hệ thống chỉ cho phép chọn các Biểu mẫu tỷ lệ cố định (ví dụ: Biểu mẫu công ty LOG, Biểu mẫu Chi nhánh VTP...). Hiện nay, do mở rộng tuyến vận tải liên tỉnh và đối tác mới, tỷ lệ chi phí nhiên liệu, thuê ngoài và lợi nhuận định mức biến động liên tục. Người dùng yêu cầu phải cho phép **cấu hình tỷ lệ linh hoạt** theo từng nhóm đối tác/tuyến đường.
* **Thực trạng bạn BA gặp phải:**
  - BP Nghiệp vụ (Ranh 3) gửi bản `SRS_QLNVVP_10950_Cấu hình Dự toán_Quyết toán.docx` dài hơn 60 trang (gồm UC01 đến UC05).
  - Họ bắt bạn BA phải đọc và review trong 2 ngày, đồng thời hỏi dồn dập: *"Tính năng này có ảnh hưởng sang FICO không? Đơn hàng cũ đang chạy dở thì tính thế nào? Tại sao lại cần sửa menu?"*.
  - Bạn BA bị ngợp và không biết bắt đầu từ đâu.

---

## BƯỚC 1: DÙNG PROMPT 1 TRÍCH XUẤT HIỆN TRẠNG (AS-IS) TỪ HDSD

Bạn BA copy phần "Dự toán & Quyết toán" trong file `HDSD hệ thống Sàn Vận tải.docx` và Slide 7, Slide 24 dán vào **Prompt 1**.

### 👉 KẾT QUẢ AI TRẢ VỀ CHO BẠN BA:
```markdown
### 1. TÓM TẮT QUY TRÌNH HIỆN TẠI (AS-IS):
- Bước 3 quy trình: Sales gom đơn -> Chọn Biểu mẫu tỷ lệ (cố định) -> Hệ thống tự tính Doanh thu/Chi phí/Lợi nhuận tạm tính -> Lưu dự toán -> Trình ký vOffice.
- Bước 10 quy trình: Sau khi hoàn thành chuyến và có hóa đơn FICO -> Kế toán gom đơn -> Chọn Biểu mẫu quyết toán -> Tính Doanh thu/Chi phí/Lợi nhuận thực tế -> Trình ký vOffice -> Đóng đơn.

### 2. MA TRẬN LUỒNG TRẠNG THÁI HIỆN TẠI:
| Đối tượng | Trạng thái hiện tại | Thao tác kích hoạt | Điều kiện chuyển | Trạng thái kế tiếp | Người thực hiện |
|---|---|---|---|---|---|
| Dự toán | Mới tạo (Nháp) | Bấm "Lưu dự toán" | Nhập đủ thông tin chi phí & biểu mẫu | Đã lưu | NVKD (Sales) |
| Dự toán | Đã lưu | Bấm "Trình ký vOffice" | Đã lưu thành công | Chờ phê duyệt | NVKD |
| Dự toán | Chờ phê duyệt | Lãnh đạo duyệt trên vOffice | Ký số hợp lệ | Đã duyệt dự toán | Lãnh đạo |
| Đơn hàng | Đã duyệt dự toán | Chuyển sang QLX | Dự toán được duyệt | Chờ gán xe/tài xế | BPVH |

### 3. ĐIỂM CHẠM VÀ RỦI RO CHÍ MẠNG:
- Số liệu Dự toán là căn cứ để Lãnh đạo duyệt chi phí tạm ứng và cho phép điều xe.
- Quyết toán sau khi được duyệt sẽ chốt số liệu lợi nhuận thực tế để đối chiếu với hóa đơn FICO và báo cáo NOC.
- RỦI RO LỚN NHẤT: Nếu tỷ lệ cấu hình mới bị áp đè lên các dự toán/quyết toán đã duyệt hoặc đang trình ký, sẽ làm SAI LỆCH toàn bộ số liệu báo cáo đã trình Lãnh đạo!
```
*(Chỉ mất 2 phút đọc bảng này, bạn BA đã nắm trọn vẹn luồng As-Is).*

---

## BƯỚC 2: DÙNG PROMPT 2 RÀ SOÁT & "BẮT LỖI" TÀI LIỆU SRS CỦA ĐỘI DEV

Bạn BA dán nội dung các Use Case trong file `SRS_QLNVVP_10950_Cấu hình Dự toán_Quyết toán.docx` vào **Prompt 2**.

### 👉 KẾT QUẢ AI PHÁT HIỆN CÁC LỖ HỔNG (SRS AUDIT FINDINGS):

```markdown
### BẢNG NHẬT KÝ BẮT LỖI SRS (SRS REVIEW MATRIX):

| STT | Vị trí SRS | Đề xuất trong SRS của Dev | Lỗ hổng / Rủi ro phát hiện | Mức độ | Yêu cầu BP Nghiệp vụ phải sửa |
|:---:|---|---|---|:---:|---|
| 1 | UC01 - Mục 2.1.2 Luồng xử lý | Cho phép tạo cấu hình tỷ lệ mới nhưng KHÔNG có trường ngày bắt đầu hiệu lực (`Effective Date`). | **CỰC KỲ NGUY HIỂM (Blocker):** Nếu lưu cấu hình mới mà áp dụng ngay lập tức trong ngày, sẽ gây xung đột với các đơn hàng đang được Sales lập dự toán cùng thời điểm. | **Blocker** | Bắt buộc bổ sung trường "Ngày bắt đầu áp dụng" (Mặc định từ 00:00 ngày hôm sau) và không cho sửa đổi khi đã đến ngày hiệu lực. |
| 2 | UC03 - Áp dụng tỷ lệ mới | SRS ghi: "Khi mở lại màn hình dự toán, hệ thống tự động tính lại theo tỷ lệ mới nhất". | **LÀM GÃY LUỒNG CŨ (Blocker):** Vi phạm nguyên tắc bảo toàn số liệu. Nếu một dự toán đã trình ký vOffice hôm qua, hôm nay cấu hình đổi tỷ lệ mà mở ra xem lại bị nhảy số mới thì số liệu trên web sẽ lệch với file PDF đã ký trên vOffice! | **Blocker** | Khóa cứng số liệu: Dự toán đã Lưu hoặc Đã trình ký thì KHÔNG ĐƯỢC PHÉP tự động tính lại. Chỉ dự toán bấm "Tạo mới" mới áp dụng tỷ lệ mới. |
| 3 | UC01 - Phân quyền | SRS ghi: "Người dùng có quyền quản trị được cấu hình". | **MƠ HỒ / THIẾU AN TOÀN (Major):** Không chỉ rõ mã quyền trên hệ thống STMS là gì, dễ dẫn đến việc cấp nhầm quyền cho nhân viên kinh doanh tự sửa tỷ lệ lợi nhuận. | **Major** | Định nghĩa rõ mã quyền mới (ví dụ: `CN_CONFIG_BUDGET`), chỉ gán cho cấp Trưởng phòng Kinh doanh / Ban Giám đốc. |
| 4 | UC02 - Hiển thị thông báo | Khi tỷ lệ thay đổi, chỉ hiển thị thông báo popup trên màn hình. | **THIẾU LUỒNG NGOẠI LỆ (Minor):** Người dùng lỡ tay bấm tắt popup thì không biết tra cứu lịch sử thay đổi ở đâu. | **Minor** | Bổ sung tab "Lịch sử thay đổi cấu hình" (Ghi rõ ai sửa, sửa lúc nào, giá trị cũ -> giá trị mới). |

### ĐIỂM ĐÙN ĐẨY TRÁCH NHIỆM BỊ BẮT BÀI:
- Tại mục 2.3.2, SRS có câu: *"Đơn vị nghiệp vụ tự chịu trách nhiệm kiểm tra tính chính xác của tỷ lệ khi áp dụng vào quyết toán"*.
- 👉 **Phản biện:** Đơn vị yêu cầu chỉ chịu trách nhiệm nhập số liệu. Hệ thống của BP Nghiệp vụ thiết kế BẮT BUỘC phải có hàm validate: Tổng các tỷ lệ thành phần phải $= 100\%$, nếu $\neq 100\%$ thì hệ thống phải chặn không cho lưu, không thể đổ lỗi cho người dùng nhập sai!
```

---

## BƯỚC 3: DÙNG PROMPT 3 SINH PHIẾU YÊU CẦU (PYC) CHUẨN ĐỂ TRÌNH KÝ

Dựa trên kết quả ở Bước 1 và Bước 2, AI tự động điền vào mẫu PYC chuẩn Viettel Post (`04_Mau_PYC_Chuan_ViettelPost.md`). Bạn BA chỉ cần copy ra Word, in và trình ký:

* **Tên PYC:** Phiếu đề nghị nâng cấp tính năng Cấu hình Dự toán/Quyết toán linh hoạt trên Sàn Vận Tải.
* **In-Scope:** Xây dựng màn hình cấu hình tỷ lệ; validate tổng $= 100\%$; bổ sung trường ngày hiệu lực; áp dụng tỷ lệ mới cho dự toán tạo mới.
* **Out-of-Scope (Chốt chặn):** Không tính toán lại các dự toán/quyết toán đã ký vOffice trước ngày hiệu lực; không thay đổi quy trình xuất hóa đơn trên FICO.
* **Acceptance Criteria (AC):** Đã viết sẵn các kịch bản test chuẩn Given-When-Then cho bạn BA dùng để nghiệm thu UAT (Bước 9).

---

## BƯỚC 4: DÙNG PROMPT 4 SOẠN SẴN KỊCH BẢN PHẢN BIỆN LẠI ĐỘI IT

Khi BP Nghiệp vụ chat hỏi:  
> *"Này bạn BA, bên tôi thấy yêu cầu cấu hình này phức tạp quá. Bạn cho tôi biết cụ thể bảng CSDL nào đang lưu tỷ lệ cũ? Và nếu đơn hàng bị hủy thì API bên bạn định rollback thế nào?"*

Bạn BA đưa câu hỏi vào **Prompt 4**, AI soạn ngay câu trả lời:

> *"Chào anh/chị bên BP Nghiệp vụ,  
> Căn cứ theo **Quy trình chi tiết 6.1.2**:  
> 1. Về mặt nghiệp vụ (Ranh 1): Đơn vị yêu cầu đã xác định rõ tại Mục 3 của PYC: 'Khi đơn hàng bị hủy, dự toán gắn với đơn hàng đó sẽ tự động chuyển sang trạng thái Đã hủy và không được đưa vào Quyết toán'.  
> 2. Về mặt kỹ thuật CSDL và cơ chế rollback API: Đây là giải pháp kiến trúc hệ thống thuộc trách nhiệm phân tích tại **Bước 3 (Phân tích và đánh giá)** của BP Nghiệp vụ. Nhờ anh/chị chủ động khảo sát cấu trúc bảng của SVT và đưa ra phương án kỹ thuật tối ưu trong tài liệu SRS nhé. Rất mong nhận được bản SRS cập nhật từ anh/chị!"*

🎯 **Kết quả:** Bạn BA trả lời cực kỳ chuẩn mực, chuyên nghiệp, giữ vững ranh giới và khiến đối tác kỹ thuật phải nể phục!
