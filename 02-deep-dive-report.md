# 02 — Deep-Dive Report (Bài nhóm)

> ## 👥 Thông tin nhóm (BẮT BUỘC điền đầy đủ)
>
> **Tên nhóm:** 🔧 null
>
> | # | Họ và tên | MSSV | Email đã đăng ký | Đóng góp chính |
> |---|-----------|------|------------------|----------------|
> | 1 | 🔧 _Họ tên_ | 🔧 | 🔧 | Code prompt_prototype.py |
> | 2 | 🔧 _Họ tên_ | 🔧 | 🔧 | Vẽ workflow diagram |
> | 3 | 🔧 _Họ tên_ | 🔧 | 🔧 | Viết Problem Statement & Evaluate |
> | 4 | 🔧 _Họ tên_ | 🔧 | 🔧 | Viết AI Log & tổng hợp báo cáo |
> | 5 | 🔧 _Họ tên_ | 🔧 | 🔧 | Phase 1 SCAN & Quick Cards |
> | 6 | 🔧 _Họ tên_ | 🔧 | 🔧 | Stress-test prompt & kiểm thử ranh giới |

---

## 🗳️ Quyết định lựa chọn bài toán

Nhóm thống nhất chọn bài toán **"Xanh SM — Xử lý sự cố hết pin thực địa"** để thực hiện Deep-Dive.

**Lý do lựa chọn và loại bỏ các thẻ khác:**
* **Loại Card Vinhomes (phản ánh cư dân):** Là tác vụ phân loại văn bản, phù hợp Rule-based router trước; rủi ro sai sót liên quan phí quản lý/tranh chấp căn hộ cần xử lý thận trọng hơn, chưa cấp thiết bằng.
* **Loại Card Hủy chuyến:** Là tác vụ phân tích offline (back-office), không tác động real-time đến hiệu suất vận hành như sự cố hết pin của tài xế đang trên đường.
* **Chọn Sự cố hết pin** vì: bài toán cụ thể, real-time, có metric đo được bằng số, ảnh hưởng trực tiếp tới doanh thu & an toàn giao thông, và ranh giới an toàn rõ ràng để stress-test bằng prompt.

---

## 🏗️ Phase 3 — DEEP-DIVE

### 3.1. Current-State Workflow (Quy trình hiện tại)

> 📌 Sơ đồ vẽ tay/bảng trắng của quy trình này được nộp kèm tại file `04-workflow-diagram.png`.

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Nhận cuộc    │ 🔄  │ Tra cứu định │ 🔄  │ Tra cứu trạm │ 🔄  │ Soạn văn bản │
│ gọi sự cố    │ ──→ │ vị GPS xe    │ ──→ │ sạc VinFast  │ ──→ │ chỉ đường    │
│              │     │              │     │ còn trụ trống│     │ gửi tài xế   │
│ Ai: Dispatch │     │ Ai: Dispatch │     │ Ai: Dispatch │     │ Ai: Dispatch │
│ ⏱ 2 phút     │     │ ⏱ 2 phút     │     │ ⏱ 5 phút 🔴  │     │ ⏱ 5 phút 🔴  │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                      │ 🔄
                                                                      ▼
                                                               ┌──────────────┐
                                                               │ Bước 5       │
                                                               │ Gọi xe cứu   │
                                                               │ hộ (nếu pin  │
                                                               │ đã cạn kiệt) │
                                                               │ ⏱ 1 phút     │
                                                               └──────────────┘

🔴 = Bottleneck    🔄 = Handoff (chuyển giao người ↔ hệ thống)
⏱ Tổng thời gian xử lý thủ công: ~15 phút/lượt.
```

**Phân tích:** Hai nút thắt cổ chai là **Bước 3 (tra cứu trạm sạc trống phù hợp loại cổng sạc)** và **Bước 4 (soạn tin chỉ đường tiếng Việt)**, cộng lại ~10/15 phút. Đây cũng là các bước có nhiều handoff thủ công và dễ sai (chỉ nhầm trạm không tương thích cổng sạc, hoặc chỉ trạm quá xa khi pin yếu).

### 3.2. Problem Statement (6-field)

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Điều phối viên (Dispatcher) tại Trung tâm Điều vận Xanh SM Hà Nội. |
| **2. Current Workflow** | Khi tài xế báo hết pin, điều phối viên tra vị trí GPS xe trên bản đồ nội bộ, mở Dashboard trạm sạc VinFast tìm trụ trống gần & phù hợp dòng xe, soạn tin chỉ đường gửi qua App tài xế, gọi cứu hộ nếu pin đã cạn. 5 bước hoàn toàn thủ công, ~15 phút/lượt. |
| **3. Bottleneck** | Bước 3 & 4 (~10 phút): tra cứu thủ công trụ sạc trống tương thích cổng sạc (VF5/VFe34/VF8) và soạn tin hướng dẫn đường đi tiếng Việt thân thiện. |
| **4. Business Impact** | ~80 sự cố pin thực địa/ngày tại Hà Nội → lãng phí ~20 giờ-người/ngày của team điều vận; tài xế chờ lâu, không đón được khách → rò rỉ doanh thu ước tính ~15% trong các lượt sự cố. |
| **5. Success Metric** | 1) Giảm thời gian xử lý sự cố từ 15 phút → **dưới 3 phút** (Efficiency). 2) Tỉ lệ chỉ đúng địa điểm & đúng loại trụ sạc đạt **≥ 98%** (Quality). |
| **6. Operational Boundary** | **Được phép:** truy xuất API vị trí xe, API trạm sạc trống, tự soạn tin **dạng nháp**. **TUYỆT ĐỐI CẤM:** tự động gửi tin cho tài xế khi chưa có điều phối viên duyệt (bắt buộc HITL — mọi nháp phải mang thẻ `[DRAFT_ONLY]`); chỉ trạm cách > 5km khi pin < 5% (phải chuyển sang điều **xe sạc pin di động**); đề xuất trạm không tương thích cổng sạc của xe. |

### 3.3. Future-State Flow & AI Fit

* **AI-Fit Matrix:** Chọn **LLM Feature**. Không dùng Agentic Loop tự trị vì quy trình có cấu trúc cố định và rủi ro cao (chỉ sai trạm khi pin yếu có thể khiến xe cạn pin giữa đường, gây tắc nghẽn giao thông) → cần con người chốt ở khâu cuối.

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Nhận cuộc    │     │ 🔵 Auto-pull │     │ 🔵 AI draft  │     │ 🟢 Dispatch  │
│ gọi sự cố    │ ──→ │ vị trí xe &  │ ──→ │ tin chỉ dẫn  │ ──→ │ review &     │
│              │     │ trạm sạc trống│    │ [DRAFT_ONLY] │     │ click gửi    │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                  │
                                                  ▼
                                          ↩️ Fallback:
                                  - Nếu pin < 5%: AI KHÔNG chỉ trạm xa,
                                    tự bật JSON dispatch_mobile_charger.
                                  - Nếu AI draft lỗi/không tự tin:
                                    Dispatcher tự viết tay như quy trình cũ.

🔵 AI Step   🟢 Human-in-the-loop (bắt buộc duyệt)   ↩️ Fallback
```

* **🔵 AI Step:** Tự động lấy vị trí + trạm trống và soạn nháp tin chỉ đường.
* **🟢 Human Step (HITL):** Điều phối viên đọc & bấm duyệt trước khi tin được gửi cho tài xế.
* **↩️ Fallback:** (1) Pin < 5% → mô hình bắt buộc trả JSON `{"action": "dispatch_mobile_charger", ...}` thay vì chỉ trạm xa; (2) Mô hình lỗi/không chắc → quay về quy trình thủ công cũ.

---

## 🏁 Phase 5 — EVALUATE

### AI Readiness Checklist

| # | Câu hỏi | Trả lời | Ghi chú |
|---|---------|---------|---------|
| 1 | Có sẵn dữ liệu mẫu/logs sạch để test? | ✅ Có | Log sự cố pin + API vị trí xe + Dashboard trạm sạc đã tồn tại. |
| 2 | Rủi ro khi AI sai có kiểm soát được (HITL/Fallback)? | ✅ Có | Bắt buộc `[DRAFT_ONLY]` + dispatcher duyệt; pin<5% bật cứu hộ. |
| 3 | Stakeholders sẵn sàng đổi quy trình cũ? | ✅ Có | Team điều vận đang quá tải, mong muốn được hỗ trợ. |

### Quyết định cuối cùng

- [x] **GO** — Bắt đầu xây dựng Prototype với scope hẹp.
- [ ] NOT YET
- [ ] NO-GO

**Justification (luận điểm kỹ thuật & chi phí):**
> Bài toán cụ thể, có metric đo được (15 phút → dưới 3 phút; độ chính xác ≥ 98%). Giải pháp **LLM Feature** đơn giản nhưng hiệu quả: chỉ cần 1 lần gọi Gemini 2.5 Flash với system prompt ràng buộc ranh giới + dữ liệu vị trí/trạm sạc, không cần huấn luyện mô hình riêng. Ranh giới an toàn đã được **kiểm chứng bằng prompt prototype** (xem `extras/prompt_prototype.py` hoặc `starter-code/prompt_prototype.py`): cả 2 ranh giới (giữ thẻ `[DRAFT_ONLY]` & ngưỡng pin 5% → điều xe sạc di động) đều trụ vững trước test tấn công.
>
> **Ước lượng chi phí vận hành:** Gemini 2.5 Flash rất rẻ cho tác vụ text ngắn. Mỗi sự cố ~vài nghìn token (input + output). Với ~80 sự cố/ngày (~2.400/tháng), chi phí API ước tính chỉ ở mức vài USD/tháng — không đáng kể so với ~20 giờ-người/ngày tiết kiệm được. ROI dương rõ rệt → quyết định **GO**.
