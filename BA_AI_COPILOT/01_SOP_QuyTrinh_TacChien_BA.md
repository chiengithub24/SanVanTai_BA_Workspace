# SỔ TAY VẬN HÀNH CHUẨN (SOP) DÀNH CHO BA SÀN VẬN TẢI
## Ứng Dụng AI Để Làm Chủ Hiện Trạng, Rà Soát SRS Và Soạn Thảo PYC Chuẩn Hóa

> **Dành cho:** Business Analyst (BA) thuộc Đơn vị yêu cầu / Nghiệp vụ Sàn Vận Tải (SVT) - Viettel Post  
> **Phiên bản:** 1.0 (Phát hành bởi Solution Architect)  
> **Hệ thống liên quan:** Sàn Vận Tải (STMS SVT), STMS Quản lý xe (QLX), SAP FICO, NOC, vOffice  

---

## 1. NGUYÊN TẮC CỐT LÕI & RANH GIỚI TRÁCH NHIỆM (SWIMLANE GOVERNANCE)

Căn cứ theo **Quy trình chi tiết 6.1.2 (Quy trình tiếp nhận và xử lý PYC phát triển / nâng cấp phần mềm)**:

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│ RANH 1: ĐƠN VỊ YÊU CẦU (BẠN ĐANG ĐỨNG Ở ĐÂY)                                            │
│ • Nhiệm vụ chính: Bước 1 (Lập PYC) -> Bước 4 (Trình ký PYC) -> Bước 9 (Nghiệm thu UAT)  │
│ • Trọng tâm: Nêu bài toán kinh doanh (WHY & WHAT), Tiêu chí chấp nhận (AC).             │
└──────────────────────────────────────────┬─────────────────────────────────────────────┘
                                           │ (Chuyển giao yêu cầu)
                                           ▼
┌────────────────────────────────────────────────────────────────────────────────────────┐
│ RANH 3: BỘ PHẬN NGHIỆP VỤ (IT BA / SOLUTION TEAM PHÍA PHÁT TRIỂN)                      │
│ • Nhiệm vụ chính: Bước 3 (Phân tích & Đánh giá) -> Viết tài liệu SRS                   │
│ • Trọng tâm: Thiết kế giải pháp hệ thống, CSDL, API, Luồng xử lý chi tiết (HOW).       │
│ • Trách nhiệm: Phải tự khảo sát hiện trạng kỹ thuật, không đùn việc cho Ranh 1.        │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

### 3 Nguyên tắc "Bất di bất dịch" để bảo vệ bản thân:
1. **Nguyên tắc "WHAT vs HOW":** 
   - Bạn chỉ chịu trách nhiệm mô tả: *User cần gì? Tại sao cần? Khi nào thì đạt (Acceptance Criteria)?*
   - BP Nghiệp vụ (Ranh 3) bắt buộc phải chịu trách nhiệm mô tả: *Hệ thống lưu bảng nào? API gọi ra sao? Màn hình cấu hình ở menu nào?*
   - 👉 **Hành động:** Khi BP Nghiệp vụ hỏi: *"Chức năng này lưu vào bảng nào?", "API này viết thế nào?"* $\rightarrow$ Lập tức từ chối lịch sự: *"Đây là giải pháp kỹ thuật thuộc Bước 3 của BP Nghiệp vụ theo quy trình 6.1.2. Đơn vị yêu cầu đã làm rõ quy tắc nghiệp vụ tại Mục 3 của PYC"*.
2. **Nguyên tắc "Tài liệu hóa mọi trao đổi (No Ticket, No Review)":**
   - Tuyệt đối không nhận lời hứa miệng hoặc trao đổi chat vội qua tin nhắn rồi xác nhận qua loa.
   - Mọi đóng góp, bắt bẻ của BP Nghiệp vụ phải được ghi nhận vào **SRS Review Log** (Nhật ký review).
3. **Nguyên tắc "Không phá vỡ luồng cũ (Do No Harm)":**
   - Hệ thống Sàn Vận Tải liên thông mật thiết với **FICO (Xuất hóa đơn, công nợ)** và **NOC/SAP (Ghi nhận doanh thu)**. 
   - Mọi tính năng mới trong SRS nếu chạm vào: Trạng thái đơn, Tỷ lệ dự toán, Biên bản nghiệm thu (BBNTKH), hay Gạch nợ FICO... đều phải được AI quét kỹ để đảm bảo không làm "gãy" luồng cũ.

---

## 2. QUY TRÌNH TÁC CHIẾN 4 BƯỚC HÀNG NGÀY VỚI AI

Khi bạn nhận được một đầu việc mới (User đề xuất nâng cấp tính năng hoặc BP Nghiệp vụ gửi tài liệu sang), hãy mở bộ tài liệu này và làm theo đúng 4 bước sau:

```
[BƯỚC 1] ─────────────────► [BƯỚC 2] ─────────────────► [BƯỚC 3] ─────────────────► [BƯỚC 4]
Nắm Hiện Trạng              Khởi Tạo PYC                 Rà Soát & Phản Biện          Bảo Vệ Ranh Giới
(Bóc tách HDSD cũ)          (Chuẩn Viettel Post)         (Bắt lỗi SRS của Dev)        (Q&A & Trình Ký)
```

---

### BƯỚC 1: NẮM HIỆN TRẠNG NHANH CHÓNG (AS-IS EXTRACTION)
* **Khi nào thực hiện:** Khi bạn phải phụ trách một tính năng mới mà chưa hiểu hệ thống hiện tại đang chạy như thế nào (tài liệu chỉ có file Word HDSD hoặc Slide đào tạo dày đặc).
* **Công cụ sử dụng:** File `02_Prompt_Chaining_Toolkit.md` $\rightarrow$ **PROMPT 1: AS-IS EXTRACTOR**.
* **Cách làm:**
  1. Mở file HDSD (ví dụ `HDSD hệ thống Sàn Vận tải.docx` hoặc Slide `SLIDE_HDSD Sàn vận tải_v1.4 PHASE CHUAN.pptx`).
  2. Copy đoạn nội dung liên quan đến phân hệ cần làm (ví dụ: phần Dự toán, BBNTKH, hoặc Công nợ).
  3. Dán vào ô `[NỘI DUNG HDSD]` trong **Prompt 1** và gửi cho AI.
* **Kết quả nhận được:** AI sẽ trả về cho bạn 1 trang tóm tắt gồm:
  - Sơ đồ chuyển trạng thái (State Machine).
  - Bảng các ràng buộc nghiệp vụ (Business Rules).
  - Điểm chạm tích hợp với hệ thống ngoài (FICO / NOC / SAP).
  *(Bạn chỉ mất 5 phút đọc bảng này là hiểu hệ thống hơn cả người làm lâu năm).*

---

### BƯỚC 2: KHỞI TẠO PHIẾU YÊU CẦU (PYC) CHUẨN FORM VIETTEL POST
* **Khi nào thực hiện:** Khi User/Nghiệp vụ đề xuất nhu cầu mới, cần soạn PYC để trình ký (Bước 1 & Bước 4 trên quy trình 6.1.2).
* **Công cụ sử dụng:** File `02_Prompt_Chaining_Toolkit.md` $\rightarrow$ **PROMPT 3: PYC GENERATOR** kết hợp mẫu `04_Mau_PYC_Chuan_ViettelPost.md`.
* **Cách làm:**
  1. Ghi lại vắn tắt yêu cầu thô của User (dù chỉ là vài gạch đầu dòng từ buổi họp hoặc tin nhắn).
  2. Dán vào **Prompt 3** kèm theo bối cảnh hệ thống đã trích xuất ở Bước 1.
  3. AI sẽ tự động điền đầy đủ vào khung PYC:
     - Nêu bối cảnh vận hành thực tế.
     - Xác định rõ **IN-SCOPE** (việc phải làm) và **OUT-OF-SCOPE** (việc không làm đợt này - chốt chặn quan trọng để không bị bôi việc).
     - Viết sẵn tiêu chí nghiệm thu (Acceptance Criteria) theo chuẩn BDD: `Given (Khi đang ở trạng thái...) - When (Khi người dùng thực hiện...) - Then (Hệ thống phải xử lý...)`.
* **Kết quả:** Bản thảo PYC hoàn chỉnh 90%, sẵn sàng chuyển sang file Word/PDF để trình ký.

---

### BƯỚC 3: RÀ SOÁT & PHẢN BIỆN TÀI LIỆU SRS CỦA ĐỘI PHÁT TRIỂN
* **Khi nào thực hiện:** Khi BP Nghiệp vụ (Ranh 3) gửi lại tài liệu SRS yêu cầu bạn xác nhận/review (Bước 3 trên sơ đồ 6.1.2).
* **Công cụ sử dụng:** File `02_Prompt_Chaining_Toolkit.md` $\rightarrow$ **PROMPT 2: SRS AUDIT ENGINE** kết hợp `03_Checklist_Review_SRS_SanVanTai.md`.
* **Cách làm:**
  1. Copy nội dung SRS (ví dụ: các Use Case trong file `SRS_QLNVVP_10950_Cấu hình Dự toán_Quyết toán.docx`).
  2. Dán vào **Prompt 2** cùng với Bảng luật As-Is ở Bước 1 và PYC ở Bước 2.
  3. AI sẽ tự động kích hoạt chế độ "Thẩm định viên cao cấp", quét qua 5 khía cạnh:
     - **Sai lệch nghiệp vụ:** Giải pháp kỹ thuật này có làm sai bài toán của User không?
     - **Gãy luồng cũ (Breaking changes):** Có làm ảnh hưởng đơn đang chạy dở, có làm sai lệch dữ liệu đồng bộ sang FICO/NOC/SAP không?
     - **Thiếu luồng ngoại lệ:** Thiếu luồng Hủy, Từ chối, Lỗi kết nối, Rollback?
     - **Bắt bài đùn đẩy:** Phát hiện ngay các câu từ thoái thác trách nhiệm như: *"Nghiệp vụ tự kiểm tra"*, *"Hệ thống sẽ cập nhật sau"*, *"Theo thỏa thuận riêng"*.
* **Kết quả:** Xuất ra **Bảng Nhật Ký Review SRS (SRS Review Matrix)** chi tiết, chỉ rõ từng trang, từng mục cần BP Nghiệp vụ giải trình và sửa lại.

---

### BƯỚC 4: BẢO VỆ RANH GIỚI & PHẢN HỒI Q&A KHI HỌP / CHẤT VẤN
* **Khi nào thực hiện:** Khi BP Nghiệp vụ hoặc Đội Dev gửi danh sách câu hỏi hóc búa, ép bạn phải đưa ra thông số kỹ thuật, cấu trúc DB hoặc cố tình đùn đẩy việc phân tích sang cho bạn.
* **Công cụ sử dụng:** File `02_Prompt_Chaining_Toolkit.md` $\rightarrow$ **PROMPT 4: DEFENSE Q&A COPILOT**.
* **Cách làm:**
  1. Copy nguyên văn các câu hỏi chất vấn của BP Nghiệp vụ.
  2. Dán vào **Prompt 4**.
  3. AI sẽ phân loại câu hỏi thành 2 nhóm:
     - **Nhóm 1 (Thuộc trách nhiệm Nghiệp vụ của bạn):** AI soạn sẵn câu trả lời logic, căn cứ đúng theo HDSD và nhu cầu thực tế.
     - **Nhóm 2 (Đùn đẩy việc kỹ thuật):** AI soạn sẵn mẫu phản hồi lịch sự nhưng cương quyết theo đúng chuẩn BPMN 6.1.2 để trả việc về đúng nơi.

---

## 3. CHECKLIST KIỂM TRA TRƯỚC KHI TRÌNH KÝ HOẶC CHỐT SRS

Trước khi bạn đặt bút ký nháy vào PYC hoặc bấm "Đồng ý" thông qua tài liệu SRS của BP Nghiệp vụ, hãy tự kiểm tra 5 câu hỏi vàng:

- [ ] **1. Đơn hàng dở dang:** Khi tính năng mới áp dụng (ví dụ: đổi công thức tính giá, đổi tỷ lệ dự toán, đổi quy tắc công nợ), các đơn hàng đã tạo trước thời điểm đó sẽ xử lý theo luật cũ hay luật mới?
- [ ] **2. Điểm chạm FICO:** Tính năng này có làm thay đổi thời điểm xuất hóa đơn hoặc thời điểm tạo BBNTKH không? Dữ liệu đẩy sang FICO có bị duplicate (trùng) hay thiếu trường bắt buộc (như `Nguồn = SVT`) không?
- [ ] **3. Trạng thái không thể đảo ngược:** Trên Sàn Vận Tải, BBNTKH sau khi đẩy sang FICO không thể hủy/sửa trực tiếp. SRS mới có biện pháp nào chặn user bấm nhầm hoặc xử lý khi cần điều chỉnh không?
- [ ] **4. Luồng xử lý lỗi (Exceptions):** Nếu hệ thống đối tác (FICO, QLX, NOC, SAP) bị timeout hoặc trả về lỗi, hệ thống có cơ chế Retry (gọi lại) hoặc thông báo rõ ràng cho User không?
- [ ] **5. Out-of-Scope:** Trong PYC đã ghi rõ những phần việc KHÔNG LÀM đợt này chưa, để tránh việc nghiệm thu bị đội phát triển kéo dài vô tận?

---

> 💡 **Lời khuyên từ Solution Architect:**  
> Bạn không cần phải nhớ toàn bộ hệ thống trong đầu. Hãy để AI làm "trợ lý bóc tách" và "khiên chắn phản biện" cho bạn. Mọi văn bản bạn đưa ra (PYC, Bảng review SRS) đều có cấu trúc chặt chẽ, dẫn chứng rõ ràng từ HDSD thì không ai có thể đùn đẩy công việc cho bạn được nữa!
