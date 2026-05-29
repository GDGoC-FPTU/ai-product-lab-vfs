## 🏛️ Bối cảnh: Tôi là ai?
---
# BÀI LÀM:
Tôi là Quỳnh, AI Engineer tại Vin Smart Future. Nhóm chúng tôi được giao nhiệm vụ phối hợp với Khối Vận Hành của Vinhomes Grand Park để tìm kiếm các cơ hội tối ưu hóa bằng trí tuệ nhân tạo trong quá trình quản lý cư dân và vận hành đô thị thông minh.

Thông qua quá trình khảo sát thực tế và nghiên cứu quy trình xử lý hồ sơ cư dân tại Vinhomes Grand Park — một đại đô thị với hàng chục nghìn cư dân — tôi nhận thấy Ban Quản Lý đang phải xử lý khối lượng lớn các thủ tục hành chính như đăng ký thi công nội thất, cấp thẻ xe, booking thang máy chuyển đồ và đăng ký khách ra vào mỗi ngày.

Tuy nhiên, phần lớn quy trình hiện tại vẫn mang tính thủ công: cư dân tải biểu mẫu, điền giấy tờ, gửi file qua app/email, sau đó nhân viên Ban Quản Lý phải tự kiểm tra từng hồ sơ để phát hiện giấy tờ thiếu, sai biểu mẫu hoặc ảnh không hợp lệ. Điều này dẫn đến việc hồ sơ bị trả lại nhiều lần, thời gian xử lý kéo dài và cư dân phải liên tục bổ sung giấy tờ.

Trong quá trình quan sát workflow thực tế, tôi nhận ra vấn đề lớn nhất không nằm ở việc thiếu ứng dụng quản lý, mà nằm ở “administrative friction” — ma sát hành chính giữa cư dân và hệ thống vận hành. Đây chính là bài toán mà nhóm tôi mang vào buổi Lab hôm nay: xây dựng một hệ thống AI Copilot hỗ trợ pre-check hồ sơ và giảm tải quy trình xử lý thủ tục cư dân cho Vinhomes Grand Park.
---
# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội (Cá nhân)

| # | Lăng kính           | Problem quan sát được                                                                    | Ai đang đau?              | Dấu hiệu thật                                            |
| - | ------------------- | ---------------------------------------------------------------------------------------- | ------------------------- | -------------------------------------------------------- |
| 1 | Tốn thời gian       | Cư dân thường điền sai hoặc thiếu thông tin trong hồ sơ đăng ký thi công nội thất        | Ban Quản Lý (BQL), cư dân | Hồ sơ bị trả đi trả lại nhiều lần, mất thời gian xử lý   |
| 2 | Lặp lại             | Nhân viên CSKH phải liên tục trả lời các câu hỏi giống nhau về giấy tờ và thủ tục cư dân | Nhân viên CSKH            | Tốn nhiều thời gian support các câu hỏi lặp lại mỗi ngày |
| 3 | AI-upgrade          | Quy trình đăng ký vé xe tháng và booking elevator vẫn làm thủ công qua giấy tờ/chat      | Cư dân, BQL               | Quy trình chậm, dễ sai sót và khó tracking trạng thái    |
| 4 | Pain từ stakeholder | Cư dân phải xuống BQL nhiều lần chỉ để bổ sung giấy tờ còn thiếu                         | Cư dân                    | Nhiều complain về trải nghiệm thủ tục bất tiện           |
| 5 | Tốn thời gian       | Nhân viên BQL phải tự kiểm tra từng file PDF/hình ảnh cư dân gửi lên                     | Nhân viên BQL             | Mất nhiều manpower để rà soát hồ sơ thủ công             |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards (Cá nhân)
---
# BÀI LÀM:
# QUICK PROBLEM CARD #1

Bài toán:
Cư dân Vinhomes thường nộp sai hoặc thiếu hồ sơ đăng ký thi công nội thất, khiến Ban Quản Lý phải kiểm tra và yêu cầu bổ sung thủ công nhiều lần.

Công ty thành viên: Vinhomes

Ai đang đau?

* Cư dân
* CSKH cư dân
* Ban quản lý tòa nhà

Workflow thủ công hiện tại:

1. Cư dân tải form PDF
2. Điền thủ công và gửi giấy tờ qua app/email
3. BQL kiểm tra từng file
4. Nếu thiếu → yêu cầu bổ sung
5. Cư dân gửi lại hồ sơ

Bước tốn thời gian/lỗi nhất:
Bước 3-4 (10-15 phút/hồ sơ)

AI có thể hỗ trợ:

* Kiểm tra thiếu giấy tờ
* OCR đọc hồ sơ
* Draft checklist bổ sung
* Tóm tắt hồ sơ cho BQL

Metric thành công:

* Giảm tỉ lệ hồ sơ bị trả từ 45% → dưới 15%
* Giảm thời gian review từ 15 phút → dưới 3 phút

Quick Architecture:
[x] Rule + LLM Feature

# QUICK PROBLEM CARD #2

Bài toán:
Cư dân mới chuyển vào Vinhomes thường gặp khó khăn khi hoàn tất các thủ tục move-in như đăng ký cư dân, khai báo xe, booking thang máy chuyển đồ và kích hoạt dịch vụ nội khu.

Công ty thành viên:
Vinhomes

Ai đang đau?

* Cư dân mới
* CSKH cư dân
* Ban quản lý tòa nhà

Workflow hiện tại:

1. Cư dân nhận căn hộ
2. Tự tìm hiểu thủ tục qua email/app
3. Điền nhiều form khác nhau
4. Gửi hồ sơ cho BQL
5. BQL kiểm tra và phản hồi thủ công
6. Cư dân bổ sung nếu thiếu

Bottleneck:

* Cư dân không hiểu quy trình
* Thiếu giấy tờ
* Booking sai thời gian
* CSKH trả lời lặp đi lặp lại

Bước tốn thời gian/lỗi nhất:
Bước 3-5 (⏱ 20-30 phút/cư dân)

AI có thể hỗ trợ:

* Personalized onboarding flow
* Checklist động theo từng loại căn hộ
* OCR đọc giấy tờ
* Draft form tự động
* Gợi ý lịch move-in phù hợp

Metric thành công:

* Giảm 60% ticket hỗ trợ move-in
* Giảm thời gian onboarding từ 2 ngày → vài giờ

Quick Architecture:
[x] Rule + LLM Feature

# QUICK PROBLEM CARD #3

Bài toán:
Ban quản lý Vinhomes nhận rất nhiều phản ánh về sự cố nội khu (thang máy, nước, điện, tiếng ồn, đỗ xe), nhưng việc tổng hợp và ưu tiên xử lý vẫn làm thủ công qua hotline và group chat.

Công ty thành viên:
Vinhomes

Ai đang đau?

* Ban quản lý
* Kỹ thuật vận hành
* CSKH cư dân

Workflow hiện tại:

1. Cư dân gọi hotline / gửi app
2. CSKH ghi nhận thủ công
3. Chuyển ticket qua Zalo/group nội bộ
4. Kỹ thuật xác minh
5. BQL ưu tiên xử lý theo kinh nghiệm cá nhân

Bottleneck:

* Ticket bị trùng
* Thiếu context
* Không xác định được severity
* Escalation chậm

Bước tốn thời gian/lỗi nhất:
Bước 2-4 (⏱ 10-15 phút/ticket)

AI có thể hỗ trợ:

* Gom nhóm ticket trùng lặp
* Tóm tắt sự cố
* Severity scoring
* Gợi ý đội xử lý phù hợp
* Predict escalation risk

Metric thành công:

* Giảm 40% thời gian điều phối
* Detect critical incident dưới 1 phút

Quick Architecture:
[x] LLM Feature

---

# BÀI LÀM:
# 🗳️ Quyết định lựa chọn của nhóm:

Nhóm quyết định chọn bài toán **"Card #1 — Vinhomes PermitFlow AI: AI hỗ trợ xử lý hồ sơ thi công & thủ tục cư dân"** để thực hiện Deep-Dive.

## Lý do lựa chọn và loại bỏ các thẻ khác:

* **Card #2 (Resident Move-in Copilot):** Mặc dù pain point onboarding cư dân mới là có thật, nhưng workflow hiện tại vẫn phụ thuộc mạnh vào chính sách riêng của từng tòa nhà và từng loại căn hộ. Dữ liệu quy trình chưa đủ chuẩn hóa giữa các khu đô thị Vinhomes, khiến việc xây dựng AI flow tổng quát khó đạt độ chính xác cao trong giai đoạn prototype đầu tiên.

* **Card #3 (Facility Incident Summarizer):** Đây là bài toán vận hành hấp dẫn nhưng mức độ rủi ro escalation cao. Nếu AI phân loại sai severity của sự cố (ví dụ: mất điện diện rộng hoặc sự cố thang máy), hệ thống có thể ảnh hưởng trực tiếp đến SLA vận hành và trải nghiệm cư dân. Ngoài ra, nhiều phần của workflow hiện tại có thể xử lý tốt bằng rule-based ticket routing trước khi cần tới LLM reasoning phức tạp.

## Vì sao nhóm chọn Card #1:

Bài toán hồ sơ thi công nội thất và thủ tục cư dân có:

* Workflow rõ ràng, ổn định và lặp lại mỗi ngày
* Pain point thực tế cho cả cư dân và Ban Quản Lý
* Dữ liệu đầu vào có cấu trúc tương đối tốt (PDF, CCCD, checklist giấy tờ)
* Rủi ro vận hành thấp hơn so với incident management real-time
* Phù hợp triển khai theo mô hình “Rule + LLM + Human-in-the-loop”

Quan trọng nhất:
AI không thay thế Ban Quản Lý Vinhomes, mà đóng vai trò “copilot” giúp:

* pre-check hồ sơ,
* phát hiện thiếu giấy tờ,
* draft phản hồi bổ sung,
* giảm ma sát hành chính cho cư dân.

Đây là bài toán có khả năng prototype nhanh, đo được hiệu quả rõ ràng và phù hợp với scope kỹ thuật của Vin Smart Future trong giai đoạn đầu.

