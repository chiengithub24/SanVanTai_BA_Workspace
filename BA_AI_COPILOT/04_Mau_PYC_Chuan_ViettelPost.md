# TẬP ĐOÀN CÔNG NGHIỆP - VIỄN THÔNG QUÂN ĐỘI
## TỔNG CÔNG TY CỔ PHẦN BƯU CHÍNH VIETTEL

---

### PHIẾU ĐỀ NGHỊ YÊU CẦU (PYC)
### VỀ VIỆC PHÁT TRIỂN / NÂNG CẤP TÍNH NĂNG TRÊN HỆ THỐNG SÀN VẬN TẢI (SMART TMS)

* **Mã PYC:** `PYC_SVT_[MÃ_TÍNH_NĂNG]_[NĂM]` (Ví dụ: `PYC_SVT_DUTOAN_2026`)
* **Ngày lập:** `.../.../2026`
* **Đơn vị đề nghị (Ranh 1):** `[Tên Trung tâm / Ban / Chi nhánh yêu cầu]`
* **Người lập phiếu:** `[Họ và tên BA Đơn vị yêu cầu]`
* **Đơn vị phối hợp thực hiện:** 
  - Bộ phận Kế hoạch (Ranh 2 - Thẩm định & Điều phối)
  - Bộ phận Nghiệp vụ / Khối CNTT (Ranh 3 - Phân tích giải pháp & Viết SRS)
  - Bộ phận Sản xuất (Ranh 4 - Đội ngũ phát triển phần mềm)

---

## I. BỐI CẢNH, CĂN CỨ VÀ MỤC TIÊU YÊU CẦU

### 1.1. Bối cảnh và Thực trạng vận hành hiện tại (As-Is)
* Mô tả ngắn gọn quy trình vận hành hiện tại trên hệ thống Sàn Vận Tải liên quan đến tính năng đề xuất.
* Các tồn tại, khó khăn, bất cập thực tế của người dùng (Kinh doanh, BPVH, Kế toán) khi thao tác trên hệ thống hiện hành:
  - *Ví dụ: Việc áp dụng tỷ lệ chi phí cố định cho mọi đơn hàng vận tải nguyên chuyến dẫn đến sai lệch với thực tế từng cung đường, buộc kinh doanh và kế toán phải điều chỉnh thủ công ngoài hệ thống.*
  - *Ví dụ: Luồng đồng bộ trạng thái công nợ từ FICO về SVT chưa tức thời, gây khó khăn cho việc đôn đốc thu hồi nợ đến hạn.*

### 1.2. Căn cứ đề xuất
* Căn cứ định hướng kinh doanh dịch vụ Sàn Vận Tải của Tổng Công ty năm 2026.
* Căn cứ phản ánh của các Chi nhánh / Đơn vị vận hành tại cuộc họp giao ban ngày `.../.../2026`.
* Căn cứ Quy trình chi tiết 6.1.2 về Tiếp nhận và xử lý PYC phát triển / nâng cấp phần mềm.

### 1.3. Mục tiêu đạt được
* **Mục tiêu định tính:**
  - Chuẩn hóa và tự động hóa quy trình nghiệp vụ trên phần mềm, giảm thiểu tối đa các thao tác thủ công ngoài hệ thống.
  - Đảm bảo tính minh bạch, thống nhất số liệu xuyên suốt chu trình: `Tạo đơn -> Báo giá -> Dự toán -> Thực hiện xe -> BBNTKH -> Xuất HĐ FICO -> Gạch nợ -> Quyết toán`.
* **Mục tiêu định lượng:**
  - Rút ngắn thời gian lập và phê duyệt từ `... giờ` xuống `... phút`.
  - Triệt tiêu 100% rủi ro sai lệch số liệu doanh thu - công nợ giữa Sàn Vận Tải, FICO và NOC.

---

## II. PHẠM VI YÊU CẦU (SCOPE BOUNDARY - CHỐT CHẶN TRÁCH NHIỆM)

> ⚠️ **LƯU Ý CỦA BA:** Phần này là "chốt chặn" pháp lý quan trọng nhất để ngăn chặn BP Nghiệp vụ và Đội Dev đùn đẩy việc phát sinh hoặc tự ý kéo dài tiến độ.

### 2.1. Thuộc phạm vi thực hiện (In-Scope)
Liệt kê chính xác những gì hệ thống PHẢI LÀM trong đợt này:
1. Xây dựng màn hình cấu hình...
2. Điều chỉnh công thức tính toán tại bước...
3. Bổ sung trường thông tin... trên API đồng bộ với FICO.
4. Bổ sung quyền thao tác cho nhóm người dùng...

### 2.2. Không thuộc phạm vi thực hiện (Out-of-Scope)
Liệt kê rõ ràng những việc KHÔNG LÀM trong đợt này (chuyển sang giai đoạn sau nếu có nhu cầu):
1. Không thay đổi luồng phê duyệt vOffice hiện hành đối với các đơn hàng thông thường.
2. Không can thiệp sửa đổi cấu trúc dữ liệu của các đơn hàng đã đóng quyết toán trước ngày hiệu lực.
3. Không phát triển tính năng trên Mobile App tài xế (nếu chỉ nâng cấp trên Web Portal).

---

## III. YÊU CẦU NGHIỆP VỤ CHI TIẾT & TIÊU CHÍ NGHIỆM THU (ACCEPTANCE CRITERIA)

### 3.1. Yêu cầu chức năng (Functional Requirements)

#### Yêu cầu 1: [Tên chức năng, ví dụ: Cấu hình tỷ lệ Dự toán/Quyết toán linh hoạt]
* **Mô tả nghiệp vụ:** Người dùng có thẩm quyền (Quản lý/Lãnh đạo) được phép thiết lập bảng tỷ lệ doanh thu - chi phí định mức theo từng loại dịch vụ, từng đơn vị hoặc từng tuyến vận chuyển.
* **Quy tắc nghiệp vụ (Business Rules):**
  - **BR-01:** Tổng các tỷ lệ thành phần (Chi phí thuê ngoài + Chi phí nhiên liệu + Chi phí quản lý + Lợi nhuận định mức) phải bằng đúng 100%. Nếu $\neq 100\%$, hệ thống cảnh báo và không cho lưu.
  - **BR-02:** Mỗi bảng cấu hình phải có ngày bắt đầu hiệu lực (`Valid From`). Không cho phép 2 bảng cấu hình cùng đối tượng có khoảng thời gian hiệu lực chồng chéo nhau.
  - **BR-03 (Chuyển tiếp dữ liệu):** Tỷ lệ mới chỉ áp dụng cho các Dự toán được tạo mới sau thời điểm cấu hình có hiệu lực. Tuyệt đối không tự động tính lại các Dự toán đã lưu hoặc đã trình ký vOffice.

* **Tiêu chí nghiệm thu (Acceptance Criteria - BDD):**
  - **AC 1.1: Lưu cấu hình thành công khi dữ liệu hợp lệ**
    * *Given (Giả sử):* Người dùng đăng nhập tài khoản có quyền `Cấu hình Dự toán` và mở màn hình Thêm mới cấu hình.
    * *When (Khi):* Nhập đủ các trường bắt buộc, tổng tỷ lệ bằng 100%, chọn ngày hiệu lực từ ngày mai và nhấn `Lưu`.
    * *Then (Thì):* Hệ thống hiển thị thông báo "Thêm mới cấu hình thành công", bản ghi xuất hiện trong danh sách ở trạng thái `Hiệu lực` khi đến ngày.
  - **AC 1.2: Chặn lưu khi tổng tỷ lệ khác 100%**
    * *Given:* Người dùng đang nhập tỷ lệ trên form cấu hình.
    * *When:* Tổng tỷ lệ các khoản mục cộng lại bằng 95% và nhấn `Lưu`.
    * *Then:* Hệ thống không cho lưu, bôi đỏ các trường dữ liệu và hiển thị thông báo lỗi: *"Tổng tỷ lệ chi phí và lợi nhuận phải bằng đúng 100%"*.

*(BA bổ sung tiếp các Yêu cầu 2, 3... tương tự)*

---

### 3.2. Yêu cầu phi chức năng (Non-Functional Requirements)
* **Thời gian đáp ứng:** Mọi thao tác tìm kiếm, tính toán dự toán phải hoàn thành dưới **2 giây**.
* **Đồng bộ dữ liệu:** Thời gian đồng bộ dữ liệu sang SAP FICO / NOC không vượt quá **5 phút** kể từ khi sự kiện kích hoạt thành công.
* **Bảo mật & Phân quyền:** Phân quyền theo 2 lớp: Quyền thao tác tính năng (Menu, Button) và Quyền truy cập phạm vi dữ liệu (theo Đơn vị / Chi nhánh / Tuyến).

---

## IV. PHẠM VI ẢNH HƯỞNG & TÍCH HỢP HỆ THỐNG

| Hệ thống liên quan | Mức độ ảnh hưởng | Nội dung phối hợp kỹ thuật |
|---|:---:|---|
| **STMS - Sàn Vận Tải (Web)** | Trực tiếp | Xây dựng màn hình cấu hình, sửa logic tính toán dự toán/quyết toán. |
| **STMS - Quản Lý Xe (QLX)** | Gián tiếp | Nhận thông tin chuyến xe đã duyệt dự toán để gán xe. |
| **SAP FICO** | Trực tiếp | Đảm bảo gói tin BBNTKH và Hóa đơn gửi sang FICO không bị lỗi cấu trúc dữ liệu, giữ nguyên trường bắt buộc `Nguồn = SVT`. |
| **NOC / SAP ZBMS** | Theo dõi | Kiểm tra việc ghi nhận doanh thu và hạch toán bút toán không bị trùng lặp hoặc sai lệch số tiền. |
| **vOffice** | Tích hợp | Luồng trình ký duyệt Dự toán và Quyết toán không bị gián đoạn. |

---

## V. ĐỀ XUẤT PHÂN CÔNG TRÁCH NHIỆM THEO QUY TRÌNH 6.1.2

1. **Đơn vị đề nghị (Ranh 1 - Bạn BA):**
   - Chịu trách nhiệm cung cấp và làm rõ các bài toán nghiệp vụ, quy tắc tính toán (Mục III).
   - Thẩm định và ký xác nhận tài liệu đặc tả SRS do BP Nghiệp vụ lập.
   - Trực tiếp xây dựng kịch bản kiểm thử UAT và thực hiện nghiệm thu người dùng (Bước 9).
2. **Bộ phận Kế hoạch (Ranh 2):**
   - Thẩm định tính hợp lệ, khả thi và điều phối lộ trình triển khai PYC.
3. **Bộ phận Nghiệp vụ / Khối CNTT (Ranh 3):**
   - Khảo sát chi tiết hiện trạng CSDL và hệ thống, thiết kế giải pháp kỹ thuật, viết tài liệu SRS chi tiết (không đùn đẩy việc thiết kế cho Ranh 1).
   - Bàn giao SRS cho Đơn vị đề nghị thẩm định trước khi chuyển sang Đội sản xuất.
4. **Bộ phận Sản xuất (Ranh 4):**
   - Lập trình tính năng, kiểm thử nội bộ (Unit Test, Integration Test) và hỗ trợ triển khai hệ thống.

---

## VI. PHÊ DUYỆT CỦA CÁC BÊN LIÊN QUAN

| NGƯỜI LẬP PHIẾU | TRƯỞNG PHÒNG ĐƠN VỊ ĐỀ NGHỊ | LÃNH ĐẠO ĐƠN VỊ ĐỀ NGHỊ |
|:---:|:---:|:---:|
| *(Ký và ghi rõ họ tên)* | *(Ký và ghi rõ họ tên)* | *(Ký và ghi rõ họ tên)* |
| <br><br><br>**...** | <br><br><br>**...** | <br><br><br>**...** |
