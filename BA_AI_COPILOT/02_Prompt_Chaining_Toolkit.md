# BỘ PROMPT TÁC CHIẾN 4 BƯỚC DÀNH CHO BA SÀN VẬN TẢI
## (Prompt Chaining Toolkit - Tối Ưu Cho Gemini, ChatGPT, Claude)

> **Hướng dẫn sử dụng:**  
> Bộ prompt này được thiết kế theo dạng **Chuỗi mắt xích (Prompt Chaining)**. Bạn chỉ cần Copy từng khối lệnh dưới đây, dán vào AI (khuyên dùng Gemini 1.5 Pro / ChatGPT-4o / Claude 3.5 Sonnet), thay thế các phần nằm trong dấu ngoặc vuông `[...]` bằng nội dung tài liệu của bạn.

---

## 🎯 PROMPT 1: BÓC TÁCH LUẬT NGHIỆP VỤ TỪ HDSD (AS-IS KNOWLEDGE EXTRACTOR)

> **Mục tiêu:** Biến hàng chục trang tài liệu HDSD thao tác dài dòng hoặc slide đào tạo thành Bảng Tóm Tắt Luật Nghiệp Vụ chỉ trong 1 phút.

```markdown
Bạn là một Solution Architect và Lead Business Analyst kỳ cựu của hệ thống Sàn Vận Tải (Smart TMS) - Viettel Post, am hiểu sâu sắc quy trình vận hành chuỗi logistics, hạch toán doanh thu và tích hợp các hệ thống (STMS Sàn Vận Tải, STMS Quản Lý Xe, SAP FICO, NOC, SAP ZBMS).

Tôi là BA thuộc Đơn vị yêu cầu nghiệp vụ. Tôi đang cần nắm bắt nhanh hiện trạng vận hành (As-Is) của một phân hệ trong hệ thống để chuẩn bị làm yêu cầu nâng cấp.

Dưới đây là nội dung trích xuất từ tài liệu Hướng dẫn sử dụng (HDSD) / Slide đào tạo hiện tại:
---
[DÁN ĐOẠN VĂN BẢN HDSD LIÊN QUAN VÀO ĐÂY]
---

Hãy phân tích và bóc tách nội dung trên thành một Báo Cáo Hiện Trạng Tinh Gọn gồm đúng 5 phần sau (dạng bảng và bullet points, không viết văn xuôi dài dòng):

1. TÓM TẮT MỤC TIÊU & ĐỐI TƯỢNG:
- Phân hệ này giải quyết bài toán gì trong chu trình vận tải?
- Các vai trò (Actors) tham gia thao tác và quyền hạn chính của họ.

2. MA TRẬN LUỒNG TRẠNG THÁI (STATE MACHINE):
Lập bảng mô tả vòng đời của đối tượng chính (Đơn hàng / Chuyến xe / Dự toán / BBNTKH / Quyết toán / Công nợ):
| STT | Trạng thái hiện tại | Thao tác kích hoạt | Điều kiện để chuyển trạng thái | Trạng thái kế tiếp | Ai thực hiện |

3. BẢNG QUY TẮC NGHIỆP VỤ NGẦM (BUSINESS RULES MATRIX):
Bóc tách các công thức tính, điều kiện ràng buộc dữ liệu:
| Mã Rule | Tên quy tắc / Ràng buộc | Chi tiết xử lý logic | Ràng buộc bắt buộc (Mandatory) / Cảnh báo |

4. CÁC ĐIỂM CHẠM TÍCH HỢP HỆ THỐNG NGOÀI (INTEGRATION TOUCHPOINTS):
- Dữ liệu đẩy sang hệ thống nào? (STMS Quản lý xe / SAP FICO / NOC / SAP ERP / vOffice)?
- Thời điểm đồng bộ là khi nào?
- Dữ liệu đồng bộ gồm những thông tin quan trọng nào?

5. CÁC ĐIỂM "BẤT KHẢ BIẾN" & RỦI RO CẦN LƯU Ý (CRITICAL WARNINGS):
- Những thao tác nào sau khi thực hiện thì KHÔNG THỂ HOÀN TÁC / KHÔNG ĐƯỢC PHÉP SỬA TRỰC TIẾP? (Ví dụ: BBNTKH đã đẩy sang FICO, Đơn hàng đã duyệt giá...)?
- Những rủi ro sai lệch doanh thu hoặc công nợ cần đặc biệt chú ý.
```

---

## 🎯 PROMPT 2: RÀ SOÁT & BẮT LỖI TÀI LIỆU SRS (SRS AUDIT & GAP ANALYSIS ENGINE)

> **Mục tiêu:** So sánh 3 chiều giữa Nhu cầu User - Hiện trạng HDSD - Đề xuất kỹ thuật trong SRS của BP Nghiệp vụ. Phát hiện các điểm gãy luồng cũ, thiếu sót và bắt bài các điểm đùn đẩy trách nhiệm.

```markdown
Bạn là một Chuyên gia Thẩm định Giải pháp (Solution Reviewer) và Lead BA độc lập, bảo vệ quyền lợi của Đơn vị Yêu cầu Nghiệp vụ theo Quy trình 6.1.2 của Viettel Post.

Nhiệm vụ của bạn là rà soát, phản biện và "bắt lỗi" bản tài liệu đặc tả chức năng (SRS) do Bộ phận Nghiệp vụ / Đội IT Phát triển gửi sang để review trước khi phê duyệt.

Dưới đây là 3 nguồn dữ liệu đầu vào:
---
[NGUỒN 1: BÀI TOÁN NGHIỆP VỤ / NHU CẦU CỦA USER]
[Dán yêu cầu của User hoặc tóm tắt nhu cầu vào đây]

[NGUỒN 2: HIỆN TRẠNG HỆ THỐNG (AS-IS TỪ HDSD HOẶC KẾT QUẢ PROMPT 1)]
[Dán tóm tắt luật nghiệp vụ hiện tại vào đây]

[NGUỒN 3: NỘI DUNG SRS DO ĐỘI PHÁT TRIỂN / BP NGHIỆP VỤ GỬI SANG]
[Dán nội dung các Use Case trong file SRS vào đây]
---

Hãy thẩm định tài liệu SRS dựa trên KHUNG KIỂM ĐỊNH 5 CHIỀU:
1. Tính đúng đắn (Correctness): SRS có giải quyết đúng và trúng bài toán của User không? Có hiểu sai ý nghiệp vụ không?
2. Tính tương thích ngược (Backward Compatibility): Luồng mới có làm GÃY (break) luồng cũ trong HDSD không? Các đơn hàng đang chạy dở dang xử lý thế nào? Tích hợp FICO / NOC / SAP có bị sai lệch không?
3. Độ bao phủ ngoại lệ (Exception Flows): Có mô tả các trường hợp lỗi mạng, hủy, từ chối, rollback không?
4. Phân quyền & Dữ liệu (RACI & Data Scope): Phân quyền có chặt chẽ không? Có hở sườn lộ dữ liệu không?
5. Bắt bài đùn đẩy (Push-back Detection): Tìm các câu từ mơ hồ nhằm trốn tránh trách nhiệm thiết kế hệ thống (ví dụ: "Nghiệp vụ tự kiểm tra", "Hệ thống sẽ cập nhật sau", "Theo quy định hiện hành...").

HÃY XUẤT BẢO CÁO REVIEW THEO ĐÚNG CẤU TRÚC SAU:

I. ĐÁNH GIÁ TỔNG QUAN:
- Kết luận: [CHẤP THUẬN / YÊU CẦU SỬA ĐỔI / TỪ CHỐI BẢO VỆ LẠI]
- Điểm đánh giá độ hoàn thiện của SRS (thang điểm 10).
- Nhận định ngắn gọn về chất lượng giải pháp kỹ thuật.

II. BẢNG NHẬT KÝ BẮT LỖI VÀ CHẤT VẤN SRS (SRS REVIEW MATRIX):
| STT | Vị trí mục / Use Case trong SRS | Hiện trạng cũ (HDSD) | Giải pháp SRS đề xuất | Vấn đề / Rủi ro phát hiện | Mức độ (Blocker / Major / Minor) | Câu hỏi chất vấn & Yêu cầu BP Nghiệp vụ phải sửa |
|---|---|---|---|---|---|---|

III. DANH SÁCH CÁC ĐIỂM ĐÙN ĐẨY TRÁCH NHIỆM BỊ PHÁT HIỆN:
- Liệt kê các điều khoản trong SRS mà BP Nghiệp vụ đang cố tình đẩy việc của họ (phân tích kỹ thuật, xử lý logic) sang cho Đơn vị yêu cầu.
- Đề xuất câu phản hồi đanh thép để trả lại việc cho BP Nghiệp vụ.

IV. CÁC LUỒNG NGOẠI LỆ BỊ BỎ QUÊN (MISSING EDGE CASES):
- Liệt kê ít nhất 3-5 kịch bản lỗi / ngoại lệ thực tế mà SRS chưa hề đề cập đến (bắt buộc dev phải bổ sung).
```

---

## 🎯 PROMPT 3: SINH PHIẾU YÊU CẦU (PYC) CHUẨN FORM VIETTEL POST (PYC GENERATOR)

> **Mục tiêu:** Chuyển hóa toàn bộ yêu cầu và kết quả phân tích thành một bản Phiếu đề nghị yêu cầu (PYC) chuyên nghiệp, chuẩn form để trình ký lãnh đạo (Bước 1 & 4 trên BPMN 6.1.2).

```markdown
Bạn là Business Analyst giàu kinh nghiệm của Tổng Công ty Cổ phần Bưu chính Viettel (Viettel Post), chuyên soạn thảo các văn bản Phiếu đề nghị yêu cầu (PYC) phát triển / nâng cấp phần mềm trình Ban Giám đốc và chuyển giao cho Khối CNTT / BP Nghiệp vụ.

Hãy sử dụng toàn bộ thông tin dưới đây để soạn thảo một bản PHIẾU ĐỀ NGHỊ YÊU CẦU (PYC) hoàn chỉnh, chặt chẽ, chuẩn thể thức:

---
[THÔNG TIN ĐẦU VÀO]
- Tên tính năng / yêu cầu: [Ví dụ: Bổ sung tính năng Cấu hình Dự toán/Quyết toán trên Sàn Vận Tải]
- Đơn vị đề nghị: [Tên phòng ban / Trung tâm của bạn]
- Phân hệ liên quan: Sàn Vận Tải (Smart TMS), tích hợp FICO / NOC / SAP
- Nhu cầu thực tế của người dùng: [Dán nhu cầu hoặc kết quả từ các bước trước vào đây]
- Các rủi ro và ràng buộc cần khóa: [Dán các điểm lưu ý từ Prompt 1 & 2 vào đây]
---

Yêu cầu xuất ra văn bản PYC theo ĐÚNG KHUNG MẪU CHUẨN sau:

1. BỐI CẢNH VÀ CĂN CỨ ĐỀ XUẤT:
- Nêu rõ thực trạng vận hành hiện tại (As-Is) trên Sàn Vận Tải và các khó khăn, bất cập thực tế gặp phải.
- Căn cứ đề xuất (Chiến lược kinh doanh, chỉ đạo của lãnh đạo, tối ưu năng suất lao động, giảm thiểu sai sót đối soát doanh thu - công nợ).

2. MỤC TIÊU YÊU CẦU:
- Mục tiêu định tính: Chuẩn hóa quy trình, tự động hóa, tăng tính minh bạch.
- Mục tiêu định lượng: Giảm thời gian xử lý thủ công (từ X giờ xuống Y phút), loại bỏ 100% sai lệch doanh thu giữa SVT và FICO.

3. PHẠM VI YÊU CẦU (SCOPE BOUNDARY - CỰC KỲ QUAN TRỌNG ĐỂ CHỐT CHẶN):
- In-Scope (Thuộc phạm vi thực hiện đợt này): Ghi rõ danh sách các chức năng cần xây dựng/điều chỉnh.
- Out-of-Scope (Ngoại phạm vi - Không thực hiện đợt này): Liệt kê rõ những thứ KHÔNG làm để ngăn chặn việc bị đùn đẩy hoặc phình to phạm vi.

4. YÊU CẦU CHI TIẾT VÀ TIÊU CHÍ NGHIỆM THU (ACCEPTANCE CRITERIA):
Mô tả chi tiết từng yêu cầu nghiệp vụ theo cấu trúc BDD (Given - When - Then):
- Nghiệp vụ 1: [Tên nghiệp vụ]
  + Mô tả quy tắc: ...
  + Tiêu chí nghiệm thu (AC 1.1): 
    * Given (Điều kiện ban đầu): ...
    * When (Hành động của người dùng / sự kiện): ...
    * Then (Kết quả kỳ vọng hệ thống phải thực hiện): ...
- Nghiệp vụ 2: [Tên nghiệp vụ] ...

5. PHẠM VI ẢNH HƯỞNG & YÊU CẦU TÍCH HỢP:
- Ảnh hưởng đến các phân hệ: Tạo đơn, Dự toán, Điều phối xe, BBNTKH, Quyết toán.
- Ảnh hưởng tích hợp: Cơ chế đẩy dữ liệu sang SAP FICO, đồng bộ NOC, bút toán SAP ZBMS.
- Quy tắc chuyển đổi dữ liệu lịch sử (Migration / Transition Rule): Đơn hàng dở dang xử lý thế nào?

6. ĐỀ XUẤT KẾ HOẠCH & ĐƠN VỊ PHỐI HỢP:
- Đơn vị đề nghị: Chịu trách nhiệm cung cấp nghiệp vụ, duyệt SRS và nghiệm thu UAT (Ranh 1).
- Bộ phận Nghiệp vụ / CNTT: Chịu trách nhiệm phân tích giải pháp kỹ thuật, viết SRS, phát triển và kiểm thử nội bộ (Ranh 3 & 4).
```

---

## 🎯 PROMPT 4: TRỢ LÝ PHẢN BIỆN & ĐẨY LÙI ĐÙN ĐẨY (DEFENSE Q&A COPILOT)

> **Mục tiêu:** Khi BP Nghiệp vụ gửi tin nhắn, email chất vấn, bắt bẻ hoặc đùn đẩy việc kỹ thuật sang cho bạn, hãy dùng prompt này để có câu trả lời chuẩn mực, vừa chuyên nghiệp vừa bảo vệ ranh giới.

```markdown
Bạn là một Solution Architect giàu kinh nghiệm, đóng vai trò là "Cố vấn bảo vệ ranh giới" cho một bạn Business Analyst (Đơn vị yêu cầu - Ranh 1 theo Quy trình 6.1.2 Viettel Post).

Hiện tại, Bộ phận Nghiệp vụ / IT BA (Ranh 3) hoặc Đội Dev (Ranh 4) đang gửi danh sách các câu hỏi / yêu cầu / chất vấn dưới đây sang cho bạn BA:
---
[DÁN NGUYÊN VĂN CÂU HỎI HOẶC TIN NHẮN CỦA ĐỐI TÁC VÀO ĐÂY]
---

Bối cảnh hệ thống: Sàn Vận Tải (Smart TMS), tích hợp SAP FICO, NOC, SAP.

Hãy phân tích từng câu hỏi và soạn thảo kịch bản phản hồi theo 2 nhóm:

1. PHÂN TÍCH BẢN CHẤT CÂU HỎI:
Chỉ rõ câu nào là:
- [A] Câu hỏi nghiệp vụ chính đáng (Thuộc phạm vi Ranh 1 của BA Đơn vị yêu cầu).
- [B] Câu hỏi mang tính đùn đẩy trách nhiệm phân tích kỹ thuật / thiết kế CSDL / API (Lẽ ra thuộc phạm vi Ranh 3 của BP Nghiệp vụ).

2. KỊCH BẢN PHẢN HỒI CHI TIẾT (DÙNG ĐỂ GỬI QUA EMAIL / ZALO / BIÊN BẢN HỌP):
- Đối với nhóm [A]: Soạn câu trả lời nghiệp vụ rõ ràng, súc tích, gắn chặt với thực tế vận hành của Sàn Vận Tải và quy định của Viettel Post.
- Đối với nhóm [B]: Soạn câu phản hồi lịch sự, văn minh nhưng đanh thép, dẫn chiếu rõ Quy trình 6.1.2 để khẳng định: Đơn vị yêu cầu chỉ chốt Quy tắc nghiệp vụ (Business Rules), phần giải pháp kỹ thuật, thiết kế cấu trúc dữ liệu và kiến trúc gọi API thuộc trách nhiệm phân tích tại Bước 3 của BP Nghiệp vụ.
```
