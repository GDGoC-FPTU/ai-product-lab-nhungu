# Phase 1 — SCAN & QUICK-ASSESS

## 📝 List bài toán vận hành (Sử dụng 4 Lenses)

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|---|---|---|
| 1 | **Vinmec** | **Time-consuming** | Bác sĩ mất trung bình 15-20 phút sau mỗi ca khám để gõ tóm tắt hồ sơ bệnh án, bệnh sử và kê đơn vào hệ thống HIS (Hospital Information System). |
| 2 | **VinFast** | **Repetitive** | Kỹ thuật viên bảo trì pin EV phải đọc thủ công hàng trăm dòng log thông số telemetry (điện áp, nhiệt độ cell pin) gửi về từ xe để phân loại lỗi cảnh báo sớm. |
| 3 | **Xanh SM** | **Stakeholder Pain** | Tổng đài viên CSKH quá tải vì phải xử lý thủ công các khiếu nại của tài xế về việc hệ thống Smart Dispatching định vị sai điểm đón hoặc bị khách hủy chuyến oan. |
| 4 | **Vinhomes** | **AI-upgrade** | Ban quản lý Vinhomes phản hồi các phản ánh tiêu cực của cư dân bằng các mẫu phản hồi rập khuôn, làm giảm trải nghiệm khách hàng. |
| 5 | **Vinpearl** | **Repetitive** | Nhân viên booking phải đọc và phân loại thủ công hàng ngàn email yêu cầu check-in, thay đổi lịch trình hoặc dịch vụ đi kèm của khách hàng. |

---

# 🃏 Quick Problem Cards (Top 3)

## QUICK PROBLEM CARD #1 — Vinmec Tự động hóa nhập liệu hồ sơ bệnh án điện tử (EHR)

### Thông tin bài toán

| Thuộc tính | Nội dung |
|------------|----------|
| **Công ty thành viên** | Vinmec |
| **Ai đang đau?** | Bác sĩ chuyên khoa, Bệnh nhân |
| **Bài toán** | Bác sĩ tốn quá nhiều thời gian nhập liệu hồ sơ bệnh án vào hệ thống HIS sau khi khám xong. |
| **Bước tốn thời gian nhất** | Bước 3 – Nhập thủ công bệnh án vào HIS (15 phút/lượt khám) |
| **AI hỗ trợ ở đâu?** | Chuyển file ghi âm thành văn bản và JSON cấu trúc hóa theo chuẩn HIS |
| **Success Metric** | Giảm thời gian hoàn thành bệnh án từ 15 phút xuống dưới 1.5 phút |
| **Quick Architecture** | Agentic Loop |

### Workflow hiện tại

```text
1. Khám lâm sàng và đối thoại với bệnh nhân
→ 2. Ghi chú nhanh triệu chứng ra giấy nháp
→ 3. Nhớ lại và nhập thủ công toàn bộ bệnh án vào HIS
→ 4. Điều dưỡng kiểm tra lỗi định dạng hành chính
```

### Giá trị kỳ vọng

- Giảm hơn 90% thời gian nhập liệu.
- Giảm sai sót hành chính.
- Tăng thời gian tư vấn bệnh nhân.
- Giảm burnout cho bác sĩ.

---

## QUICK PROBLEM CARD #2 — Vinhomes Tối ưu phản hồi phản ánh của cư dân

### Thông tin bài toán

| Thuộc tính | Nội dung |
|------------|----------|
| **Công ty thành viên** | Vinhomes |
| **Ai đang đau?** | Ban quản lý đô thị, Cư dân |
| **Bài toán** | Ban quản lý phản hồi chậm và sử dụng các mẫu phản hồi rập khuôn cho phản ánh của cư dân. |
| **Bước tốn thời gian nhất** | Bước 3 – Soạn phản hồi (20 phút/phản ánh) |
| **AI hỗ trợ ở đâu?** | Phân tích cảm xúc và tạo phản hồi cá nhân hóa |
| **Success Metric** | Rút ngắn thời gian phản hồi từ 120 phút xuống 15 phút |
| **Quick Architecture** | LLM Assistant |

### Workflow hiện tại

```text
1. Nhận phản ánh
→ 2. Xác minh thông tin
→ 3. Soạn văn bản phản hồi
→ 4. Phê duyệt nội bộ
→ 5. Gửi tới cư dân
```

### Giá trị kỳ vọng

- Tăng tốc độ phản hồi.
- Cải thiện trải nghiệm cư dân.
- Giảm tỷ lệ khiếu nại leo thang.
- Chuẩn hóa chất lượng giao tiếp.

---

## QUICK PROBLEM CARD #3 — Xanh SM Tự động xử lý khiếu nại tài xế

### Thông tin bài toán

| Thuộc tính | Nội dung |
|------------|----------|
| **Công ty thành viên** | Xanh SM |
| **Ai đang đau?** | Đội ngũ QA/Ops, Tài xế |
| **Bài toán** | Đối soát và xử lý thủ công các khiếu nại liên quan đến thưởng phạt và doanh thu. |
| **Bước tốn thời gian nhất** | Bước 2 & 3 – Tra cứu dữ liệu và đối chiếu chính sách (25 phút/ticket) |
| **AI hỗ trợ ở đâu?** | Trích xuất lý do khiếu nại, gọi API đối soát và đề xuất quyết định xử lý |
| **Success Metric** | Tăng tỷ lệ xử lý tự động từ 0% lên 65% |
| **Quick Architecture** | Agentic System |

### Workflow hiện tại

```text
1. Nhận ticket
→ 2. Tra cứu lịch sử vi phạm
→ 3. Đối chiếu chính sách thưởng/phạt
→ 4. Viết phản hồi gửi tài xế
```

### Giá trị kỳ vọng

- Giảm tải cho đội ngũ vận hành.
- Tăng tốc độ xử lý ticket.
- Tăng tính minh bạch trong đối soát.
- Nâng cao mức độ hài lòng của tài xế.

---

# 🎯 Kết luận sơ bộ

| Xếp hạng | Bài toán | AI Fit | Mức ưu tiên |
|-----------|-----------|---------|-------------|
| 🥇 | Vinmec EHR Copilot | Agentic Loop | Cao nhất |
| 🥈 | Xanh SM Complaint Agent | Agentic System | Cao |
| 🥉 | Vinhomes Resident Response Copilot | LLM Assistant | Trung bình |

## Đề xuất lựa chọn

**Vinmec EHR Copilot** là bài toán phù hợp nhất để triển khai Prototype vì:

- ROI rõ ràng.
- Có chỉ số đo lường cụ thể.
- Workflow hiện tại có nhiều thao tác thủ công.
- Dễ triển khai Human-in-the-Loop (HITL).
- Tác động trực tiếp đến năng suất và chất lượng dịch vụ y tế.