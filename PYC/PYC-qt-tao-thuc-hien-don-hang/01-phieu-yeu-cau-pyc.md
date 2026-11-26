# TẬP ĐOÀN CÔNG NGHIỆP - VIỄN THÔNG QUÂN ĐỘI
## TỔNG CÔNG TY CỔ PHẦN BƯU CHÍNH VIETTEL

---

### PHIẾU ĐỀ NGHỊ YÊU CẦU (PYC)
### VỀ VIỆC XÂY DỰNG TÍNH NĂNG TẠO ĐƠN HÀNG & THỰC HIỆN ĐƠN HÀNG VẬN TẢI QUỐC TẾ TRÊN HỆ THỐNG SÀN VẬN TẢI (SMART TMS)

* **Mã PYC:** `PYC_SVT_QT_DONHANG_2026`
* **Ngày lập:** `25/11/2026`
* **Đơn vị đề nghị (Ranh 1):** `Phòng DVVHCP / Khối Nghiệp vụ Vận tải Quốc tế - Công ty LOG & Chi nhánh`
* **Tài liệu sở cứ đầu vào:**
  * `SRS/VẬN TẢI QUỐC TẾ.pdf` (Mục I - Quy trình tổng quan; Mục II.1 - Quản lý đơn hàng; Mục II.3 - Quản lý lộ trình và thực hiện đơn hàng)
  * `PYC/PYC-san-van-tai-quoc-te/raw/PYC Sàn vận tải dv Quốc tế.pdf` (Lưu đồ phục vụ đơn hàng Quốc tế, luồng trạng thái thực hiện đơn, chứng từ & cảnh báo)
  * `HDSD/HDSD hệ thống Sàn Vận tải.docx` (Luồng Đơn nội địa As-Is để đảm bảo không gãy luồng cũ)
* **Đơn vị phối hợp thực hiện (theo Quy trình 6.1.2):**
  * Bộ phận Kế hoạch (Ranh 2 - Thẩm định & Điều phối)
  * Bộ phận Nghiệp vụ / Khối CNTT (Ranh 3 - Khảo sát hệ thống, thiết kế giải pháp & Viết SRS chi tiết)
  * Bộ phận Sản xuất (Ranh 4 - Phát triển phần mềm & Kiểm thử nội bộ)

---

## I. BỐI CẢNH, CĂN CỨ VÀ MỤC TIÊU YÊU CẦU

### 1.1. Bối cảnh và Thực trạng vận hành hiện tại (As-Is)
* Hiện tại, hệ thống Sàn Vận Tải (`sanvantai.viettelpost.vn`) mới chỉ hỗ trợ luồng tạo đơn, báo giá và điều phối chuyến xe cho **Đơn nội địa** (`Menu > Đơn nội địa -> Quản lý đơn hàng`).
* Đối với hoạt động kinh doanh và vận hành **Vận tải Quốc tế (VTQT)**:
  1. Dữ liệu và thông tin phối hợp giữa Công ty LOG (Phòng Vận tải Quốc tế, Pricing, CS Quốc tế) và các Chi nhánh Bưu chính đang rời rạc, thực hiện thủ công/offline qua email, file Excel rời và tin nhắn, gây hạn chế trong việc chia sẻ nguồn lực và kiểm soát tiến độ.
  2. Biểu mẫu tạo đơn nội địa hiện hữu không đáp ứng được đặc thù đơn hàng quốc tế: thiếu phân loại Xuất khẩu / Nhập khẩu / Tại chỗ, thiếu 11 điều kiện giao hàng quốc tế (Incoterms), thiếu thông tin cảng/sân bay đi - đến - chuyển tải, mã HS code, quy cách container/CBM/nhiệt độ lạnh, khai báo Hải quan và 45 khoản mục phụ phí địa phương/quốc tế (Local charges) theo 10 đầu mục chi phí tài chính.
  3. Chưa có màn hình chuyên biệt để CS/Vận hành theo dõi toàn trình **lộ trình và thực hiện đơn hàng quốc tế** (Booking no, MBL/MAWB, HBL, ETD/ATD/ETA/ATA tại POL, Transit Port, POD, tình trạng thông quan, cấp lệnh giao hàng DO, thông báo hàng đến và cảnh báo mốc thời gian quan trọng).

### 1.2. Căn cứ đề xuất
* Căn cứ nhu cầu số hóa và quản lý toàn trình hoạt động kinh doanh dịch vụ Vận tải Quốc tế tại Tổng Công ty và Công ty LOG năm 2026.
* Căn cứ tài liệu mô tả yêu cầu `VẬN TẢI QUỐC TẾ.pdf` và hồ sơ đề xuất nghiệp vụ từ Phòng Vận tải Quốc tế / Công ty LOG.
* Căn cứ Quy trình chi tiết **6.1.2** về Tiếp nhận và xử lý PYC phát triển / nâng cấp phần mềm.

### 1.3. Mục tiêu đạt được
* **Mục tiêu định tính:**
  * Tách biệt và chuẩn hóa phân hệ `Đơn quốc tế` trên Web Portal Sàn Vận Tải, không làm ảnh hưởng đến luồng `Đơn nội địa` đang vận hành.
  * Số hóa xuyên suốt 2 mắt xích đầu vào của chu trình VTQT: **(1) Tiếp nhận nhu cầu - Tạo đơn - Báo giá** và **(2) Quản lý lộ trình - Thực hiện đơn hàng - Phát hành chứng từ vận hành**, tạo dữ liệu đầu vào sạch và đồng nhất cho các bước Dự toán, Nghiệm thu, Xuất hóa đơn FICO và Quyết toán.
  * Thiết lập cơ chế cảnh báo chủ động giúp CS/Kinh doanh kiểm soát mốc hàng chuyển tải và lấy vận đơn đúng hạn, hạn chế phát sinh phí lưu bãi/lưu container (DEM/DET).
* **Mục tiêu định lượng:**
  * 100% đơn hàng Vận tải Quốc tế (Xuất khẩu, Nhập khẩu, Tại chỗ) được khởi tạo, báo giá, theo dõi lộ trình và lưu vết tập trung trên Sàn Vận Tải thay cho theo dõi file rời.
  * Giảm thời gian tổng hợp thông tin báo giá và phát hành chứng từ vận tải (HBL, Thông báo hàng đến, Lệnh giao hàng DO) từ thao tác thủ công nhiều file xuống thao tác trực tiếp và xuất PDF ngay trên hệ thống.

---

## II. PHẠM VI YÊU CẦU (SCOPE BOUNDARY - CHỐT CHẶN TRÁCH NHIỆM)

> ⚠️ **LƯU Ý CỦA BA (RANH 1):** Phần In-Scope và Out-of-Scope là ranh giới pháp lý để kiểm soát phạm vi phát triển của PYC này, tránh phát sinh/phình phạm vi hoặc đùn đẩy sang các phân hệ chưa hoàn thiện nghiệp vụ.

### 2.1. Thuộc phạm vi thực hiện (In-Scope)
Xây dựng phân hệ `Menu -> Đơn quốc tế` trên Web Portal STMS - Sàn Vận Tải cho **02 nhóm chức năng chính**:

1. **Nhóm chức năng 1: Quản lý & Tạo đơn hàng, Báo giá Quốc tế (`Menu -> Đơn quốc tế -> Quản lý đơn hàng -> Tạo đơn`)**
   * Form tạo/chỉnh sửa đơn hàng Quốc tế gồm 5 khối thông tin:
     1. Thông tin Chung & Khách hàng (tự động Sales/Đơn vị, chọn/nhập Khách hàng, Mã KH, Nhóm KH, Hồ sơ đính kèm, hỗ trợ SĐT khách hàng quốc tế 11 số).
     2. Tuyến đường và chặng vận chuyển Quốc tế (cho phép thêm/xóa nhiều tuyến, chọn nhiều loại hình vận tải, chọn 1 hình thức Xuất khẩu/Nhập khẩu/Tại chỗ, điểm đi/đến & quốc gia đi/đến, thời gian dự kiến, transit time).
     3. Chi tiết hàng hóa và quy cách Quốc tế (Loại hàng, Tên thương mại, HS code, Gross W, Net W, DxRxC, CBM, Số lượng kiện/container, Nhiệt độ bảo quản hàng lạnh).
     4. Điều kiện thương mại (11 loại Incoterms) và yêu cầu vận chuyển (Pickup/Delivery Address có ràng buộc theo Incoterms, Hãng vận chuyển chỉ định, Giá đề xuất của khách hàng).
     5. Khai báo Hải quan và dịch vụ phụ trợ (tùy chọn mở luồng Hải quan + các trường bắt buộc khi tích chọn; mức độ thông quan Đỏ/Vàng/Xanh; dịch vụ phụ: Kiểm dịch, C/O, xin giấy phép, thanh lý tờ khai...).
   * Chức năng **Yêu cầu báo giá & Phản hồi báo giá Quốc tế** theo cấu trúc mới: mặc định hiển thị thông tin Doanh thu, cho phép CS/Pricing thêm nhiều dòng Doanh thu và Chi phí/Phụ phí (Local charges) theo danh mục chuẩn hóa từ 10 đầu mục chi phí tài chính (Đường biển, Đường không, Đường sắt, Đường bộ, Hải quan, Khác; có nhận diện chi phí đối tác nước ngoài không hóa đơn). Hỗ trợ luồng duyệt nhanh nếu CS đồng ý `Giá đề xuất khách hàng`.
2. **Nhóm chức năng 2: Quản lý lộ trình và Thực hiện đơn hàng Quốc tế**
   * Tự động khởi tạo bản ghi thực hiện đơn hàng ở trạng thái `Cần thực hiện` sau khi hoàn tất đặt đơn / chốt giá và chuyển sang màn hình **Quản lý lộ trình và Thực hiện đơn hàng Quốc tế** (song song với màn Quản lý lộ trình theo hiện trạng).
   * Bảng chi tiết 30 trường thông tin quản lý lộ trình & thực hiện đơn hàng quốc tế (Định danh `REF`, `Ex-im`, nhân sự `Pricing PIC`/`CS PIC`/`Sale PIC`, `Volume`, các mốc `POL`/`Transit port`/`POD` với `ETD`/`ATD`/`ETA`/`ATA`, `O/F`, `Carrier`, `Agency/FWD`, `Booking no`, `MBL no`, `HBL no`, `BL status`, `Số tờ khai`/`Ngày tờ khai`/`Ngày thông quan`, `Note`).
   * Quản lý vòng đời trạng thái thực hiện đơn (`Cần thực hiện` $\rightarrow$ `Đang thực hiện` $\rightarrow$ `Hoàn thành`) và khóa chỉnh sửa khi đã `Hoàn thành` (cơ chế mở khóa phải qua phê duyệt).
   * Danh sách theo dõi, thống kê số lượng theo trạng thái, tìm kiếm/bộ lọc đa tiêu chí (18 cột hiển thị), hỗ trợ Import/Export dữ liệu theo đơn hàng.
   * Phát hành và xuất PDF chứng từ tác nghiệp trực tiếp trên màn Thực hiện đơn hàng: `Tạo vận đơn phụ (HBL)` (đối với đơn Xuất khẩu); `Tạo thông báo hàng đến` và `Tạo lệnh giao hàng (DO)` (đối với đơn Nhập khẩu).
   * Cơ chế **Cảnh báo chủ động theo Mã đơn hàng** đối với mốc sắp đến cảng/sân bay chuyển tải và mốc lấy vận đơn.

### 2.2. Không thuộc phạm vi thực hiện (Out-of-Scope)
Các nội dung sau **KHÔNG thực hiện** trong PYC này (sẽ tách thành PYC/giai đoạn riêng hoặc giữ nguyên hiện trạng):
1. **Không** xây dựng/chỉnh sửa Module **Quản lý đối tác quốc tế** (Mục II.2 trong `VẬN TẢI QUỐC TẾ.pdf`: thêm/import đối tác nước ngoài, tài khoản ngân hàng SWIFT/IBAN, bỏ qua tab năng lực pháp lý). *Đơn hàng quốc tế trong PYC này kế thừa danh mục Đối tác hiện có hoặc trường text đối với đối tác chưa kết nối, và sẽ đồng bộ danh mục khi Module Đối tác hoàn thiện.*
2. **Không** xây dựng/chỉnh sửa Module **Quản lý Dự toán - Quyết toán Quốc tế** (Mục II.4 trong `VẬN TẢI QUỐC TẾ.pdf`: cấu trúc form giải trình doanh thu - chi phí - lợi nhuận dương, trình ký vOffice dự toán/quyết toán).
3. **Không** xây dựng/chỉnh sửa phân hệ **Quản lý Biên bản nghiệm thu (BBNTKH)**, **Quản lý Chuyến xe (STMS QLX)** *(trong tài liệu nguồn đang ghi "Sẽ tiếp tục thu thập")*.
4. **Không** thay đổi quy trình xuất hóa đơn điện tử trên **SAP FICO**, đối soát doanh thu **NOC / SAP ZBMS** và quản lý công nợ.
5. **Không** can thiệp, sửa đổi giao diện, công thức hoặc luồng xử lý của **Đơn nội địa** (`Menu > Đơn nội địa`).
6. **Không** phát triển tính năng trên **Mobile App tài xế**; toàn bộ thao tác của PYC này thực hiện trên Web Portal Sàn Vận Tải.

---

## III. YÊU CẦU NGHIỆP VỤ CHI TIẾT & TIÊU CHÍ NGHIỆM THU (ACCEPTANCE CRITERIA)

### 3.1. Yêu cầu chức năng (Functional Requirements)

---

#### Yêu cầu 1: Tạo đơn hàng Vận tải Quốc tế (`Menu -> Đơn quốc tế -> Quản lý đơn hàng -> Tạo đơn`)

* **Mô tả nghiệp vụ:** Cho phép Nhân viên kinh doanh (Sales) khởi tạo đơn hàng Vận tải Quốc tế với đầy đủ thông tin đặc thù (khách hàng, nhiều tuyến/phương thức vận tải, hàng hóa & mã HS, Incoterms, khai báo Hải quan và dịch vụ phụ).
* **Quy tắc nghiệp vụ (Business Rules):**
  * **BR-DH-01 (Tự động điền thông tin người tạo):** Hệ thống tự động lấy và hiển thị `Nhân viên kinh doanh (Sales)` và `Đơn vị chủ quản` theo tài khoản user đang đăng nhập; hỗ trợ chọn/tìm kiếm `Khách hàng` từ danh sách đã khai báo (hỗ trợ SĐT khách hàng quốc tế 11 số) và tự động hiển thị `Nhóm khách hàng` khi đã có `Mã khách hàng`.
  * **BR-DH-02 (Ràng buộc tuyến và phương thức vận tải):**
    * Cho phép Thêm/Xóa nhiều tuyến trong một đơn hàng.
    * Tại mỗi tuyến: `Loại hình vận tải` (Đường thủy/biển, Đường bộ, Đường sắt, Đường hàng không) là bắt buộc và **cho phép chọn nhiều**.
    * `Hình thức hàng hóa` là bắt buộc và **chỉ được chọn 1** trong 3 giá trị: `Xuất khẩu`, `Nhập khẩu`, `Tại chỗ` (*Tại chỗ* áp dụng cho khách hàng nước ngoài nhưng vận chuyển nội địa).
    * `Điểm đi`, `Quốc gia đi`, `Điểm đến`, `Quốc gia đến`, `Thời gian dự kiến đi` là bắt buộc. Địa chỉ quốc tế hỗ trợ khai báo tối thiểu đến cấp tỉnh/thành phố (hoặc cảng/sân bay); cấp xã/phường là tùy chọn nếu có.
  * **BR-DH-03 (Quy cách hàng hóa Quốc tế):** Bắt buộc nhập `Loại hàng hóa`, `Chi tiết nội dung hàng`, `Mã HS (HS code)`, `Trọng lượng Gross (Gross W)`, `Kích thước 3 chiều (DxRxC)`, `Thể tích (CBM)`, `Số lượng kiện`. Các trường `Trọng lượng Net (Net W)` và `Nhiệt độ bảo quản` (°C / % thông gió cho hàng lạnh) là không bắt buộc.
  * **BR-DH-04 (Điều kiện thương mại Incoterms 11 loại):**
    * `Điều kiện giao hàng (terms)` là bắt buộc và chỉ cho chọn **1 trong 11 loại Incoterms** (`EXW`, `FCA`, `FAS`, `FOB`, `CFR`, `CIF`, `CPT`, `CIP`, `DAP`, `DPU`, `DDP`).
    * Ràng buộc có điều kiện: Khi chọn `EXW` hoặc `FCA` $\rightarrow$ bắt buộc nhập `Điểm lấy hàng (Pickup Address)`. Khi chọn `DAP` hoặc `DDP` $\rightarrow$ bắt buộc nhập `Điểm trả hàng (Delivery Address)`.
    * Lưu ý chuẩn hóa form: Loại bỏ trường `Quốc gia đến` bị khai báo lặp ở Khối Điều kiện thương mại (đã có ở Khối Tuyến đường).
  * **BR-DH-05 (Khai báo Hải quan & Dịch vụ phụ trợ):**
    * Khi người dùng tích chọn `Khai báo Hải quan`: hệ thống bắt buộc nhập 3 trường `Tên / Mã HS Hải quan`, `Tỉnh mở tờ khai`, `Chi cục Hải quan`; các trường `Mức độ thông quan` (Đỏ/Vàng/Xanh) và `Ghi chú Hải quan` là tùy chọn.
    * Khi người dùng chọn các dịch vụ phụ khác (gợi ý: `Kiểm dịch`, `C/O`, `Xin giấy phép`, `Thanh lý tờ khai`, khác): thông tin các dịch vụ phụ này phải được truyền và hiển thị đầy đủ sang màn hình Thực hiện đơn hàng.
  * **BR-DH-06 (Bảo toàn luồng nội địa hiện hành):** Việc tạo, sửa hoặc hủy đơn hàng Quốc tế tại `Menu -> Đơn quốc tế` tuyệt đối không ảnh hưởng đến danh sách, mã đơn và quy tắc xử lý của `Menu -> Đơn nội địa`.

* **Tiêu chí nghiệm thu (Acceptance Criteria - BDD):**
  * **AC 1.1: Tạo mới đơn hàng Quốc tế hợp lệ**
    * *Given:* Nhân viên kinh doanh đã đăng nhập hệ thống và truy cập `Menu -> Đơn quốc tế -> Quản lý đơn hàng -> Tạo đơn`.
    * *When:* Người dùng chọn Khách hàng, nhập đủ thông tin 1 tuyến (chọn nhiều loại hình: `Đường thủy` + `Đường bộ`, Hình thức: `Xuất khẩu`, Điểm đi/đến, Quốc gia đi/đến, Thời gian dự kiến đi), nhập đủ thông tin hàng hóa & mã HS, chọn term `FOB`, không tích Khai báo Hải quan và nhấn lưu/gửi yêu cầu.
    * *Then:* Hệ thống lưu đơn hàng Quốc tế thành công, sinh mã đơn hàng theo quy cách đơn quốc tế (`YYMMXXXX`, ví dụ `25010001`), không xuất hiện lẫn trong danh sách Đơn nội địa.
  * **AC 1.2: Ràng buộc bắt buộc địa chỉ lấy/trả hàng theo điều kiện Incoterms**
    * *Given:* Người dùng đang tạo đơn hàng Quốc tế trên form Tạo đơn.
    * *When:* Người dùng chọn `Điều kiện giao hàng (terms)` là `EXW` (hoặc `FCA`) nhưng để trống `Điểm lấy hàng (Pickup Address)` và nhấn Lưu/Gửi.
    * *Then:* Hệ thống chặn lưu, đánh dấu lỗi và thông báo bắt buộc nhập `Điểm lấy hàng (Pickup Address)`. *(Tương tự chặn lưu khi chọn `DAP`/`DDP` mà bỏ trống `Điểm trả hàng (Delivery Address)`).*
  * **AC 1.3: Ràng buộc thông tin khi tích chọn Khai báo Hải quan**
    * *Given:* Người dùng đang tạo đơn hàng Quốc tế và tích chọn `Khai báo Hải quan`.
    * *When:* Người dùng bỏ trống một trong các trường `Tên / Mã HS Hải quan`, `Tỉnh mở tờ khai`, hoặc `Chi cục Hải quan` và nhấn Lưu/Gửi.
    * *Then:* Hệ thống chặn thao tác, highlight trường còn thiếu và yêu cầu bổ sung đủ 3 thông tin hải quan bắt buộc.

---

#### Yêu cầu 2: Báo giá & Phụ phí Địa phương (Local Charges) cho Đơn hàng Quốc tế

* **Mô tả nghiệp vụ:** Đáp ứng luồng trao đổi báo giá đa chiều giữa Kinh doanh, Pricing (chặng quốc tế/hãng tàu/airlines/co-loader), CS nội địa (chặng nội địa nếu có) và Khách hàng theo cấu trúc khoản mục chi phí tài chính đặc thù của Vận tải Quốc tế.
* **Quy tắc nghiệp vụ (Business Rules):**
  * **BR-BG-01 (Luồng giá đề xuất của khách hàng):**
    * Nếu Kinh doanh nhập `Giá đề xuất khách hàng` trên đơn hàng và CS/Pricing **Đồng ý** với giá đề xuất $\rightarrow$ đơn hàng chuyển trạng thái đã chốt/duyệt giá, không phải thực hiện vòng lặp báo giá lại.
    * Nếu không có giá đề xuất hoặc CS/Pricing **Không đồng ý** giá đề xuất $\rightarrow$ đơn hàng chuyển sang luồng báo giá chi tiết để Pricing (chặng quốc tế) và CS nội địa (chặng nội địa nếu có) phản hồi giá.
  * **BR-BG-02 (Cấu trúc Doanh thu & Chi phí linh hoạt):**
    * Trên màn hình Báo giá quốc tế, mặc định hiển thị các dòng thông tin **Doanh thu**.
    * Cho phép người dùng (Sales / CS / Pricing) chủ động **thêm/xóa nhiều dòng Doanh thu và Chi phí khác** theo nhu cầu thực tế từng đơn hàng.
  * **BR-BG-03 (Danh mục 10 đầu mục chi phí tài chính & Local charges):**
    * Danh mục chi phí lựa chọn trong báo giá phải bao gồm đầy đủ nhóm chi phí theo từng phương thức:
      * *I. Vận chuyển quốc tế:* Đường biển, Đường không, Đường sắt, Đường bộ (hỗ trợ gắn nhãn/ghi chú `Chi phí vận tải quốc tế qua đại lý $` cho đối tác nước ngoài không có hóa đơn).
      * *II.1. Phụ phí Đường biển:* LSS, THC, CIC, ISF, Phí lệnh giao hàng, Phụ phí đầu nước ngoài (Facility), Phí chuyển chứng từ đầu nước ngoài (Courier-agent), Door Delivery, Phí EXW, CFS fee, EBS, FAF, CAF, COD, PCS, PSS, Phí cắm điện container lạnh, Bill fee, Seal fee, AFR, ENS, AMS, Telex, DEM, DET, Phụ phí trả lại container (RR), Nâng hạ, Kéo cont kiểm hóa.
      * *II.2. Phụ phí Đường không:* FSC, SSC, WSC, X-ray fee, Storage (lưu kho), AWB, AMS, Phí DO (hàng nhập).
      * *III. Các phí khác:* Vận chuyển nội địa từ kho KH đến sân bay/cảng; Dịch vụ hun trùng, khử khuẩn.
    * *Lưu ý chuẩn hóa danh mục:* Khi thiết kế danh mục chuẩn, BP Nghiệp vụ cần gộp/khử trùng lặp các mục ghi trùng trong tài liệu gốc (LSS, Storage) và bỏ dòng trống.
  * **BR-BG-04 (Xác nhận báo giá với Khách hàng):** Sau khi Pricing/CS phản hồi báo giá, Kinh doanh gửi báo giá cho khách hàng (ghi nhận kết quả Khách hàng Đồng ý hoặc Từ chối để quay lại điều chỉnh báo giá; trường hợp đặc thù báo giá vận chuyển có thể lưu đính kèm làm căn cứ thay thế hợp đồng vận chuyển).

* **Tiêu chí nghiệm thu (Acceptance Criteria - BDD):**
  * **AC 2.1: Phê duyệt nhanh khi CS/Pricing đồng ý Giá đề xuất khách hàng**
    * *Given:* Đơn hàng Quốc tế có nhập `Giá đề xuất khách hàng` (ví dụ `1,250 USD / Cont 20'DC`) và được gửi lên hệ thống.
    * *When:* Tài khoản có quyền CS/Pricing mở báo giá đơn hàng và chọn `Đồng ý` với giá đề xuất.
    * *Then:* Hệ thống xác nhận hoàn tất bước chốt giá mà không yêu cầu nhập lại bảng chi tiết báo giá từ đầu, cập nhật trạng thái sẵn sàng cho bước tiếp theo.
  * **AC 2.2: Thêm dòng Doanh thu và Phụ phí Local charges trên Báo giá Quốc tế**
    * *Given:* Đơn hàng Quốc tế ở trạng thái chờ báo giá, người dùng có quyền CS/Pricing mở màn hình Phản hồi báo giá.
    * *When:* Người dùng kiểm tra thông tin Doanh thu mặc định, bấm thêm dòng chi phí từ danh mục chuẩn (ví dụ: `Cước vận chuyển quốc tế đường biển`, `Phí THC`, `Phí LSS`, `Phí Bill fee`), nhập đơn giá (bao gồm cả dòng đánh dấu đối tác nước ngoài không có hóa đơn) và bấm `Gửi báo giá`.
    * *Then:* Hệ thống lưu đầy đủ các dòng doanh thu/chi phí đã nhập, tính tổng chính xác và chuyển đơn về cho Nhân viên kinh doanh ở trạng thái `Đã báo giá` để báo giá khách hàng.

---

#### Yêu cầu 3: Quản lý lộ trình và Thực hiện đơn hàng Quốc tế

* **Mô tả nghiệp vụ:** Khi đơn hàng Quốc tế hoàn tất bước đặt đơn / chốt phương án thực hiện (và được cấp Booking), hệ thống tự động tạo bản ghi tại màn hình **Quản lý lộ trình và Thực hiện đơn hàng Quốc tế** để CS/Vận hành theo dõi toàn bộ lộ trình thực tế, chứng từ và hoàn thành đơn hàng.
* **Quy tắc nghiệp vụ (Business Rules):**
  * **BR-TH-01 (Khởi tạo tự động & kế thừa dữ liệu):**
    * Sau khi đặt đơn thành công, hệ thống tự động sinh 01 bản ghi tại màn hình Quản lý lộ trình và **01 bản ghi mới tại màn Thực hiện đơn hàng Quốc tế** với trạng thái khởi tạo là **`Cần thực hiện`**.
    * Tự động kế thừa dữ liệu từ màn Tạo đơn (`Ex-im`, `REF`, `Pricing PIC`, `CS PIC`, `Sale PIC`, `CN Tỉnh`, `Customer`, `Volume`, `POL`/`POD`, `ETD POL`, `ETA POD`, thông tin dịch vụ phụ/hải quan, số tờ khai/hồ sơ nếu đã có).
    * *Lưu ý chuẩn hóa định nghĩa trường:* Trường `ETA POD` phải thể hiện đúng là `Ngày/giờ dự kiến tàu/máy bay cập cảng đến` (khắc phục lỗi copy mô tả của `ATD Transit port` trong tài liệu nguồn).
  * **BR-TH-02 (Luồng trạng thái thực hiện đơn hàng & Khóa chỉnh sửa):**
    * **`Cần thực hiện` $\rightarrow$ `Đang thực hiện`:** Người thực hiện mở chi tiết đơn hàng, điền đầy đủ các trường bắt buộc (`Ex-im`, `REF`, `Pricing PIC`, `CS PIC`, `Sale PIC`, `Customer`, `Volume`, `POL Country`, `POD Country`, `ETD POL`, `ATD POL`, `Ngày thực tế chạy`, `Người thực hiện`, `Ngày đến cảng/sân bay chuyển tải` nếu có chặng chuyển tải) và bấm **`Gửi`**.
    * **`Đang thực hiện` $\rightarrow$ `Hoàn thành`:** Tại trạng thái `Đang thực hiện`, hiển thị nút `Xem` (cho phép cập nhật bổ sung `ATA Transit port`, `ETD/ATD Transit port`, `ETA/ATA POD`, `O/F`, `Carrier`, `Agency/FWD`, `Booking no`, `MBL no`, `HBL no`, `BL status`, `Số tờ khai`, `Ngày tờ khai`, `Ngày thông quan`, `Lệnh giao hàng`, `Note`) và nút **`Hoàn thành`**.
    * **Quy tắc khóa dữ liệu sau Hoàn thành:** Khi người dùng bấm `Hoàn thành`, đơn hàng chuyển trạng thái `Hoàn thành` và **KHÓA toàn bộ chức năng chỉnh sửa thông tin đơn hàng**. Nếu phát sinh nhu cầu sửa đổi sau khi đã Hoàn thành, bắt buộc phải gửi yêu cầu và có **cấp phê duyệt** mở khóa/duyệt sửa.
  * **BR-TH-03 (Tra cứu, Thống kê & Import/Export):**
    * Màn hình danh sách hiển thị thanh đếm số lượng đơn theo từng trạng thái (`Booking`, `Cần thực hiện`, `Đang thực hiện`, `Tạo chứng từ`, `Hoàn thành`).
    * Bảng danh sách hiển thị đầy đủ 18 cột thông tin (Mã đơn hàng, Mã - tên KH, Ngày tạo, Trạng thái, Sale, CS thực hiện, Tổng trọng lượng, Số lượng, Cảng XK, Nước XK, Cảng NK, Nước NK, Ngày dự kiến chạy, Ngày thực tế chạy, Ngày dự kiến đến, Ngày thực tế đến, Dịch vụ vận chuyển, Ghi chú) kèm bộ lọc tìm kiếm theo từng tiêu chí tương ứng.
    * Hỗ trợ `Import` và `Export` file dữ liệu tương ứng với danh sách/từng đơn hàng.

* **Tiêu chí nghiệm thu (Acceptance Criteria - BDD):**
  * **AC 3.1: Khởi tạo đơn ở màn Thực hiện đơn hàng Quốc tế**
    * *Given:* Nhân viên kinh doanh hoàn tất đặt đơn hàng Quốc tế có đầy đủ thông tin khách hàng, tuyến `Cảng Thượng Hải (China) -> Hải Phòng (Viet Nam)`, dịch vụ phụ `Kiểm dịch`.
    * *When:* Đơn hàng chuyển sang giai đoạn thực hiện.
    * *Then:* Màn hình `Thực hiện đơn hàng Quốc tế` tự động xuất hiện 01 bản ghi ở trạng thái `Cần thực hiện`, kế thừa đúng thông tin khách hàng, tuyến cảng đi/đến, ngày dự kiến đi/đến và hiển thị đầy đủ dịch vụ phụ `Kiểm dịch`.
  * **AC 3.2: Chuyển trạng thái Cần thực hiện sang Đang thực hiện**
    * *Given:* Có 01 đơn hàng Quốc tế ở trạng thái `Cần thực hiện` và người dùng (CS thực hiện) mở chi tiết đơn.
    * *When:* Người dùng nhập đủ các trường bắt buộc (`ATD POL`, `Ngày thực tế chạy`, `Người thực hiện`...) và bấm nút `Gửi`.
    * *Then:* Trạng thái đơn chuyển thành `Đang thực hiện`, bộ đếm số lượng trạng thái trên màn hình danh sách tự động giảm 1 ở `Cần thực hiện` và tăng 1 ở `Đang thực hiện`.
  * **AC 3.3: Khóa chỉnh sửa khi đơn hàng chuyển trạng thái Hoàn thành**
    * *Given:* Đơn hàng Quốc tế đang ở trạng thái `Đang thực hiện`.
    * *When:* Người dùng bấm nút `Hoàn thành` và xác nhận hoàn thành đơn hàng.
    * *Then:* Trạng thái đơn chuyển thành `Hoàn thành`; các trường thông tin chi tiết đơn hàng chuyển sang chế độ chỉ đọc (Read-only), không cho phép người dùng thường chỉnh sửa nếu chưa có phê duyệt từ cấp có thẩm quyền.

---

#### Yêu cầu 4: Phát hành chứng từ XNK & Hệ thống Cảnh báo chủ động trên đơn hàng Quốc tế

* **Mô tả nghiệp vụ:** Hỗ trợ CS/Vận hành phát hành nhanh các chứng từ đặc thù ngay tại đơn hàng đang thực hiện (đồng thời lưu vết trên hệ thống) và nhận cảnh báo tự động trước các mốc thời gian tới hạn để không trễ lấy vận đơn hoặc trễ xử lý hàng chuyển tải.
* **Quy tắc nghiệp vụ (Business Rules):**
  * **BR-CT-01 (Sinh chứng từ theo loại hình Xuất khẩu / Nhập khẩu):**
    * Đối với đơn hàng **Xuất khẩu (`Exp`)**: Hiển thị thao tác **`Tạo vận đơn phụ`** (`HBL`). Khi bấm vào, hiển thị form nhập theo `Mẫu Vận đơn phụ`, sau khi bấm tạo $\rightarrow$ hệ thống **tự động Lưu thông tin** gắn với đơn hàng và cho phép **xuất file PDF**.
    * Đối với đơn hàng **Nhập khẩu (`Imp`)**: Hiển thị thao tác **`Tạo thông báo hàng đến`** và **`Tạo lệnh giao hàng`**. Khi bấm vào từng nút, hiển thị form nhập theo mẫu tương ứng (`Mẫu Thông báo hàng đến`, `Mẫu Lệnh giao hàng`), sau khi bấm tạo $\rightarrow$ hệ thống **tự động Lưu thông tin** gắn với đơn hàng và cho phép **xuất file PDF**.
  * **BR-CB-01 (Cảnh báo tàu/hàng sắp đến cảng chuyển tải):** Hệ thống tự động sinh **CẢNH BÁO** kèm `Mã đơn hàng` **trước 7 ngày** so với `Ngày đến cảng/sân bay chuyển tải` đã nhập trên đơn hàng.
  * **BR-CB-02 (Cảnh báo mốc lấy vận đơn):**
    * Đối với lô hàng có tổng thời gian vận chuyển dự kiến **> 20 ngày**: Cảnh báo lấy vận đơn **trước 7 ngày** so với `Ngày dự kiến đến (ETA POD)`.
    * Đối với lô hàng có tổng thời gian vận chuyển dự kiến **< 5 ngày**: Cảnh báo lấy vận đơn **trước 3 ngày** so với `Ngày dự kiến đến (ETA POD)`.
    * *(Lưu ý nghiệp vụ cần làm rõ với ĐV yêu cầu trong Bước 3: Khoảng lô hàng có thời gian vận chuyển từ `5 đến 20 ngày` áp dụng ngưỡng cảnh báo 3 ngày hay 7 ngày để tránh sót cảnh báo).*

* **Tiêu chí nghiệm thu (Acceptance Criteria - BDD):**
  * **AC 4.1: Tạo và xuất PDF Vận đơn phụ (HBL) cho đơn Xuất khẩu**
    * *Given:* Đơn hàng Quốc tế có `Ex-im = Exp` đang ở màn hình Thực hiện đơn hàng.
    * *When:* Người dùng bấm `Tạo vận đơn phụ`, điền đầy đủ thông tin trên form `Mẫu Vận đơn phụ` và bấm Xác nhận/Tạo.
    * *Then:* Hệ thống lưu thông tin Vận đơn phụ vào đơn hàng và cho phép tải về/xuất file PDF đúng định dạng mẫu.
  * **AC 4.2: Tạo và xuất PDF Thông báo hàng đến / Lệnh giao hàng cho đơn Nhập khẩu**
    * *Given:* Đơn hàng Quốc tế có `Ex-im = Imp` đang ở màn hình Thực hiện đơn hàng.
    * *When:* Người dùng lần lượt thực hiện `Tạo thông báo hàng đến` và `Tạo lệnh giao hàng` theo mẫu biểu quy định.
    * *Then:* Hệ thống hiển thị đúng popup/màn hình theo từng loại chứng từ (không hiển thị nhầm sang nút `Tạo vận đơn phụ` của hàng xuất), lưu dữ liệu thành công và xuất file PDF tương ứng.
  * **AC 4.3: Cảnh báo tự động mốc đến cảng chuyển tải và mốc lấy vận đơn**
    * *Given:* Có 02 đơn hàng đang thực hiện: Đơn A có `Ngày đến cảng chuyển tải` cách ngày hiện tại đúng 7 ngày; Đơn B có thời gian vận chuyển = 25 ngày (> 20 ngày) và `ETA POD` cách ngày hiện tại đúng 7 ngày.
    * *When:* Hệ thống chạy tiến trình kiểm tra/hiển thị cảnh báo hàng ngày.
    * *Then:* Hệ thống hiển thị cảnh báo đúng cho `Mã đơn hàng A` (cảnh báo hàng sắp đến cảng chuyển tải) và `Mã đơn hàng B` (cảnh báo lấy vận đơn) gửi tới CS/người thực hiện đơn hàng.

---

### 3.2. Yêu cầu phi chức năng (Non-Functional Requirements)
* **Hiệu năng & Tìm kiếm:** Danh sách đơn hàng và màn hình Thực hiện đơn hàng Quốc tế đáp ứng tìm kiếm/lọc đa tiêu chí trong thời gian **$\le 2$ giây**; xuất file PDF chứng từ (HBL, Thông báo hàng đến, DO) hoàn thành trong **$\le 5$ giây**.
* **Phân quyền 2 lớp (Theo mã quyền STMS):**
  * Phân quyền chức năng thao tác theo vai trò trên Swimlane: `Kinh doanh/Sales`, `CS Pricing`, `CS Quốc tế / CS thực hiện`, `Lãnh đạo phê duyệt mở khóa hoàn thành`.
  * Phân quyền phạm vi dữ liệu: Nhân sự Chi nhánh chỉ xem/thao tác đơn thuộc đơn vị mình phụ trách; Phòng VTQT/Công ty LOG và cấp quản lý được cấu hình phạm vi xem điều phối toàn trình.
* **Lưu vết lịch sử (Audit Trail):** Ghi nhận lịch sử người thực hiện, thời điểm chuyển trạng thái (`Cần thực hiện` $\rightarrow$ `Đang thực hiện` $\rightarrow$ `Hoàn thành`), lịch sử chỉnh sửa sau khi được cấp phê duyệt mở khóa, và lịch sử phát hành chứng từ PDF.

---

## IV. PHẠM VI ẢNH HƯỞNG & YÊU CẦU TÍCH HỢP / LIÊN THÔNG

| Phân hệ / Hệ thống liên quan | Mức độ ảnh hưởng | Yêu cầu phối hợp & Ràng buộc dữ liệu |
|---|:---:|---|
| **STMS Sàn Vận Tải — Đơn nội địa** | Không được làm gãy luồng | Tách menu `Đơn quốc tế` độc lập với `Đơn nội địa`; không làm thay đổi logic tạo đơn, báo giá, mã đơn hay trạng thái của đơn nội địa hiện hữu. |
| **STMS Sàn Vận Tải — Quản lý Đối tác** | Liên thông danh mục | Trường `Carrier` / `Agency/FWD` / `Hãng vận chuyển chỉ định` chuẩn bị sẵn khả năng liên kết với danh mục Đối tác quốc tế (khi Module Đối tác triển khai ở PYC riêng). |
| **STMS Sàn Vận Tải — Dự toán & Quyết toán** | Truyền dữ liệu đầu vào | Thông tin đơn hàng, 10 đầu mục chi phí báo giá, `Term`, `Cảng đi/đến`, `Số tờ khai`, `Số vận đơn (MBL/HBL)`, `Ngày dự kiến/thực tế đi-đến` phải sẵn sàng để Dự toán/Quyết toán kế thừa tự động ở bước sau. |
| **Danh mục CRM / Quản trị hàng hóa** | Đọc dữ liệu | Kế thừa danh mục nhóm hàng hóa từ CRM và danh mục Khách hàng (bao gồm khách hàng quốc tế có SĐT 11 số). |
| **SAP FICO / NOC / SAP ZBMS / QLX** | Chưa tác động trực tiếp | Không thay đổi luồng tích hợp FICO/NOC/SAP/QLX hiện tại trong PYC này; giữ nguyên cấu trúc nhận diện nguồn `SVT`. |

---

## V. CÁC ĐIỂM CẦN BP NGHIỆP VỤ (RANH 3) KHẢO SÁT & LÀM RÕ TRONG SRS

> 📌 Theo **Quy trình 6.1.2**, Đơn vị yêu cầu (Ranh 1) chỉ chốt **Quy tắc nghiệp vụ (WHAT & WHY)** tại PYC này. Khi tiếp nhận triển khai ở Bước 3, Bộ phận Nghiệp vụ (Ranh 3) có trách nhiệm khảo sát kỹ thuật (HOW) và làm rõ các điểm sau trong tài liệu SRS để Ranh 1 thẩm định:

1. **Chuẩn hóa dữ liệu nguồn từ tài liệu `VẬN TẢI QUỐC TẾ.pdf`:**
   * Khử trùng lặp trường `Quốc gia đến` đang xuất hiện ở cả Khối Tuyến đường (tr. 5) và Khối Điều kiện thương mại (tr. 7).
   * Rà soát và hợp nhất danh mục 45 khoản mục phụ phí (tr. 8–11): xử lý 2 dòng trùng (`LSS` ở STT 5 & 30; `Storage` ở STT 39 & 42), dòng trống STT 32 và đánh số nhầm mục `II.1 Đường không`.
   * Chuẩn hóa mô tả trường `ETA POD` ở Bảng thực hiện đơn hàng (tr. 14) thành *"Ngày/giờ dự kiến tàu/máy bay cập cảng đến"* và rà soát khuyết STT 24.
2. **Làm rõ các mẫu biểu & ngưỡng còn thiếu/hở:**
   * Thu thập bộ template chuẩn để xuất PDF/Excel từ ĐV nghiệp vụ trước khi dev: **Mẫu Vận đơn phụ (HBL)**, **Mẫu Thông báo hàng đến**, **Mẫu Lệnh giao hàng (DO)**, **Mẫu Import/Export đơn hàng quốc tế**, **Danh sách bảng giá có sẵn** (nếu áp dụng).
   * Xác nhận lại với ĐV yêu cầu ngưỡng cảnh báo lấy vận đơn cho lô hàng có thời gian vận chuyển **từ 5 đến 20 ngày** (đang khuyết giữa `< 5 ngày` và `> 20 ngày`), cũng như logic tính tổng thời gian vận chuyển (`ETA POD - ETD POL` hay trường `transit time`).
   * Xác nhận sự đồng nhất của 2 luồng chuyển giao sau tạo đơn: giữa màn hình `Quản lý lộ trình` và `Thực hiện đơn hàng Quốc tế` (tách 2 màn hình riêng hay hợp nhất 2 tab trên cùng 1 màn hình theo cấu trúc Mục II.3 của PDF mới).
3. **Trách nhiệm thiết kế kỹ thuật (Ranh 3 & Ranh 4):**
   * Tự khảo sát CSDL hiện hữu của STMS Sàn Vận Tải để thiết kế bảng lưu đơn quốc tế đa tuyến, 10 đầu mục chi phí tài chính, cơ chế khóa bản ghi `Hoàn thành` và job quét cảnh báo tự động — **không đẩy câu hỏi thiết kế DB/API về Đơn vị yêu cầu**.

---

## VI. ĐỀ XUẤT PHÂN CÔNG TRÁCH NHIỆM THEO QUY TRÌNH 6.1.2

1. **Đơn vị đề nghị (Ranh 1 - BA / Phòng DVVHCP - Công ty LOG):**
   * Chịu trách nhiệm làm rõ bài toán nghiệp vụ, quy tắc kiểm soát dữ liệu và các mẫu biểu chứng từ đầu vào (Mục III).
   * Thẩm định, phản biện và ký xác nhận tài liệu SRS do BP Nghiệp vụ lập (bằng bộ tiêu chí Review SRS Sàn Vận Tải).
   * Xây dựng kịch bản UAT theo chuẩn BDD (Given-When-Then) và trực tiếp nghiệm thu người dùng ở Bước 9.
2. **Bộ phận Kế hoạch (Ranh 2):**
   * Thẩm định tính hợp lệ, phân bổ nguồn lực và điều phối lộ trình triển khai PYC.
3. **Bộ phận Nghiệp vụ / Khối CNTT (Ranh 3):**
   * Khảo sát hiện trạng CSDL và kiến trúc hệ thống STMS; thiết kế giải pháp kỹ thuật, cấu trúc dữ liệu, API liên thông và viết tài liệu SRS chi tiết; bàn giao SRS cho Ranh 1 thẩm định trước khi chuyển sang Đội sản xuất.
4. **Bộ phận Sản xuất (Ranh 4):**
   * Lập trình tính năng, kiểm thử nội bộ (Unit Test, Integration Test) và hỗ trợ triển khai UAT/Golive.

---

## VII. PHÊ DUYỆT CỦA CÁC BÊN LIÊN QUAN

| NGƯỜI LẬP PHIẾU | TRƯỞNG PHÒNG ĐƠN VỊ ĐỀ NGHỊ | LÃNH ĐẠO ĐƠN VỊ ĐỀ NGHỊ |
|:---:|:---:|:---:|
| *(Ký và ghi rõ họ tên)* | *(Ký và ghi rõ họ tên)* | *(Ký và ghi rõ họ tên)* |
| <br><br><br>**...** | <br><br><br>**...** | <br><br><br>**...** |
