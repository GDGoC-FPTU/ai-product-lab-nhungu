# 01 — Problem Scan & Quick Cards (Bài cá nhân)

> **Họ và tên:** 🔧 Dương Quang Khải
> **MSSV / Email:** 🔧 duongkhai222204pt@gmail.com
> **Nhóm:** 🔧 null
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
