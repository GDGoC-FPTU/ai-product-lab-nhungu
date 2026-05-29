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
