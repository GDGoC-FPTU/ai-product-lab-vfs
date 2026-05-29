# Lab 02 — Worksheet: AI Product Scoping (Vin Smart Future)

---

## 🏛️ 1. Bối cảnh thực tế: Vin Smart Future (Vingroup)

**Vingroup** — Tập đoàn tư nhân lớn nhất Việt Nam — vừa sáp nhập toàn bộ các phòng ban công nghệ thuộc các công ty thành viên thành một đơn vị công nghệ thống nhất mang tên **Vin Smart Future**. 

Nhiệm vụ của **Vin Smart Future** là xây dựng các giải pháp AI, số hóa, và tự động hóa cốt lõi để nâng cao hiệu suất vận hành và trải nghiệm khách hàng xuyên suốt các công ty thành viên:
* 🚗 **VinFast:** Hệ thống xe điện thông minh (EV), trợ lý AI ảo trong xe, dự đoán bảo trì pin, và quản lý chuỗi cung ứng sản xuất.
* 🚕 **Xanh SM (GSM):** Vận hành đội xe taxi/xe máy điện thông minh, điều vận thông minh (Smart Dispatching), tối ưu hóa lộ trình di chuyển.
* 🏢 **Vinhomes:** Quản lý đô thị thông minh (Smart Cities), trợ lý cư dân thông minh, tối ưu hóa mức tiêu thụ năng lượng.
* 🏥 **Vinmec:** Y tế thông minh, chẩn đoán hình ảnh bằng AI, tối ưu hóa quản lý hồ sơ bệnh án.
* 🎢 **Vinpearl / VinWonders:** Trải nghiệm du lịch số hóa, quản lý phòng và luồng khách thông minh tại các khu vui chơi.

Trong buổi Lab hôm nay, nhóm của bạn sẽ đóng vai trò là **AI Product Engineer** tại **Vin Smart Future**, tiến hành tìm kiếm, scoping, phân tích độ khả thi, thiết lập ranh giới vận hành, và xây dựng một **bản mẫu kỹ thuật (prompt prototype)** cho một bài toán cụ thể thuộc một trong những mảng kinh doanh trên.

---

## 📊 2. Cơ cấu tính điểm bài lab

### 👥 Điểm nhóm (60 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **G1. Workflow Mapping** | 20 | Problem Deep-Dive | Vẽ chi tiết quy trình hiện tại: các bước, handoff, thời gian, bottleneck |
| **G2. Problem Statement** | 20 | Problem Deep-Dive | Problem Statement 6-field bám sát thực tế, metric có số và ranh giới rõ ràng |
| **G3. AI Fit & Future Flow** | 10 | Problem Deep-Dive | So sánh Rule vs LLM vs Agent, future flow có bước AI, ranh giới và Fallback |
| **G4. Decision Quality** | 10 | Problem Deep-Dive | Quyết định Go/Not Yet/No-Go trung thực và có chứng cứ rõ ràng |

### 👤 Điểm cá nhân (40 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **I1. Scan & Cards** | 15 | Quick Cards | Liệt kê 5 problems sử dụng 3 lenses, hoàn thiện 3 quick cards chất lượng |
| **I2. Prototyping** | 10 | 02-lab/ | Chạy thử nghiệm programmatic prompt prototype thành công |
| **I3. AI Log & Reflection** | 15 | 03-ai-log.md | Phản ánh trung thực về việc dùng AI làm thought-partner (giúp gì, sai gì, sửa gì) |

---

# 🚀 Phase 0 — worked Example: Xanh SM Intelligent Dispatcher (15 min)

*Giảng viên walk-through ví dụ thực tế từ Vin Smart Future để bạn hiểu rõ cách scoping một bài toán AI.*
Đọc chi tiết worked example tại file [02-deliverable-example.md](02-deliverable-example.md).

---

# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng [Chọn một: VinFast / Xanh SM / Vinhomes / Vinmec]. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 |VinFast |Lặp lại & Tốn thời gian|Đối chiếu hóa đơn sạc điện từ các trạm sạc đối tác liên kết ngoài (đơn vị thứ ba) với dữ liệu thực thu trên hệ thống VinFast. Nhân viên kế toán phải tải file Excel đối soát hàng tuần từ các đối tác trạm sạc, dùng hàm VLOOKUP hoặc so khớp thủ công từng mã giao dịch, thời lượng sạc, dòng điện tiêu thụ và đơn giá để phát hiện chênh lệch lệch dòng tiền.Mất 12 - 16 giờ làm việc/tuần của một kế toán viên chuyên trách.
Tỷ lệ sai sót đối chiếu thủ công khoảng 1.5%, gây thất thoát trung bình 80,000,000 VND/tháng do bỏ sót các giao dịch lỗi hoặc thanh toán trùng lặp cho đối tác.
| 2 |Xanh SM | Tốn thời gian & Pain từ người khác |Tiếp nhận và xử lý thủ công các báo cáo khẩn cấp từ tài xế về sự cố pin yếu thực địa trên đường đón chở khách.Tài xế gọi điện lên tổng đài báo pin dưới 5%. Điều phối viên (Dispatcher) phải mở bản đồ nội bộ định vị vị trí xe, tìm trạm sạc VinFast còn trụ trống phù hợp gần nhất, soạn tin nhắn chỉ đường gửi lại tài xế, hoặc điều xe cứu hộ pin nếu xe cạn kiệt pin hoàn toàn.Mất 15 phút/lượt xử lý, trong giờ cao điểm tài xế phải xếp hàng chờ đợi cuộc gọi gây ức chế cực lớn.
Ước tính gây rò rỉ doanh thu ~15% trong khung giờ cao điểm do xe nằm im không đón được khách, cộng thêm chi phí cứu hộ phát sinh 500,000 VND/lượt nếu không điều hướng kịp thời đến trạm sạc gần nhất trước khi sập nguồn.
| 3 |Vinhomes |Lặp lại |Đọc, phân loại và chuyển tiếp thủ công các phản ánh, khiếu nại của cư dân (ví dụ: hỏng đèn hành lang, mất nước, tiếng ồn, đăng ký thẻ xe) gửi qua ứng dụng Vinhomes Resident.Thời gian phản hồi ban đầu bị kéo dài từ 4 - 12 tiếng gây phàn nàn lớn từ cư dân (SLA đạt dưới 75% vào giờ cao điểm). Tốn trung bình 1.5 nhân sự Full-time chỉ để ngồi phân loại và gõ tay chuyển tiếp yêu cầu tại mỗi khu đại đô thị lớn.
| 4 |Vinmec |Tốn thời gian |Bác sĩ soạn thảo bản tóm tắt từ ghi chú lâm sàng thô, kết quả xét nghiệm và đơn thuốc trên hệ thống bệnh án điện tử. Bác sĩ phải ngồi đọc lại toàn bộ tiến trình điều trị phức tạp của bệnh nhân, lọc các chỉ số quan trọng và viết lại bằng ngôn ngữ phổ thông, dễ hiểu để bệnh nhân và người nhà biết cách tự chăm sóc tại nhà.Bác sĩ mất từ 20 - 30 phút/bệnh nhân chỉ để làm công tác giấy tờ này, làm giảm thời gian khám chữa bệnh trực tiếp cho các bệnh nhân khác.
Làm tăng thời gian chờ đợi làm thủ tục ra viện của khách hàng lên trên 1.5 tiếng, gây ảnh hưởng nghiêm trọng tới chỉ số hài lòng của bệnh nhân
| 5 |Vinpearl |Pain từ người khác & AI có thể tốt hơn |Rà soát và phân tích các đánh giá (Reviews) của khách hàng trên các nền tảng OTA (Booking.com, Agoda, TripAdvisor, Google Maps) để tổng hợp khiếu nại khẩn cấp gửi quản lý khách sạn. Nhân viên truyền thông CSKH phải truy cập từng trang web hàng ngày, đọc hàng trăm đánh giá của khách bằng nhiều ngôn ngữ khác nhau, dịch sang tiếng Việt và copy các phàn nàn nghiêm trọng (như phòng bẩn, thái độ nhân viên kém) vào file báo cáo cuối ngày.Mất 3 - 4 tiếng/ngày của nhân viên để tổng hợp báo cáo thủ công.
Độ trễ xử lý các phàn nàn khẩn cấp lên tới 24 - 48 giờ, khiến khách hàng đã rời đi trước khi khách sạn kịp xin lỗi hoặc khắc phục, làm giảm điểm đánh giá trung bình từ 4.5 xuống dưới 4.0, trực tiếp ảnh hưởng đến tỷ lệ đặt phòng tiếp theo (ước tính giảm 5% doanh số đặt phòng trực tuyến).

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                    │
│                                                             │
│ Bài toán (1 câu): Tài xế Xanh SM báo cáo sự cố hết pin thực │
│ địa cần hỗ trợ cứu hộ hoặc chỉ đường tới trạm sạc gần nhất. │
│ Công ty thành viên: [ ] VinFast  [X] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Tài xế phải chờ , điều phối viên phải xác định vị trí rồi điều hướng (mất thời gian) │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Tài xế gọi báo hết pin ──> 2. Điều phối viên xác định vị trí tìm trạm gần nhất ──> 3. Điều phối viên hướng dẫn tài xế ──> 4.Tài xế phải làm theo chỉ dẫn ___                   │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 và 3 (⏱ 15 phút/lượt)      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? 3 │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? Giảm thời gian xử lý của nhân viên điều phối từ 15 phút xuống dưới 2 phút để xác minh lại kết quả hướng dẫn của ai │
││
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [X] LLM  [] Agent │
└─────────────────────────────────────────────────────────────┘
```
```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                    │
│                                                             │
│ Bài toán (1 câu): Tự động phân loại và điều hướng phản ánh  │
│ khiếu nại của cư dân trên ứng dụng Vinhomes Resident. │
│ Công ty thành viên: [ ] VinFast  [] Xanh SM  [X] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Cư dân phải chờ phản hồi , Bên cskh phải hướng dẫn thủ công │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1.Cư dân gửi khiếu nại ──> 2.cskh review khiếu nại ──>3. cskh liên hệ với khách hàng làm rõ vấn đề ──>4.cskh tìm kiếm các bên liên quan ___                   │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 (⏱ 10 phút/lượt) và 4 (⏱ 15 phút/lượt)      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? 3 và 4 │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? Giảm thời gian xử lý của cskh từ 25 phút xuống dưới 5 phút để xác minh lại phản hồi người dùng. │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [X] LLM  [] Agent │
└─────────────────────────────────────────────────────────────┘
```
```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu):  Soạn thảo bản tóm tắt hồ sơ xuất viện từ  │
│ ghi chú lâm sàng thô của bác sĩ. │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [X] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Bác sĩ phải dành thời gian soạn tóm tắt hồ sơ thay vì dành thời gian khám bệnh nhân.  │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Bác sĩ ghi chú lâm sàng thô sau khi khám bệnh nhân ──> 2. Bác sĩ viết tóm tắt hồ sơ xuất viện ──> 3. Bác sĩ ký duyệt ---                          │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 (⏱ 15 phút/lượt)      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? 2 │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? Giảm thời gian xử lý của bác sĩ từ 15 phút xuống dưới 2 phút để xác minh lại kết quả tóm tắt hồ sơ của ai │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [X] LLM  [] Agent │
└─────────────────────────────────────────────────────────────┘
```
> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)
**Vẽ quy trình hiện tại lên bảng/giấy A3.** Sử dụng các ký hiệu:
* 🔴 **Bottleneck:** Bước gây tắc nghẽn, tốn thời gian, hoặc sai sót nhiều nhất.
* 🔄 **Handoff:** Điểm chuyển giao thông tin giữa người và hệ thống, hoặc giữa các bộ phận.
* Ghi rõ thời gian vận hành trung bình: **Tổng cộng = ____ phút/lượt**.

## 3.2. Problem Statement (6-field) & Metrics (15 min)
Điền đầy đủ 6 trường thông tin của bài toán:

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Ai đang thực hiện tác vụ hằng ngày? |
| **2. Current Workflow** | Mô tả tóm tắt quy trình thủ công hiện tại và công cụ sử dụng. |
| **3. Bottleneck** | Bước nào chậm, lỗi, hoặc cần xử lý ngôn ngữ tự động nhiều nhất? |
| **4. Business Impact** | Tổn thất thực tế đo bằng thời gian, chi phí, hoặc SLA của Vingroup. |
| **5. Success Metric** | AI giải quyết được thì đạt ngưỡng số mấy? (Ví dụ: *"85% vé được phân loại dưới 10s"*). |
| **6. Operational Boundary** | AI được phép làm gì, TUYỆT ĐỐI không được làm gì, điểm nào cần duyệt? |

## 3.3. Future-State Flow & AI Fit (25 min)
* **Xác định mức AI Fit (AI-Fit Matrix):** Giải pháp thuộc nhóm nào? [ ] Rule / State-Machine [ ] LLM Feature [ ] Agentic Loop.
* **Vẽ Future-State Flow:** Đánh dấu rõ:
  * 🔵 **AI Step:** Tác vụ LLM xử lý.
  * 🟢 **Human Step (HITL):** Bước con người phê duyệt/review (Human-in-the-loop).
  * ↩️ **Fallback:** Kế hoạch dự phòng khi LLM trả về kết quả lỗi hoặc không tự tin.

---

# 💻 Phase 4 — TECHNICAL PROMPT PROTOTYPE (Nhóm, 30 min)

Để đảm bảo kỹ sư của Vin Smart Future luôn giữ vững năng lực lập trình, nhóm của bạn sẽ tiến hành **lập trình bản mẫu prompt** trực tiếp trên **Gemini 2.5 Flash** bằng Python để stress-test hệ thống.

### Hướng dẫn thực hiện:
1. Mở file [starter-code/prompt_prototype.py](starter-code/prompt_prototype.py) bằng VS Code/Cursor.
2. Hoàn thiện các nội dung sau:
   * **System Prompt:** Viết chỉ thị cực kỳ nghiêm ngặt quy định vai trò, nhiệm vụ, định dạng output và **Operational Boundary (Ranh giới cấm)** của mô hình.
   * **Structured Output:** Định nghĩa định dạng JSON output rõ ràng.
   * **Adversarial Test Cases:** Viết ít nhất 3 prompts "tấn công" (Adversarial inputs) cố tình dụ AI vượt ranh giới hoặc đưa ra câu trả lời không được phép để kiểm tra xem ranh giới của bạn có thực sự vững chắc.
3. Chạy file python:
   ```bash
   python3 prompt_prototype.py
   ```
4. Kiểm tra xem các ranh giới an toàn có bị LLM phá vỡ hay không và ghi lại kết quả vào worksheet.

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [ ] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?
2. [ ] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?
3. [ ] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[ ] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> *Viết lý giải chi tiết tại đây*

---

# 📝 Phase 6 — REFLECTION (Cá nhân)
*Ghi nhận phản ánh của cá nhân bạn về việc phối hợp với AI trong buổi học hôm nay vào file `03-ai-log.md`.*
