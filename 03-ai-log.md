# Phase 6 — Rule / Workflow / Agent + Decision

## Bước 6.0 — Ma trận độ phù hợp với AI

### Bài toán nằm ở ô:

* Độ mơ hồ thấp
* Độ phức tạp trung bình/cao

### Vì sao?

* Checklist giấy tờ tương đối rõ
* Workflow gồm nhiều bước và nhiều lần handoff
* Không cần AI tự lập kế hoạch phức tạp

---

## Bước 6.1 — So sánh Rule / Workflow / Agent

| Mức      | Phương án cho bài toán nhóm       | Khi nào đủ                   | Rủi ro                          | Chọn?   |
| -------- | --------------------------------- | ---------------------------- | ------------------------------- | ------- |
| Rule     | Check format và checklist cố định | Hồ sơ chuẩn hóa cao          | Không đọc được nội dung ảnh/PDF | Partial |
| Workflow | AI + automation + human review    | Quy trình nhiều bước rõ ràng | OCR sai hoặc false positive     | Yes     |
| Agent    | AI tự quyết định toàn bộ flow     | Khi workflow biến động mạnh  | Khó kiểm soát và audit          | No      |

### Mức chọn:

Workflow

### Vì sao chọn:

* Các bước xử lý khá rõ
* Có thể automation nhiều bước nhưng vẫn cần human review cuối
* Không cần AI tự suy luận chiến lược phức tạp

### Vì sao không chọn mức đơn giản hơn:

* Rule-based không đủ để đọc PDF/hình ảnh đa dạng
* Không xử lý tốt các case thiếu giấy tờ phức tạp

---

## Bước 6.2 — Problem Statement v1

| Field                        | Nội dung                                                |
| ---------------------------- | ------------------------------------------------------- |
| Actor                        | Cư dân và nhân viên BQL Vinhomes                        |
| Workflow                     | Đăng ký thi công nội thất và kiểm tra hồ sơ             |
| Bottleneck                   | Hồ sơ thiếu/sai khiến BQL xử lý thủ công nhiều vòng     |
| Impact                       | Tăng thời gian xử lý và trải nghiệm cư dân kém          |
| Success Metric               | Giảm 50% số lần trả hồ sơ, giảm 60% thời gian pre-check |
| Boundary                     | AI không approve hồ sơ cuối cùng                        |
| AI intervention point        | Pre-check hồ sơ và phản hồi thiếu giấy tờ               |
| Mức chọn                     | Workflow                                                |
| Rủi ro & người thật kiểm tra | Human review final trước approval                       |

---

## Bước 6.3 — Final decision

| Câu hỏi                                      | Yes / Not Yet / No | Ghi chú                 |
| -------------------------------------------- | ------------------ | ----------------------- |
| Actor và workflow đã rõ chưa?                | Yes                | Có workflow cụ thể      |
| Baseline và success metric đã đo được chưa?  | Not Yet            | Chưa có số liệu thực tế |
| Có data/input đủ dùng chưa?                  | Not Yet            | Cần sample hồ sơ        |
| Nếu AI sai, hậu quả có chấp nhận được không? | Yes                | Có human review         |
| Có người review/owner vận hành không?        | Yes                | BQL                     |
| Có cách non-AI đơn giản hơn không?           | Yes                | Rule-based checklist    |

### Decision:

Go

### Lý do:

* Pain thực tế rõ
* Workflow ổn định
* Có thể pilot nhỏ với rủi ro thấp

### Nếu Go, pilot nhỏ nhất là:

* AI check checklist hồ sơ PDF cơ bản cho 1 loại thủ tục nội thất
* Human review toàn bộ output AI trong giai đoạn pilot


Trong buổi Lab này, tôi sử dụng AI (ChatGPT và Gemini) như một “thought-partner” để hỗ trợ quá trình phân tích và scoping bài toán AI cho Vinhomes Grand Park. Chủ đề nhóm tôi lựa chọn là bài toán tối ưu hóa quy trình xử lý thủ tục cư dân tại Vinhomes Grand Park thông qua hệ thống “PermitFlow AI” — AI Copilot hỗ trợ kiểm tra và pre-review hồ sơ hành chính của cư dân.

## 1. AI đã giúp gì?

AI hỗ trợ tôi nhiều nhất ở giai đoạn brainstorm và mở rộng góc nhìn bài toán. Ban đầu, tôi chỉ nghĩ theo hướng khá phổ biến như chatbot cư dân hoặc trợ lý hỏi đáp tự động. Tuy nhiên, khi trao đổi với AI, tôi được gợi ý nhìn vấn đề từ góc độ “administrative friction” — tức ma sát hành chính giữa cư dân và ban quản lý.

Từ đó, bài toán được chuyển hướng thành:

* AI hỗ trợ pre-check hồ sơ thi công nội thất,
* kiểm tra giấy tờ thiếu,
* OCR đọc file cư dân upload,
* draft phản hồi bổ sung hồ sơ cho Ban Quản Lý.

AI cũng hỗ trợ tôi:

* brainstorm workflow hiện tại,
* xác định bottleneck,
* viết Problem Statement theo format 6-field,
* phân tích AI Fit giữa Rule-based vs LLM vs Human-in-the-loop,
* đề xuất Operational Boundary phù hợp với môi trường enterprise.

Ngoài ra, tôi còn sử dụng AI để brainstorm các tình huống adversarial nhằm kiểm tra ranh giới an toàn của hệ thống, ví dụ:

* cố tình yêu cầu AI “auto approve” hồ sơ,
* bỏ qua giấy tờ mandatory,
* hoặc ưu tiên xử lý cho “cư dân VIP”.

Điều này giúp tôi hiểu rõ hơn rằng khi thiết kế AI cho môi trường vận hành thực tế, boundary và fallback quan trọng không kém accuracy.

---

## 2. AI đã sai gì?

Trong quá trình làm bài, AI nhiều lần đưa ra các giải pháp quá “AI-first” và chưa thực tế với workflow enterprise thật.

Ví dụ:
AI từng đề xuất sử dụng “fully autonomous AI agent” để tự động duyệt hồ sơ thi công nội thất mà không cần con người review. Tuy nhiên, sau khi phân tích lại, tôi nhận ra điều này không phù hợp vì:

* hồ sơ liên quan đến pháp lý và an toàn thi công,
* ảnh giấy tờ có thể mờ hoặc sai định dạng,
* nhiều trường hợp ngoại lệ cần Ban Quản Lý quyết định thủ công.

Ngoài ra, AI cũng từng hallucinate về việc hệ thống cư dân hiện tại của Vinhomes đã có “AI document verification pipeline”, trong khi thực tế đây chỉ là giả định và không có dữ liệu xác nhận chính thức.

Một lỗi khác là AI ban đầu đề xuất workflow quá phức tạp với nhiều multi-agent orchestration không cần thiết. Sau khi đối chiếu rubric của Lab, tôi nhận ra một giải pháp Rule + LLM Feature đơn giản sẽ phù hợp và thực tế hơn nhiều.

---

## 3. Tôi đã sửa đổi như thế nào?

Sau khi nhận ra các vấn đề trên, tôi đã thay đổi cách prompt AI theo hướng:

* problem-first thay vì AI-first,
* yêu cầu AI phân biệt rõ:

  * task nào dùng Rule-based,
  * task nào dùng LLM,
  * task nào bắt buộc Human-in-the-loop.

Tôi cũng bổ sung Operational Boundary rõ ràng hơn trong system prompt:

* AI chỉ được pre-check hồ sơ,
* AI không được tự approve,
* AI không được bỏ qua mandatory documents,
* mọi quyết định cuối cùng phải do Ban Quản Lý xác nhận.

Ngoài ra, tôi bổ sung thêm fallback flow:

* nếu AI confidence thấp,
* OCR không đọc rõ giấy tờ,
* hoặc hồ sơ nằm ngoài template chuẩn,
  → hệ thống phải route về manual review thay vì tự xử lý.

Qua bài Lab này, tôi nhận ra AI rất mạnh trong việc hỗ trợ brainstorming, tổng hợp workflow và tạo prototype nhanh. Tuy nhiên, AI không tự hiểu business constraint nếu người dùng không đặt boundary rõ ràng. Việc thiết kế AI cho doanh nghiệp không chỉ là “làm AI thông minh hơn”, mà còn là thiết kế giới hạn phù hợp để AI hoạt động an toàn trong môi trường thực tế.
