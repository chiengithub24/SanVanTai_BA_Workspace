# CẨM NANG DỰ ÁN SÀN VẬN TẢI (SMART TMS - VIETTEL POST)

Tài liệu này đóng vai trò là **Index và Bản đồ tri thức (Knowledge Base)** cho toàn bộ dự án Sàn Vận Tải (Web Portal, tích hợp STMS Quản Lý Xe, SAP FICO, NOC, SAP ERP và các Phiếu yêu cầu - PYC).  
Bất kỳ phiên làm việc nào của AI (Antigravity IDE) hay thành viên dự án (Solution Architect, Business Analyst) khi bắt đầu đều cần tham khảo cấu trúc này.

---

## 📂 1. CẤU TRÚC THƯ MỤC CHUẨN

```text
SanVanTai_BA_Workspace/
│
├── README.md                                   # [BẠN ĐANG Ở ĐÂY] Bản đồ tri thức & Cẩm nang dự án
├── AGENTS.md                                   # Nguyên tắc chỉ dẫn tự động lưu trữ & bảo vệ ranh giới
│
├── System-Docs/                                # 📁 TÀI LIỆU CHUNG HỆ THỐNG (Living Knowledge Base)
│   ├── 00-tong-quan-chu-trinh-10-buoc.md       # Sơ đồ toàn trình 10 bước: Đơn hàng -> Báo giá -> FICO -> Quyết toán
│   ├── 01-phan-he-don-hang-va-bao-gia.md       # Luật tạo đơn, chuyến xe, CS Pricing, duyệt giá
│   ├── 02-phan-he-du-toan-va-ty-le-chi-phi.md  # Luật phân bổ tỷ lệ dự toán, duyệt vOffice, chuyển tiếp dữ liệu
│   ├── 03-phan-he-dieu-xe-va-stms-qlx.md       # Luồng kết nối QLX, gán xe, app tài xế
│   ├── 04-phan-he-bbntkh-va-dong-bo-fico.md    # Luật lập BBNTKH, quy tắc cấm hủy sau khi sang FICO
│   ├── 05-phan-he-hoa-don-va-doanh-thu-sap.md  # Xuất hóa đơn FICO (Nguồn = SVT), đối soát NOC, bút toán ZBMS
│   ├── 06-phan-he-quan-ly-cong-no-va-gach-no.md# Luật công nợ, job 00:30 ngày 01, chốt ngày 05, clearing FICO
│   └── 07-phan-he-quyet-toan-toan-trinh.md     # Quyết toán Doanh thu - Chi phí - Lợi nhuận thực tế
│
├── PYC/                                        # 📁 TÀI LIỆU CÁC PHIẾU YÊU CẦU (Theo từng Ticket/Feature)
│   ├── PYC-10950-cau-hinh-du-toan-quyet-toan/  # Phân hệ Cấu hình tỷ lệ Dự toán/Quyết toán
│   │   ├── raw/                                # File gốc từ nghiệp vụ hoặc IT (.docx, .pdf...)
│   │   │   └── SRS_QLNVVP_10950_Cấu hình Dự toán_Quyết toán.docx
│   │   ├── 01-phieu-yeu-cau-pyc.md             # Bản PYC chuẩn Viettel Post để trình ký
│   │   ├── 02-nhat-ky-review-srs-phan-bien.md  # Bảng đối chiếu bắt lỗi SRS và câu hỏi chất vấn
│   │   └── 03-kich-ban-nghiem-thu-uat.md       # Bảng kịch bản test Acceptance Criteria
│   │
│   ├── PYC-cong-no-v2.5/                       # Quản lý kế hoạch thu công nợ Sàn Vận Tải - FICO
│   │   ├── raw/
│   │   │   └── SRS_Công nợ_v2.5.docx
│   │   ├── 01-phieu-yeu-cau-pyc.md
│   │   ├── 02-nhat-ky-review-srs-phan-bien.md
│   │   └── 03-kich-ban-nghiem-thu-uat.md
│   │
│   └── PYC-san-van-tai-quoc-te/                # Đơn vận tải dịch vụ quốc tế
│       └── raw/
│           └── PYC Sàn vận tải dv Quốc tế.pdf
│
├── .agents/                                    # 📁 CẤU HÌNH SKILLS DÀNH CHO ANTIGRAVITY IDE (Đã gắn Git)
│   └── skills/
│       ├── doc-hdsd/SKILL.md                   # /doc-hdsd: Bóc tách tài liệu cũ thành luật nghiệp vụ
│       ├── review-srs/SKILL.md                 # /review-srs: Rà soát, bắt lỗi và bẫy đùn đẩy trong SRS
│       ├── soan-pyc/SKILL.md                   # /soan-pyc: Sinh PYC chuẩn Viettel Post với tiêu chí BDD
│       └── phan-bien-ba/SKILL.md               # /phan-bien-ba: Soạn câu trả lời đanh thép chống đùn việc
│
├── BA_AI_COPILOT/                              # 📁 TÀI LIỆU HƯỚNG DẪN CHI TIẾT & CHECKLIST CHO BA
│   ├── README.md                               # Hướng dẫn nhanh cho BA
│   ├── 01_SOP_QuyTrinh_TacChien_BA.md          # Sổ tay quy trình 4 bước tác chiến
│   ├── 02_Prompt_Chaining_Toolkit.md           # Bản dự phòng các prompt nếu dùng web LLM
│   ├── 03_Checklist_Review_SRS_SanVanTai.md    # Bộ tiêu chí kiểm định chuyên sâu Sàn Vận Tải
│   ├── 04_Mau_PYC_Chuan_ViettelPost.md         # Mẫu biểu PYC chuẩn Viettel Post
│   └── 05_ViDu_ThucChien_CaseStudy_DuToan_QuyetToan.md # Ca thực chiến mẫu
│
├── QT/                                         # 📁 SƠ ĐỒ QUY TRÌNH HỆ THỐNG
│   └── 1794453105069_384732770943577577_...jpg # Quy trình chi tiết 6.1.2 tiếp nhận và xử lý PYC
└── HDSD/                                       # 📁 KHO TÀI LIỆU GỐC NGUYÊN BẢN (Archives)
```

---

## 📌 2. NGUYÊN TẮC TỰ ĐỘNG LƯU TRỮ VÀ CẬP NHẬT (DÀNH CHO AI & BA)

Mỗi khi hoàn thành một phần việc, phân tích tính năng mới, hoặc golive một PYC:
1. **Kiến thức dùng chung:** Nếu là quy tắc nghiệp vụ cốt lõi, công thức tính toán, trạng thái luồng mới $\rightarrow$ **Cập nhật ngay vào thư mục `System-Docs/`**.
2. **Nhiệm vụ theo PYC:** Mỗi khi có yêu cầu mới $\rightarrow$ Tạo thư mục `PYC/<mã-pyc>-<tên-ngắn-gọn>/` và lưu trữ đầy đủ 3 file chuẩn:
   - `01-phieu-yeu-cau-pyc.md`: Yêu cầu nghiệp vụ và Acceptance Criteria.
   - `02-nhat-ky-review-srs-phan-bien.md`: Đánh giá rủi ro và chất vấn BP Nghiệp vụ.
   - `03-kich-ban-nghiem-thu-uat.md`: Tiêu chuẩn nghiệm thu chức năng.
3. **Vòng lặp khép kín:** Khi nghiệm thu UAT hoàn tất (Bước 9) $\rightarrow$ AI tự động trích xuất các thay đổi để cập nhật vào `System-Docs/`. Lần sau có yêu cầu mới liên quan đến phân hệ đó, cả AI và BA chỉ cần đọc `System-Docs/` trong 30 giây, không phải đọc lại tài liệu cũ!

---

## ⚡ 3. CÁC LỆNH TẮC CHIẾN NHANH TRONG ANTIGRAVITY IDE

Khi bạn BA mở dự án này trên Antigravity IDE, chỉ cần gõ lệnh hoặc chat tự nhiên:

| Lệnh tắt | Tên kỹ năng | Khi nào sử dụng? |
|:---:|---|---|
| **`/doc-hdsd`** | Bóc tách hiện trạng | Khi cần đọc hiểu nhanh một tính năng cũ từ file HDSD hoặc Slide. |
| **`/review-srs`** | Rà soát & Bắt lỗi SRS | Khi BP Nghiệp vụ gửi tài liệu SRS sang, cần tìm lỗ hổng, rủi ro và điểm đùn đẩy. |
| **`/soan-pyc`** | Soạn thảo PYC chuẩn | Khi có yêu cầu mới từ User, cần tạo bản PYC chuẩn Viettel Post để trình ký. |
| **`/phan-bien-ba`** | Cố vấn phản biện Q&A | Khi BP Nghiệp vụ hoặc Dev hỏi vặn, chất vấn hoặc đùn đẩy việc kỹ thuật. |

*(Thậm chí bạn BA không cần nhớ cú pháp có dấu gạch chéo `/`, chỉ cần chat câu tự nhiên: "Review giúp mình file SRS trong thư mục PYC-10950 với", AI Antigravity sẽ tự động kích hoạt kỹ năng tương ứng!)*
