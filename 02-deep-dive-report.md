# Báo Cáo Phân Tích Sâu Dự Án AI (Deep-Dive Report) - Nhóm

* **Tên nhóm:** [Điền tên nhóm của bạn tại đây]
* **Danh sách thành viên:**
  1. Lê Thiên Khang - MSSV: 2A202600726 (Trưởng nhóm)
  2. [Điền họ và tên thành viên 2 tại đây] - MSSV: [Điền MSSV thành viên 2]
  3. [Điền họ và tên thành viên 3 tại đây] - MSSV: [Điền MSSV thành viên 3]

---

# PHASE 3 — DEEP-DIVE

## UrbanOps Copilot — Vinhomes Smart City Incident Response

---

# 3.1 Current-State Workflow Mapping

## Current Workflow (Hiện tại)

```text
┌────────────────────┐
│ Bước 1             │
│ Cư dân gọi hotline │
│ hoặc gửi ticket    │
│ qua app cư dân     │
│ ⏱ 3 phút           │
└─────────┬──────────┘
          │ 🔄 Handoff
          ▼
┌────────────────────┐
│ Bước 2             │
│ CSKH đọc ticket    │
│ và tạo incident    │
│ thủ công            │
│ ⏱ 5 phút 🔴        │
└─────────┬──────────┘
          │ 🔄 Handoff
          ▼
┌────────────────────┐
│ Bước 3             │
│ Ban quản lý gọi    │
│ bảo vệ/kỹ thuật    │
│ để xác minh        │
│ ⏱ 8 phút 🔴        │
└─────────┬──────────┘
          │ 🔄 Handoff
          ▼
┌────────────────────┐
│ Bước 4             │
│ Update tình trạng  │
│ qua Zalo/group chat│
│ nội bộ             │
│ ⏱ 5 phút 🔴        │
└─────────┬──────────┘
          ▼
┌────────────────────┐
│ Bước 5             │
│ Escalate nếu       │
│ cư dân tiếp tục    │
│ phản ứng/livestream│
└────────────────────┘
```

## 3.2. Problem Statement (6-field) & Metrics (15 min)
Điền đầy đủ 6 trường thông tin của bài toán:

| Field | Nội dung chi tiết |
|---|---|

| Field                       | Nội dung                                                                                                                                                                                
| **1. Actor / Operator**     | Ban quản lý tòa nhà, CSKH cư dân, bảo vệ nội khu và đội kỹ thuật vận hành                                                                                                                                                                                                                                       |
| **2. Current Workflow**     | Khi có sự cố cư dân, CSKH tiếp nhận ticket từ hotline hoặc app cư dân rồi tạo incident thủ công. Ban quản lý phải gọi bảo vệ hoặc kỹ thuật để xác minh tình hình và cập nhật tiến độ qua Zalo/group chat nội bộ                                                                                                 |
| **3. Bottleneck**           | Không có hệ thống tổng hợp context và đánh giá mức độ nghiêm trọng theo thời gian thực. Việc đọc ticket, phân loại severity và điều phối xử lý phụ thuộc nhiều vào kinh nghiệm cá nhân                                                                                                                          |
| **4. Business Impact**      | Chậm phản ứng làm tăng nguy cơ cư dân livestream, public post hoặc khiếu nại trên mạng xã hội, ảnh hưởng resident satisfaction và hình ảnh thương hiệu Vinhomes                                                                                                                                                 |
| **5. Success Metric**       | 80% incident được phân loại severity và đề xuất action dưới 10 giây. Giảm thời gian phản ứng trung bình từ 20 phút xuống dưới 5 phút và giảm 30% incident escalation lên social media                                                                                                                           |
| **6. Operational Boundary** | AI được phép: tóm tắt context, phân loại severity, đề xuất action draft và draft communication cho Ban Quản Lý. AI tuyệt đối KHÔNG được: tự gửi thông báo cho cư dân, khóa thẻ cư dân, xử phạt cư dân, gọi cơ quan chức năng hoặc đưa ra kết luận pháp lý. Mọi action đều phải được Human-in-the-loop phê duyệt |

## 3.3. Future-State Flow & AI Fit (25 min)
* **Xác định mức AI Fit (AI-Fit Matrix):** Giải pháp thuộc nhóm nào? [ ] Rule / State-Machine [ ] LLM Feature [ ] Agentic Loop.
* **Vẽ Future-State Flow:** Đánh dấu rõ:
  * 🔵 **AI Step:** Tác vụ LLM xử lý.
  * 🟢 **Human Step (HITL):** Bước con người phê duyệt/review (Human-in-the-loop).
  * ↩️ **Fallback:** Kế hoạch dự phòng khi LLM trả về kết quả lỗi hoặc không tự tin.

---
AI-Fit Matrix :
Bài toán chứa nhiều dữ liệu ngôn ngữ tự nhiên như:

complaint ticket,
hotline transcript,
mô tả sự cố,
group chat nội bộ.

LLM phù hợp để:

summarize context,
classify severity,
draft communication,
hỗ trợ decision-making.
LLM Feature
```text
┌────────────────────┐
│ Bước 1             │
│ Incident từ        │
│ hotline/app cư dân │
└─────────┬──────────┘
          ▼
┌────────────────────┐
│ 🔵 AI Step         │
│ AI summarize       │
│ context + detect   │
│ escalation risk    │
│ ⏱ < 10 giây        │
└─────────┬──────────┘
          ▼
┌────────────────────┐
│ 🔵 AI Step         │
│ AI classify        │
│ severity level     │
│ + đề xuất action   │
└─────────┬──────────┘
          ▼
┌────────────────────┐
│ 🔵 AI Step         │
│ Draft communication│
│ cho BQL nội bộ     │
└─────────┬──────────┘
          ▼
┌────────────────────┐
│ 🟢 Human Step      │
│ Ban quản lý review │
│ và approve action  │
└─────────┬──────────┘
          ▼
┌────────────────────┐
│ Đội bảo vệ/kỹ thuật│
│ thực hiện xử lý    │
└────────────────────┘
```
# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [v] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?
Có thể sử dụng dữ liệu ticket cư dân từ app Vinhomes, hotline logs, lịch sử xử lý sự cố và group escalation nội bộ để tạo dataset ban đầu cho prototype.
2. [v] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?
Có. AI chỉ đóng vai trò hỗ trợ tóm tắt context, phân loại mức độ nghiêm trọng và draft action recommendation.
3. [v] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?
Có khả năng cao vì hệ thống giúp giảm áp lực vận hành real-time cho CSKH và Ban quản lý, đặc biệt trong các tình huống khẩn cấp hoặc có nguy cơ leo thang truyền thông.

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[x] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
Bắt đầu phát triển với scope hẹp.