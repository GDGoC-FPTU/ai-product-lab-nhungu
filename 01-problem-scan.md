# 01 — Problem Scan & Quick Cards (Bài cá nhân)

> **Họ và tên:** 🔧 Dương Quang Khải
> **MSSV / Email:** 🔧 duongkhai222204pt@gmail.com
> **Nhóm:** 🔧 nhungu
> **Mảng kinh doanh lựa chọn:** Xanh SM (GSM) — Vận hành xe taxi điện thông minh.

---

## 🔍 Phase 1 — SCAN: Quét cơ hội bằng 4 Lenses

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **Xanh SM** | Tốn thời gian | Điều phối viên xử lý thủ công sự cố tài xế báo hết pin / sự cố sạc giữa đường: tra cứu vị trí xe, tìm trạm sạc trống và soạn tin chỉ đường (15 phút/lượt). |
| 2 | **Xanh SM** | Lặp lại | Phân bổ lại cuốc xe khi khách đổi điểm đến giữa chừng, phải tính lại lộ trình và giá cước thủ công. |
| 3 | **VinFast** | Lặp lại | Đối chiếu hóa đơn sạc điện hằng tuần từ hàng nghìn trụ sạc đối tác với dữ liệu tài chính nội bộ. |
| 4 | **Vinhomes** | AI có thể tốt hơn | Phân loại & điều hướng phản ánh cư dân (mất nước, hỏng đèn, ồn ào) trên App Resident đến đúng ban quản lý từng tòa (phản hồi rập khuôn, chậm ~12 tiếng). |
| 5 | **Xanh SM** | Pain từ người khác | Nghe ghi âm cuộc gọi hủy chuyến + ghi chú tài xế để phân loại 10 lý do hủy phổ biến nhằm tìm pattern lỗi hệ thống. |
| 6 | **Vinmec** | Tốn thời gian | Soạn thảo bản tóm tắt hồ sơ xuất viện cho bệnh nhân từ bệnh án điện tử (20–30 phút/bệnh nhân, bác sĩ quá tải). |

---

## 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Chọn top 3 từ danh sách SCAN: **#1 (Xanh SM — Sự cố hết pin thực địa), #4 (Vinhomes — Phản ánh cư dân), #5 (Xanh SM — Phân tích hủy chuyến).**

### Card #1 — Xanh SM: Xử lý sự cố hết pin thực địa

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Tài xế Xanh SM báo hết pin / sự cố sạc giữa       │
│ đường, cần điều phối viên hướng dẫn đến trạm sạc gần nhất    │
│ hoặc điều xe cứu hộ.                                         │
│ Công ty thành viên: [x] Xanh SM (GSM)                       │
│                                                             │
│ Ai đang đau? Tài xế (chờ đợi, mất cuốc) + Điều phối viên     │
│ (quá tải giờ cao điểm).                                     │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Tài xế gọi tổng đài báo hết pin                        │
│   → 2. Điều phối viên tra cứu vị trí GPS của xe             │
│   → 3. Tra cứu thủ công trạm sạc VinFast còn trụ trống       │
│   → 4. Soạn tin nhắn chỉ đường gửi qua App tài xế           │
│   → 5. Gọi xe cứu hộ nếu pin đã cạn kiệt                    │
│                                                             │
│ Bước nào tốn nhất? Bước 3-4 (⏱ ~10 phút/lượt)               │
│ AI có thể nhảy vào ở bước nào? Bước 3-4 (tra trạm trống &   │
│ tự động soạn tin chỉ đường dạng nháp).                      │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Giảm thời gian xử lý sự cố từ 15 phút ──> dưới 3 phút.      │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
└─────────────────────────────────────────────────────────────┘
```

### Card #2 — Vinhomes: Phân loại & Điều hướng phản ánh cư dân

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Phân loại tự động khiếu nại cư dân trên App        │
│ Resident và route đến đúng ban quản lý từng tòa nhà.        │
│ Công ty thành viên: [x] Vinhomes                            │
│                                                             │
│ Ai đang đau? Nhân viên CSKH (phân loại tay) + Cư dân (chờ). │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Cư dân gửi phản ánh dạng text trên App                 │
│   → 2. CSKH đọc, phân loại nhóm vấn đề                      │
│   → 3. Chuyển thủ công cho ban quản lý đúng tòa             │
│   → 4. Soạn tin phản hồi cư dân                             │
│                                                             │
│ Bước nào tốn nhất? Bước 2-3 (⏱ ~8 phút/phản ánh)            │
│ AI có thể nhảy vào ở bước nào? Bước 2-3 (phân loại + route).│
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ 85% phản ánh được phân loại & route đúng dưới 10 giây.      │
│                                                             │
│ Quick Architecture: [x] Rule + LLM Feature                  │
└─────────────────────────────────────────────────────────────┘
```

### Card #3 — Xanh SM: Phân tích lý do hủy chuyến

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Tổng hợp ghi âm cuộc gọi + ghi chú tài xế để       │
│ phân loại lý do hủy chuyến, tìm pattern rò rỉ cuốc.         │
│ Công ty thành viên: [x] Xanh SM (GSM)                       │
│                                                             │
│ Ai đang đau? Đội phân tích vận hành (back-office).          │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Thu thập log hủy chuyến + ghi chú tài xế               │
│   → 2. Nghe lại ghi âm / đọc ghi chú                       │
│   → 3. Gán nhãn lý do hủy thủ công                         │
│   → 4. Tổng hợp báo cáo tuần                                │
│                                                             │
│ Bước nào tốn nhất? Bước 2-3 (⏱ ~6 phút/case)                │
│ AI có thể nhảy vào ở bước nào? Bước 3 (auto-gán nhãn).      │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Giảm thời gian gán nhãn từ 6 phút ──> dưới 1 phút/case.     │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
└─────────────────────────────────────────────────────────────┘
```

---

## 🗳️ Đề xuất cá nhân

Tôi đề xuất nhóm chọn **Card #1 — Xanh SM: Xử lý sự cố hết pin thực địa** để Deep-Dive, vì đây là bài toán real-time ảnh hưởng trực tiếp đến doanh thu và an toàn giao thông, có metric rõ ràng và ranh giới an toàn cụ thể (bắt buộc Human-in-the-loop + ngưỡng pin nguy cấp).



Họ và tên : Trần Văn Khoa
Email: khoatranvippro3@gmail.com
Github username : Khoatranvipaz1
DIscord username: Trần Văn Khoa - 2A202600827

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

# 01 — Problem Scan & Quick Cards (Bài cá nhân)

> **Họ và tên:** 🔧 Phùng Hoàng Anh
> **MSSV / Email:** 🔧 anhh3642@gmail.com
> **Nhóm:** 🔧 nhungu
> **Mảng kinh doanh lựa chọn:** Vinmec

---

## 🔍 Phase 1 — SCAN: Quét cơ hội bằng 4 Lenses

|| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | Vinmec | Time-consuming | Phân luồng nhu cầu khám và đặt lịch thủ công, phải đối chiếu chuyên khoa, slot bác sĩ, mức độ ưu tiên và gọi xác nhận lại nhiều vòng. |
| 2 | Vinmec | AI-upgrade | Tóm tắt hồ sơ bệnh án trước giờ khám từ nhiều nguồn dữ liệu rời rạc, giúp bác sĩ nắm nhanh tiền sử và thuốc đang dùng. |
| 3 | Vinmec | Repetitive | Soạn giấy ra viện, hướng dẫn tái khám và dặn dò thuốc gần như lặp lại nhưng vẫn phải cá nhân hóa theo từng ca bệnh. |
| 4 | Vinmec | Stakeholder Pain | Tổng đài/CSKH trả lời lặp lại các câu hỏi về giờ khám, chuẩn bị xét nghiệm, bảo hiểm, chỉ đường và quy định nhập viện. |
| 5 | Vinmec | Repetitive | Đối soát hồ sơ bảo hiểm và kiểm tra thiếu giấy tờ, thiếu mã ICD, thiếu chữ ký hoặc lệch thông tin bệnh nhân trước khi gửi đi. |

---

## 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): Tự động phân luồng nhu cầu khám và đặt    │
│ lịch cho bệnh nhân Vinmec theo chuyên khoa và slot phù hợp. │
│                                                             │
│ Công ty thành viên: [x] Vinmec                              │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên lễ tân/điều phối lịch khám.  │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Nhận yêu cầu từ hotline/app/quầy tiếp tân              │
│   2. Hỏi triệu chứng, chuyên khoa, bảo hiểm, thời gian      │
│   3. Tra lịch trống của bác sĩ/phòng khám                   │
│   4. Gọi/nhắn lại để xác nhận lịch                           │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Đối chiếu slot và xác      │
│ nhận qua lại với bệnh nhân (4-7 phút/lượt)                  │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Gợi ý chuyên khoa,   │
│ đề xuất slot phù hợp và soạn tin nhắn xác nhận ban đầu.     │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? Giảm thời gian đặt   │
│ lịch trung bình từ 6 phút xuống dưới 2 phút và giảm ít      │
│ nhất 30% số cuộc gọi xác nhận lại.                          │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent│
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu): Tóm tắt hồ sơ bệnh án trước buổi khám để  │
│ bác sĩ nhìn nhanh tiền sử, thuốc đang dùng và xét nghiệm.   │
│                                                             │
│ Công ty thành viên: [x] Vinmec                              │
│                                                             │
│ Ai đang đau (Actor)? Bác sĩ khám bệnh và điều dưỡng hỗ trợ │
│ chuẩn bị hồ sơ.                                             │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Mở hồ sơ cũ, kết quả xét nghiệm, chẩn đoán, đơn thuốc  │
│   2. Đọc nhiều tài liệu rời rạc để tìm điểm quan trọng      │
│   3. Tự tóm tắt tình trạng, thuốc đang dùng, điểm cần hỏi   │
│   4. Chuẩn bị ghi chú cho buổi khám hiện tại                │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Tổng hợp và đọc chéo nhiều │
│ nguồn thông tin (8-15 phút/bệnh nhân)                       │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Trích xuất thông tin │
│ quan trọng và tạo bản tóm tắt ngắn theo mẫu cố định.        │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? Giảm thời gian đọc   │
│ trước khám từ 10 phút xuống dưới 3 phút mỗi bệnh nhân và    │
│ đạt độ đầy đủ thông tin trên 90%.                           │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent│
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): Soạn giấy ra viện, hướng dẫn dùng thuốc   │
│ và lịch tái khám theo từng ca bệnh một cách nhất quán.      │
│                                                             │
│ Công ty thành viên: [x] Vinmec                              │
│                                                             │
│ Ai đang đau (Actor)? Điều dưỡng, bác sĩ điều trị và bộ      │
│ phận hành chính y khoa.                                     │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Lấy chẩn đoán cuối, toa thuốc và chỉ định tái khám     │
│   2. Copy mẫu giấy ra viện hoặc hướng dẫn chuẩn             │
│   3. Chỉnh sửa thủ công theo từng bệnh nhân và loại thuốc   │
│   4. Kiểm tra lại nội dung để tránh thiếu thông tin         │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Cá nhân hóa nội dung và    │
│ rà lỗi hành chính, khoảng 5-10 phút/hồ sơ.                  │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Tạo bản nháp giấy     │
│ ra viện và dặn dò sau khám từ dữ liệu có cấu trúc.          │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? Giảm thời gian soạn  │
│ từ 8 phút xuống dưới 2 phút/hồ sơ và giảm lỗi thiếu trường  │
│ bắt buộc xuống dưới 2%.                                     │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent│
└─────────────────────────────────────────────────────────────┘

Họ và tên : Phùng Hoàng Anh
Email: anhh3642@gmail.com
Github username : hoanganh-k2
DIscord username: hoanganh5428

<!-- # 🔍 Phase 1 — SCAN

| # | Subsidiary | Lens                          | Mô tả ngắn bài toán                                                                                                                                            |
| - | ---------- | ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1 | Xanh SM    | Stakeholder Pain + Repetitive | Tài xế thường phàn nàn hệ thống gợi ý điểm đón khách chưa chính xác tại sân bay/trung tâm thương mại, dẫn đến thời gian đón lâu và bị huỷ chuyến.              |
| 2 | VinFast    | Repetitive + Time-consuming   | Bộ phận hỗ trợ kỹ thuật phải xử lý hàng nghìn ticket liên quan lỗi pin/sạc EV mỗi ngày, phần lớn là các case lặp lại nhưng vẫn cần nhân viên đọc log thủ công. |
| 3 | Vinhomes   | Time-consuming                | Nhân viên CSKH mất nhiều thời gian đọc và phản hồi review 1-star từ cư dân trên app/community group.                                                           |
| 4 | Vinmec     | Stakeholder Pain              | Bệnh nhân thường phải chờ lâu khi đặt lịch khám vì hotline quá tải, đặc biệt giờ cao điểm.                                                                     |
| 5 | Vinpearl   | AI-upgrade                    | Chatbot hỗ trợ đặt vé/voucher hoạt động cứng nhắc, không hiểu câu hỏi đa bước hoặc khách muốn đổi lịch linh hoạt.                                              |
| 6 | Xanh SM    | Repetitive                    | Điều phối viên phải route lại tài xế EV khi pin yếu và nhu cầu khách thay đổi theo thời gian thực.                                                             |
| 7 | VinFast    | Stakeholder Pain              | Khách hàng EV lo lắng về “range anxiety” nhưng hệ thống hiện tại chưa cảnh báo chủ động rủi ro hết pin theo điều kiện giao thông thực tế.                      |
| 8 | Vinhomes   | AI-upgrade                    | Ban quản lý cư dân nhận quá nhiều ticket bảo trì giống nhau (điện nước/thang máy/internet) nhưng chưa có hệ thống AI phân loại ưu tiên tự động.                |

---

# 🃏 Phase 2 — QUICK-ASSESS

────────────────────────────────────────────
QUICK PROBLEM CARD #1
────────────────────────────────────────────

Bài toán (1 câu):
Hệ thống Xanh SM hiện gợi ý điểm đón khách chưa chính xác tại các khu vực đông đúc như sân bay hoặc trung tâm thương mại.

Công ty thành viên:
[X] Xanh SM

Ai đang đau (Actor)?

* Tài xế Xanh SM
* Khách hàng
* Dispatcher vận hành

Workflow thủ công hiện tại:

1. Khách đặt xe
2. Hệ thống chọn điểm đón mặc định
3. Tài xế gọi điện xác nhận vị trí
4. Khách/tài xế tìm nhau
5. Huỷ chuyến hoặc đón trễ

Bước nào tốn thời gian/lỗi nhất?

* Bước 3–4
* ⏱ 5–10 phút/chuyến tại giờ cao điểm

AI có thể nhảy vào hỗ trợ ở bước nào?

* AI dự đoán “pickup hotspot” tối ưu dựa trên:

  * GPS lịch sử
  * camera giao thông
  * heatmap đón khách thành công
  * traffic realtime

Đo thành công bằng gì?

* Giảm tỷ lệ huỷ chuyến từ 18% → dưới 8%
* Giảm thời gian tìm khách từ 7 phút → dưới 2 phút

Quick Architecture:
[ ] No AI
[ ] Rule
[X] LLM
[X] Agent

---

────────────────────────────────────────────
QUICK PROBLEM CARD #2
────────────────────────────────────────────

Bài toán (1 câu):
VinFast đang xử lý ticket lỗi pin EV thủ công gây quá tải cho đội technical support.

Công ty thành viên:
[X] VinFast

Ai đang đau (Actor)?

* Technical support team
* Chủ xe EV
* Call center

Workflow thủ công hiện tại:

1. Khách gọi hotline/app support
2. Nhân viên đọc mô tả lỗi
3. Mở log pin/charging
4. Đối chiếu knowledge base
5. Escalate kỹ sư nếu cần

Bước nào tốn thời gian/lỗi nhất?

* Bước 3–4
* ⏱ 15–25 phút/ticket

AI có thể nhảy vào hỗ trợ ở bước nào?

* AI đọc log lỗi pin tự động
* Tóm tắt nguyên nhân khả thi
* Đề xuất SOP xử lý phù hợp

Đo thành công bằng gì?

* Giảm thời gian xử lý ticket từ 20 phút → dưới 5 phút
* Giảm 40% số ticket cần escalate kỹ sư

Quick Architecture:
[ ] No AI
[X] Rule
[X] LLM
[ ] Agent

---

────────────────────────────────────────────
QUICK PROBLEM CARD #3
────────────────────────────────────────────

Bài toán (1 câu):
Nhân viên Vinhomes mất nhiều thời gian phản hồi review tiêu cực của cư dân trên app/community channels.

Công ty thành viên:
[X] Vinhomes

Ai đang đau (Actor)?

* CSKH cư dân
* Ban quản lý toà nhà
* Cư dân

Workflow thủ công hiện tại:

1. Nhân viên đọc review
2. Xác định mức độ nghiêm trọng
3. Soạn phản hồi thủ công
4. Chuyển ticket cho bộ phận liên quan
5. Theo dõi xử lý

Bước nào tốn thời gian/lỗi nhất?

* Bước 2–3
* ⏱ 10–15 phút/review

AI có thể nhảy vào hỗ trợ ở bước nào?

* AI sentiment analysis
* Auto-draft phản hồi chuyên nghiệp
* Tự động phân loại ticket urgency

Đo thành công bằng gì?

* Giảm thời gian phản hồi từ 12 phút → dưới 2 phút
* Tăng CSAT cư dân từ 78% → 90%

Quick Architecture:
[ ] No AI
[X] Rule
[X] LLM
[ ] Agent -->


# 🔍 Phase 1 — SCAN

| # | Subsidiary | Lens                          | Mô tả ngắn bài toán                                                                                                                                                      |
| - | ---------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1 | Xanh SM    | Stakeholder Pain + Repetitive | Tài xế thường mất nhiều thời gian tìm khách tại sân bay, Vincom hoặc khu đông người do hệ thống gợi ý điểm đón chưa chính xác, dẫn tới huỷ chuyến và tăng thời gian chờ. |
| 2 | VinFast    | Time-consuming                | Đội technical support phải đọc log lỗi pin/sạc EV thủ công để phân loại ticket bảo hành, gây quá tải vào giờ cao điểm.                                                   |
| 3 | Vinhomes   | Time-consuming + AI-upgrade   | Nhân viên CSKH phải phản hồi thủ công hàng trăm review tiêu cực và ticket cư dân mỗi ngày, phản hồi thiếu nhất quán và chậm.                                             |
| 4 | Vinmec     | Stakeholder Pain              | Hotline đặt lịch khám thường quá tải vào giờ cao điểm khiến bệnh nhân chờ lâu hoặc bỏ cuộc giữa chừng.                                                                   |
| 5 | Vinpearl   | AI-upgrade                    | Chatbot đặt phòng/vé hiện tại phản hồi cứng nhắc, không xử lý tốt các yêu cầu nhiều bước như đổi lịch hoặc combo gia đình.                                               |
| 6 | Xanh SM    | Repetitive                    | Điều phối viên phải route lại tài xế EV thủ công khi pin yếu hoặc khu vực có nhu cầu khách tăng đột biến.                                                                |
| 7 | VinFast    | Stakeholder Pain              | Chủ xe EV lo lắng về việc hết pin giữa đường nhưng hệ thống hiện chưa dự đoán chủ động nguy cơ “range anxiety” theo traffic thực tế.                                     |
| 8 | Vinhomes   | Repetitive                    | Ban quản lý tòa nhà phải phân loại thủ công ticket bảo trì như điện nước, thang máy, internet trước khi chuyển đúng đội xử lý.                                           |

---

# 🃏 Phase 2 — QUICK-ASSESS
# 🃏 Phase 2 — QUICK-ASSESS

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu):                                           │
│ Tài xế Xanh SM gặp tình trạng pin yếu hoặc lỗi sạc giữa     │
│ đường, khiến điều phối viên phải xử lý thủ công để tìm      │
│ trạm sạc phù hợp hoặc điều xe cứu hộ.                       │
│                                                             │
│ Công ty thành viên:                                         │
│ [ ] VinFast   [x] Xanh SM   [ ] Vinhomes                    │
│ [ ] Vinmec    [ ] Khác: ____________________                │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ - Tài xế Xanh SM                                            │
│ - Điều phối viên vận hành                                   │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Tài xế gọi hotline báo pin yếu                         │
│   → 2. Điều phối viên kiểm tra GPS và mức pin               │
│   → 3. Tra cứu thủ công trạm sạc còn slot                   │
│   → 4. Soạn tin nhắn hướng dẫn tài xế                       │
│   → 5. Điều xe cứu hộ nếu pin quá thấp                      │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Bước 3–4 (⏱ ~10–15 phút/lượt)                               │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ - Tự động tìm trạm sạc phù hợp theo GPS + traffic realtime  │
│ - Draft tin nhắn điều phối cho tài xế                       │
│ - Trigger xe cứu hộ nếu pin dưới ngưỡng an toàn             │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ - Giảm thời gian xử lý từ 15 phút → dưới 3 phút             │
│ - Giảm 40% workload thủ công cho dispatcher                 │
│ - Giảm tỷ lệ xe chết pin giữa đường xuống <1%               │
│                                                             │
│ Quick Architecture:                                         │
│ [ ] No AI   [x] Rule   [x] LLM   [x] Agent                  │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu):                                           │
│ Phản ánh cư dân trên ứng dụng Vinhomes Resident đang được   │
│ phân loại thủ công, gây chậm phản hồi và route sai đội xử lý│
│                                                             │
│ Công ty thành viên:                                         │
│ [ ] VinFast   [ ] Xanh SM   [x] Vinhomes                    │
│ [ ] Vinmec    [ ] Khác: ____________________                │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ - Nhân viên CSKH                                            │
│ - Ban quản lý tòa nhà                                       │
│ - Cư dân                                                    │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Cư dân gửi phản ánh trên app                           │
│   → 2. CSKH đọc và phân loại vấn đề                         │
│   → 3. Chuyển ticket cho đúng bộ phận                       │
│   → 4. Soạn phản hồi cập nhật cho cư dân                    │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Bước 2–3 (⏱ ~8–12 phút/phản ánh)                            │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ - Tự động phân loại ticket                                  │
│ - Route đúng đội kỹ thuật / ban quản lý                     │
│ - Draft phản hồi chuyên nghiệp cho cư dân                   │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ - 85% ticket được route đúng dưới 10 giây                   │
│ - Giảm thời gian phản hồi đầu tiên từ 15 phút → dưới 2 phút │
│ - Giảm 50% workload phân loại thủ công                      │
│                                                             │
│ Quick Architecture:                                         │
│ [ ] No AI   [x] Rule   [x] LLM   [ ] Agent                  │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu):                                           │
│ Đội vận hành Xanh SM phải nghe lại ghi âm và đọc ghi chú    │
│ thủ công để xác định lý do khách hủy chuyến.                │
│                                                             │
│ Công ty thành viên:                                         │
│ [ ] VinFast   [x] Xanh SM   [ ] Vinhomes                    │
│ [ ] Vinmec    [ ] Khác: ____________________                │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ - Đội phân tích vận hành                                    │
│ - Quản lý fleet & dispatch                                  │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Thu thập log hủy chuyến                                │
│   → 2. Nghe ghi âm cuộc gọi                                 │
│   → 3. Gán nhãn lý do hủy thủ công                          │
│   → 4. Tổng hợp báo cáo vận hành                            │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Bước 2–3 (⏱ ~5–6 phút/case)                                 │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ - Speech-to-text chuyển ghi âm thành văn bản                │
│ - LLM tự động phân loại lý do hủy chuyến                    │
│ - Tạo dashboard insight theo khu vực/thời gian              │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ - Giảm thời gian phân tích từ 6 phút → dưới 1 phút/case     │
│ - Tăng độ chính xác phân loại lý do hủy >90%                │
│ - Phát hiện hotspot hủy chuyến realtime                     │
│                                                             │
│ Quick Architecture:                                         │
│ [ ] No AI   [ ] Rule   [x] LLM   [x] Agent                  │
└─────────────────────────────────────────────────────────────┘

Họ và tên : Phạm Văn Mạnh
Email: pham95168@gmail.com
Github username : manhdepzi
DIscord username: pham_van_manh_2a202600837
<!-- # 🔍 Phase 1 — SCAN

| # | Subsidiary | Lens                          | Mô tả ngắn bài toán                                                                                                                                            |
| - | ---------- | ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1 | Xanh SM    | Stakeholder Pain + Repetitive | Tài xế thường phàn nàn hệ thống gợi ý điểm đón khách chưa chính xác tại sân bay/trung tâm thương mại, dẫn đến thời gian đón lâu và bị huỷ chuyến.              |
| 2 | VinFast    | Repetitive + Time-consuming   | Bộ phận hỗ trợ kỹ thuật phải xử lý hàng nghìn ticket liên quan lỗi pin/sạc EV mỗi ngày, phần lớn là các case lặp lại nhưng vẫn cần nhân viên đọc log thủ công. |
| 3 | Vinhomes   | Time-consuming                | Nhân viên CSKH mất nhiều thời gian đọc và phản hồi review 1-star từ cư dân trên app/community group.                                                           |
| 4 | Vinmec     | Stakeholder Pain              | Bệnh nhân thường phải chờ lâu khi đặt lịch khám vì hotline quá tải, đặc biệt giờ cao điểm.                                                                     |
| 5 | Vinpearl   | AI-upgrade                    | Chatbot hỗ trợ đặt vé/voucher hoạt động cứng nhắc, không hiểu câu hỏi đa bước hoặc khách muốn đổi lịch linh hoạt.                                              |
| 6 | Xanh SM    | Repetitive                    | Điều phối viên phải route lại tài xế EV khi pin yếu và nhu cầu khách thay đổi theo thời gian thực.                                                             |
| 7 | VinFast    | Stakeholder Pain              | Khách hàng EV lo lắng về “range anxiety” nhưng hệ thống hiện tại chưa cảnh báo chủ động rủi ro hết pin theo điều kiện giao thông thực tế.                      |
| 8 | Vinhomes   | AI-upgrade                    | Ban quản lý cư dân nhận quá nhiều ticket bảo trì giống nhau (điện nước/thang máy/internet) nhưng chưa có hệ thống AI phân loại ưu tiên tự động.                |

---

# 🃏 Phase 2 — QUICK-ASSESS

────────────────────────────────────────────
QUICK PROBLEM CARD #1
────────────────────────────────────────────

Bài toán (1 câu):
Hệ thống Xanh SM hiện gợi ý điểm đón khách chưa chính xác tại các khu vực đông đúc như sân bay hoặc trung tâm thương mại.

Công ty thành viên:
[X] Xanh SM

Ai đang đau (Actor)?

* Tài xế Xanh SM
* Khách hàng
* Dispatcher vận hành

Workflow thủ công hiện tại:

1. Khách đặt xe
2. Hệ thống chọn điểm đón mặc định
3. Tài xế gọi điện xác nhận vị trí
4. Khách/tài xế tìm nhau
5. Huỷ chuyến hoặc đón trễ

Bước nào tốn thời gian/lỗi nhất?

* Bước 3–4
* ⏱ 5–10 phút/chuyến tại giờ cao điểm

AI có thể nhảy vào hỗ trợ ở bước nào?

* AI dự đoán “pickup hotspot” tối ưu dựa trên:

  * GPS lịch sử
  * camera giao thông
  * heatmap đón khách thành công
  * traffic realtime

Đo thành công bằng gì?

* Giảm tỷ lệ huỷ chuyến từ 18% → dưới 8%
* Giảm thời gian tìm khách từ 7 phút → dưới 2 phút

Quick Architecture:
[ ] No AI
[ ] Rule
[X] LLM
[X] Agent

---

────────────────────────────────────────────
QUICK PROBLEM CARD #2
────────────────────────────────────────────

Bài toán (1 câu):
VinFast đang xử lý ticket lỗi pin EV thủ công gây quá tải cho đội technical support.

Công ty thành viên:
[X] VinFast

Ai đang đau (Actor)?

* Technical support team
* Chủ xe EV
* Call center

Workflow thủ công hiện tại:

1. Khách gọi hotline/app support
2. Nhân viên đọc mô tả lỗi
3. Mở log pin/charging
4. Đối chiếu knowledge base
5. Escalate kỹ sư nếu cần

Bước nào tốn thời gian/lỗi nhất?

* Bước 3–4
* ⏱ 15–25 phút/ticket

AI có thể nhảy vào hỗ trợ ở bước nào?

* AI đọc log lỗi pin tự động
* Tóm tắt nguyên nhân khả thi
* Đề xuất SOP xử lý phù hợp

Đo thành công bằng gì?

* Giảm thời gian xử lý ticket từ 20 phút → dưới 5 phút
* Giảm 40% số ticket cần escalate kỹ sư

Quick Architecture:
[ ] No AI
[X] Rule
[X] LLM
[ ] Agent

---

────────────────────────────────────────────
QUICK PROBLEM CARD #3
────────────────────────────────────────────

Bài toán (1 câu):
Nhân viên Vinhomes mất nhiều thời gian phản hồi review tiêu cực của cư dân trên app/community channels.

Công ty thành viên:
[X] Vinhomes

Ai đang đau (Actor)?

* CSKH cư dân
* Ban quản lý toà nhà
* Cư dân

Workflow thủ công hiện tại:

1. Nhân viên đọc review
2. Xác định mức độ nghiêm trọng
3. Soạn phản hồi thủ công
4. Chuyển ticket cho bộ phận liên quan
5. Theo dõi xử lý

Bước nào tốn thời gian/lỗi nhất?

* Bước 2–3
* ⏱ 10–15 phút/review

AI có thể nhảy vào hỗ trợ ở bước nào?

* AI sentiment analysis
* Auto-draft phản hồi chuyên nghiệp
* Tự động phân loại ticket urgency

Đo thành công bằng gì?

* Giảm thời gian phản hồi từ 12 phút → dưới 2 phút
* Tăng CSAT cư dân từ 78% → 90%

Quick Architecture:
[ ] No AI
[X] Rule
[X] LLM
[ ] Agent -->


# 🔍 Phase 1 — SCAN

| # | Subsidiary | Lens                          | Mô tả ngắn bài toán                                                                                                                                                      |
| - | ---------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1 | Xanh SM    | Stakeholder Pain + Repetitive | Tài xế thường mất nhiều thời gian tìm khách tại sân bay, Vincom hoặc khu đông người do hệ thống gợi ý điểm đón chưa chính xác, dẫn tới huỷ chuyến và tăng thời gian chờ. |
| 2 | VinFast    | Time-consuming                | Đội technical support phải đọc log lỗi pin/sạc EV thủ công để phân loại ticket bảo hành, gây quá tải vào giờ cao điểm.                                                   |
| 3 | Vinhomes   | Time-consuming + AI-upgrade   | Nhân viên CSKH phải phản hồi thủ công hàng trăm review tiêu cực và ticket cư dân mỗi ngày, phản hồi thiếu nhất quán và chậm.                                             |
| 4 | Vinmec     | Stakeholder Pain              | Hotline đặt lịch khám thường quá tải vào giờ cao điểm khiến bệnh nhân chờ lâu hoặc bỏ cuộc giữa chừng.                                                                   |
| 5 | Vinpearl   | AI-upgrade                    | Chatbot đặt phòng/vé hiện tại phản hồi cứng nhắc, không xử lý tốt các yêu cầu nhiều bước như đổi lịch hoặc combo gia đình.                                               |
| 6 | Xanh SM    | Repetitive                    | Điều phối viên phải route lại tài xế EV thủ công khi pin yếu hoặc khu vực có nhu cầu khách tăng đột biến.                                                                |
| 7 | VinFast    | Stakeholder Pain              | Chủ xe EV lo lắng về việc hết pin giữa đường nhưng hệ thống hiện chưa dự đoán chủ động nguy cơ “range anxiety” theo traffic thực tế.                                     |
| 8 | Vinhomes   | Repetitive                    | Ban quản lý tòa nhà phải phân loại thủ công ticket bảo trì như điện nước, thang máy, internet trước khi chuyển đúng đội xử lý.                                           |

---

# 🃏 Phase 2 — QUICK-ASSESS
# 🃏 Phase 2 — QUICK-ASSESS

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu):                                           │
│ Tài xế Xanh SM gặp tình trạng pin yếu hoặc lỗi sạc giữa     │
│ đường, khiến điều phối viên phải xử lý thủ công để tìm      │
│ trạm sạc phù hợp hoặc điều xe cứu hộ.                       │
│                                                             │
│ Công ty thành viên:                                         │
│ [ ] VinFast   [x] Xanh SM   [ ] Vinhomes                    │
│ [ ] Vinmec    [ ] Khác: ____________________                │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ - Tài xế Xanh SM                                            │
│ - Điều phối viên vận hành                                   │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Tài xế gọi hotline báo pin yếu                         │
│   → 2. Điều phối viên kiểm tra GPS và mức pin               │
│   → 3. Tra cứu thủ công trạm sạc còn slot                   │
│   → 4. Soạn tin nhắn hướng dẫn tài xế                       │
│   → 5. Điều xe cứu hộ nếu pin quá thấp                      │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Bước 3–4 (⏱ ~10–15 phút/lượt)                               │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ - Tự động tìm trạm sạc phù hợp theo GPS + traffic realtime  │
│ - Draft tin nhắn điều phối cho tài xế                       │
│ - Trigger xe cứu hộ nếu pin dưới ngưỡng an toàn             │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ - Giảm thời gian xử lý từ 15 phút → dưới 3 phút             │
│ - Giảm 40% workload thủ công cho dispatcher                 │
│ - Giảm tỷ lệ xe chết pin giữa đường xuống <1%               │
│                                                             │
│ Quick Architecture:                                         │
│ [ ] No AI   [x] Rule   [x] LLM   [x] Agent                  │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu):                                           │
│ Phản ánh cư dân trên ứng dụng Vinhomes Resident đang được   │
│ phân loại thủ công, gây chậm phản hồi và route sai đội xử lý│
│                                                             │
│ Công ty thành viên:                                         │
│ [ ] VinFast   [ ] Xanh SM   [x] Vinhomes                    │
│ [ ] Vinmec    [ ] Khác: ____________________                │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ - Nhân viên CSKH                                            │
│ - Ban quản lý tòa nhà                                       │
│ - Cư dân                                                    │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Cư dân gửi phản ánh trên app                           │
│   → 2. CSKH đọc và phân loại vấn đề                         │
│   → 3. Chuyển ticket cho đúng bộ phận                       │
│   → 4. Soạn phản hồi cập nhật cho cư dân                    │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Bước 2–3 (⏱ ~8–12 phút/phản ánh)                            │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ - Tự động phân loại ticket                                  │
│ - Route đúng đội kỹ thuật / ban quản lý                     │
│ - Draft phản hồi chuyên nghiệp cho cư dân                   │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ - 85% ticket được route đúng dưới 10 giây                   │
│ - Giảm thời gian phản hồi đầu tiên từ 15 phút → dưới 2 phút │
│ - Giảm 50% workload phân loại thủ công                      │
│                                                             │
│ Quick Architecture:                                         │
│ [ ] No AI   [x] Rule   [x] LLM   [ ] Agent                  │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu):                                           │
│ Đội vận hành Xanh SM phải nghe lại ghi âm và đọc ghi chú    │
│ thủ công để xác định lý do khách hủy chuyến.                │
│                                                             │
│ Công ty thành viên:                                         │
│ [ ] VinFast   [x] Xanh SM   [ ] Vinhomes                    │
│ [ ] Vinmec    [ ] Khác: ____________________                │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ - Đội phân tích vận hành                                    │
│ - Quản lý fleet & dispatch                                  │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Thu thập log hủy chuyến                                │
│   → 2. Nghe ghi âm cuộc gọi                                 │
│   → 3. Gán nhãn lý do hủy thủ công                          │
│   → 4. Tổng hợp báo cáo vận hành                            │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Bước 2–3 (⏱ ~5–6 phút/case)                                 │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ - Speech-to-text chuyển ghi âm thành văn bản                │
│ - LLM tự động phân loại lý do hủy chuyến                    │
│ - Tạo dashboard insight theo khu vực/thời gian              │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ - Giảm thời gian phân tích từ 6 phút → dưới 1 phút/case     │
│ - Tăng độ chính xác phân loại lý do hủy >90%                │
│ - Phát hiện hotspot hủy chuyến realtime                     │
│                                                             │
│ Quick Architecture:                                         │
│ [ ] No AI   [ ] Rule   [x] LLM   [x] Agent                  │
└─────────────────────────────────────────────────────────────┘
