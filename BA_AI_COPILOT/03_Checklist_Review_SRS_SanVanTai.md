# BẢNG KIỂM TRA (CHECKLIST) RÀ SOÁT TÀI LIỆU SRS
## CHUYÊN BIỆT CHO HỆ THỐNG SÀN VẬN TẢI (SMART TMS) - VIETTEL POST

> **Mục đích:** Bộ tiêu chí giúp BA thẩm định nhanh bất kỳ tài liệu SRS nào do BP Nghiệp vụ / Đội IT gửi sang, phát hiện ngay các "lỗ hổng chết người" trước khi ký nháy hoặc chuyển sang Đội sản xuất phát triển.

---

## 1. KHUNG TIÊU CHÍ RÀ SOÁT CHUNG (5 NGUYÊN TẮC VÀNG)

| STT | Tiêu chí | Câu hỏi BA cần tự đặt ra khi đọc SRS | Đánh giá |
|:---:|---|---|:---:|
| **1** | **Bài toán gốc** | Chức năng trong SRS có giải quyết đúng khó khăn ban đầu của người dùng (Kinh doanh, Điều vận, Kế toán) hay đang "bôi" thêm việc phức tạp? | [ ] Đạt / [ ] Hở |
| **2** | **Tương thích ngược** | Tính năng mới có làm "chết" các đơn hàng, dự toán hoặc công nợ đang chạy dở dang trong quá khứ không? | [ ] Đạt / [ ] Hở |
| **3** | **Điểm chạm FICO/SAP** | Có làm sai lệch doanh thu, thiếu trường dữ liệu đồng bộ, hoặc vỡ quy trình xuất hóa đơn và gạch nợ trên FICO không? | [ ] Đạt / [ ] Hở |
| **4** | **Bẫy đùn đẩy** | Có điều khoản nào dùng từ mập mờ kiểu: *"Nghiệp vụ tự kiểm tra"*, *"Hệ thống sẽ cập nhật sau"*, *"Theo thỏa thuận riêng"* không? | [ ] Không / [ ] Có |
| **5** | **Độ phủ luồng ngoại lệ** | Khi mạng rớt, API timeout, người dùng bấm Hủy/Từ chối duyệt thì hệ thống xử lý thế nào? SRS có vẽ luồng không? | [ ] Đạt / [ ] Hở |

---

## 2. BẢNG KIỂM CHI TIẾT THEO TỪNG PHÂN HỆ NGHIỆP VỤ

### PHÂN HỆ 1: ĐƠN HÀNG, CHUYẾN XE & BÁO GIÁ (BƯỚC 1 & 2)
- [ ] **Báo giá & Dự kiến chi phí:** SRS mới có đảm bảo người dùng bắt buộc phải nhập đủ *Chi phí dự kiến* và *Báo giá khách hàng* trước khi duyệt giá không? (Nếu thiếu sẽ không ghi nhận được doanh thu/chi phí tạm tính).
- [ ] **Import Excel hàng loạt:** Nếu có chức năng Import đơn hàng hoặc chuyến xe, SRS có quy định:
  - Có file template mẫu chuẩn không?
  - Cơ chế validate khi file sai dòng tiêu đề hoặc sai định dạng số điện thoại/địa chỉ?
  - Có xuất file log ghi rõ dòng nào lỗi, lý do lỗi để user tải về sửa không?
- [ ] **Khóa đơn sau duyệt giá:** Sau khi đơn đã ở trạng thái "Đã duyệt giá", những trường thông tin nào bị KHÓA không cho sửa trực tiếp? Nếu muốn sửa có luồng "Hủy duyệt" hoặc "Yêu cầu điều chỉnh" không?

---

### PHÂN HỆ 2: DỰ TOÁN CHI PHÍ & DOANH THU (BƯỚC 3)
- [ ] **Cấu hình tỷ lệ Doanh thu - Chi phí - Lợi nhuận:** 
  - Khi thay đổi tỷ lệ cấu hình, SRS có quy định rõ tỷ lệ mới chỉ áp dụng cho các Dự toán TẠO MỚI sau ngày hiệu lực hay áp dụng cả cho dự toán cũ không?
  - Các dự toán đang ở trạng thái "Chờ duyệt vOffice" hoặc "Đã duyệt" có bị tự động nhảy lại số liệu không? (Tuyệt đối KHÔNG được tự nhảy làm sai lệch số liệu đã trình ký).
- [ ] **Gom đơn vào Dự toán:** Một đơn hàng có được phép nằm trong 2 dự toán khác nhau không? (SRS phải có cơ chế validate chặn gom trùng).
- [ ] **Tích hợp trình ký vOffice:** SRS có mô tả rõ: Người dùng phải "Lưu dự toán thành công" rồi mới cho phép bấm "Trình ký vOffice" không? Nếu vOffice trả về kết quả "Từ chối duyệt", dự toán quay về trạng thái nào?

---

### PHÂN HỆ 3: ĐIỀU PHỐI VẬN TẢI & HOÀN THÀNH CHUYẾN (BƯỚC 4 & 5 - STMS QLX)
- [ ] **Đồng bộ giữa SVT và STMS QLX:** Khi chuyến xe được tạo trên SVT và đẩy sang QLX để gán xe/tài xế, nếu gán xe thất bại hoặc đổi tài xế trên App, trạng thái trên SVT có được cập nhật thời gian thực (realtime) không?
- [ ] **Xác nhận hoàn thành chuyến:** Tài xế bấm "Hoàn thành chuyến" trên App di động thì điều kiện nào để SVT cho phép chuyển sang bước Lập Biên Bản Nghiệm Thu (BBNTKH)?

---

### PHÂN HỆ 4: BIÊN BẢN NGHIỆM THU KHÁCH HÀNG (BBNTKH - BƯỚC 6) - ⚠️ CỰC KỲ RỦI RO
- [ ] **Quy tắc bất khả biến:** BBNTKH sau khi duyệt và đồng bộ sang FICO thì **TUYỆT ĐỐI KHÔNG ĐƯỢC PHÉP HỦY HOẶC CHỈNH SỬA TRỰC TIẾP TRÊN SVT**. SRS mới có tuân thủ quy tắc này không?
- [ ] **Cơ chế điều chỉnh (Adjustment):** Nếu khách hàng khiếu nại sai số liệu sau khi BBNTKH đã sang FICO, SRS có thiết kế luồng "Lập BBNT điều chỉnh (tăng/giảm)" không? Hay lại để ngỏ cho can thiệp DB thủ công?
- [ ] **Timeout đồng bộ FICO:** Nếu sau 15 phút FICO không phản hồi mã tiếp nhận BBNTKH, hệ thống có đổi trạng thái "Lỗi đồng bộ FICO" và có nút "Đồng bộ lại (Retry)" cho user bấm không?

---

### PHÂN HỆ 5: HÓA ĐƠN & GHI NHẬN DOANH THU FICO / NOC / SAP (BƯỚC 7 & 8)
- [ ] **Trường dữ liệu bắt buộc:** Khi đẩy sang FICO để xuất hóa đơn, SRS có đảm bảo trường `Nguồn = SVT` luôn được truyền không? (Nếu thiếu trường này, kế toán tìm kiếm trên FICO sẽ không ra đơn).
- [ ] **Xuất hóa đơn tự động vs thủ công:** SRS có quy định rõ khi nào xuất tự động từ SVT, khi nào xuất thủ công trên FICO không?
- [ ] **Kiểm soát trùng lặp doanh thu:** SRS có đảm bảo tuyệt đối không còn luồng khai báo song song qua E2 $\rightarrow$ HR $\rightarrow$ NOC không? (Chỉ duy nhất nguồn SVT $\rightarrow$ FICO $\rightarrow$ NOC/SAP).
- [ ] **Hóa đơn điều chỉnh:** Nếu có điều chỉnh cước, SRS có validate bắt buộc phải chọn ít nhất 1 đơn hàng điều chỉnh không? (Giá trị âm = giảm, dương = tăng).

---

### PHÂN HỆ 6: QUẢN LÝ CÔNG NỢ & GẠCH NỢ (BƯỚC 9)
- [ ] **Công thức xác định lịch thu công nợ:** SRS có mô tả đúng: `Lịch thu công nợ = Ngày nhập doanh thu + Thời hạn thu công nợ cấu hình` không?
- [ ] **Job tự động (Batch Jobs):**
  - Job chạy 00:30 ngày 01 hàng tháng: Phân nhóm công nợ, tính tổng nợ tồn, nợ quá 3 tháng / 6 tháng?
  - Job chạy 08:00 hàng ngày: Bắn thông báo nhắc nợ theo cấu hình (qua SMS/Email/App)?
- [ ] **Gạch nợ từ FICO (`event_type = CLEARING`):** Khi FICO gạch nợ từng phần (khách trả trước một phần), hệ thống có cập nhật lũy kế số tiền đã thu và dừng nhắc nợ khi gạch đủ 100% không?
- [ ] **Chốt kế hoạch thu & Khóa sổ kỳ:** Hạn chốt ngày 05 hàng tháng. Nếu đơn vị quên không chốt, SRS có cơ chế "Hệ thống tự động chốt lúc 23:59 ngày 05" không?

---

### PHÂN HỆ 7: QUYẾT TOÁN ĐƠN HÀNG (BƯỚC 10)
- [ ] **Đối soát Doanh thu - Chi phí - Lợi nhuận:** Số liệu doanh thu lấy từ Hóa đơn FICO thực tế, chi phí lấy từ đâu? Có đối chiếu cảnh báo nếu Chi phí thực tế vượt quá Dự toán ban đầu không?
- [ ] **Trình ký vOffice:** Sau khi Lưu quyết toán thành công mới cho Trình ký. Khi vOffice duyệt xong, trạng thái đơn hàng trên SVT có chuyển thành "Đã đóng / Hoàn thành toàn trình" không?

---

## 3. MẪU BẢNG NHẬT KÝ REVIEW SRS (DÙNG ĐỂ GỬI LẠI BP NGHIỆP VỤ)

| STT | Mục / Use Case | Trang trong SRS | Hiện trạng (Theo HDSD) | Đề xuất trong SRS | Vấn đề / Rủi ro phát hiện | Mức độ | Yêu cầu BP Nghiệp vụ giải trình / sửa |
|:---:|---|:---:|---|---|---|:---:|---|
| 1 | UC01 - Cấu hình tỷ lệ | Tr.12 | Tỷ lệ dự toán áp dụng cố định theo biểu mẫu chi nhánh | Cho phép sửa tỷ lệ linh hoạt | Không quy định cách xử lý các dự toán đang lập dở dang | **Blocker** | Bổ sung rule: Tỷ lệ mới chỉ áp dụng cho dự toán tạo mới sau thời điểm hiệu lực. |
| 2 | UC03 - API Công nợ | Tr.25 | FICO gọi API SVT khi có thay đổi | Chưa mô tả trường hợp API timeout hoặc trả về HTTP 500 | Dữ liệu gạch nợ bị treo, hệ thống vẫn tiếp tục bắn tin nhắc nợ sai | **Major** | Bổ sung cơ chế Retry Job và bảng log theo dõi trạng thái đồng bộ API. |
| 3 | UC05 - Màn hình danh sách | Tr.38 | Phân quyền theo Chi nhánh / Tuyến | SRS ghi "Người dùng có quyền sẽ thấy dữ liệu" | Câu từ mơ hồ, không nêu rõ quyền mã gì (CN_...) | **Minor** | Định nghĩa rõ Ma trận phân quyền theo mã Role STMS hiện hành. |

*(Phân loại mức độ: **Blocker** = Nguy cơ vỡ hệ thống/sai số liệu kế toán, bắt buộc dừng lại không cho code; **Major** = Thiếu luồng ngoại lệ quan trọng; **Minor** = Cần chỉnh sửa mô tả giao diện/câu chữ).*
