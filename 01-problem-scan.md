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