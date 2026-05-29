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

# =========================================================================
# 👤 PHẦN CÁ NHÂN 1: LÊ THIÊN KHANG - MSSV: 2A202600726
# =========================================================================

## 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

### 📝 List bài toán của tôi (Lê Thiên Khang):
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 |VinFast |Lặp lại & Tốn thời gian|Đối chiếu hóa đơn sạc điện từ các trạm sạc đối tác liên kết ngoài (đơn vị thứ ba) với dữ liệu thực thu trên hệ thống VinFast. Nhân viên kế toán phải tải file Excel đối soát hàng tuần từ các đối tác trạm sạc, dùng hàm VLOOKUP hoặc so khớp thủ công từng mã giao dịch, thời lượng sạc, dòng điện tiêu thụ và đơn giá để phát hiện chênh lệch lệch dòng tiền.Mất 12 - 16 giờ làm việc/tuần của một kế toán viên chuyên trách. Tỷ lệ sai sót đối chiếu thủ công khoảng 1.5%, gây thất thoát trung bình 80,000,000 VND/tháng do bỏ sót các giao dịch lỗi hoặc thanh toán trùng lặp cho đối tác.|
| 2 |Xanh SM | Tốn thời gian & Pain từ người khác |Tiếp nhận và xử lý thủ công các báo cáo khẩn cấp từ tài xế về sự cố pin yếu thực địa trên đường đón chở khách.Tài xế gọi điện lên tổng đài báo pin dưới 5%. Điều phối viên (Dispatcher) phải mở bản đồ nội bộ định vị vị trí xe, tìm trạm sạc VinFast còn trụ trống phù hợp gần nhất, soạn tin nhắn chỉ đường gửi lại tài xế, hoặc điều xe cứu hộ pin nếu xe cạn kiệt pin hoàn toàn.Mất 15 phút/lượt xử lý, trong giờ cao điểm tài xế phải xếp hàng chờ đợi cuộc gọi gây ức chế cực lớn. Ước tính gây rò rỉ doanh thu ~15% trong khung giờ cao điểm do xe nằm im không đón được khách, cộng thêm chi phí cứu hộ phát sinh 500,000 VND/lượt nếu không điều hướng kịp thời đến trạm sạc gần nhất trước khi sập nguồn.|
| 3 |Vinhomes |Lặp lại |Đọc, phân loại và chuyển tiếp thủ công các phản ánh, khiếu nại của cư dân (ví dụ: hỏng đèn hành lang, mất nước, tiếng ồn, đăng ký thẻ xe) gửi qua ứng dụng Vinhomes Resident.Thời gian phản hồi ban đầu bị kéo dài từ 4 - 12 tiếng gây phàn nàn lớn từ cư dân (SLA đạt dưới 75% vào giờ cao điểm). Tốn trung bình 1.5 nhân sự Full-time chỉ để ngồi phân loại và gõ tay chuyển tiếp yêu cầu tại mỗi khu đại đô thị lớn.|
| 4 |Vinmec |Tốn thời gian |Bác sĩ soạn thảo bản tóm tắt từ ghi chú lâm sàng thô, kết quả xét nghiệm và đơn thuốc trên hệ thống bệnh án điện tử. Bác sĩ phải ngồi đọc lại toàn bộ tiến trình điều trị phức tạp của bệnh nhân, lọc các chỉ số quan trọng và viết lại bằng ngôn ngữ phổ thông, dễ hiểu để bệnh nhân và người nhà biết cách tự chăm sóc tại nhà.Bác sĩ mất từ 20 - 30 phút/bệnh nhân chỉ để làm công tác giấy tờ này, làm giảm thời gian khám chữa bệnh trực tiếp cho các bệnh nhân khác. Làm tăng thời gian chờ đợi làm thủ tục ra viện của khách hàng lên trên 1.5 tiếng, gây ảnh hưởng nghiêm trọng tới chỉ số hài lòng của bệnh nhân|
| 5 |Vinpearl |Pain từ người khác & AI có thể tốt hơn |Rà soát và phân tích các đánh giá (Reviews) của khách hàng trên các nền tảng OTA (Booking.com, Agoda, TripAdvisor, Google Maps) để tổng hợp khiếu nại khẩn cấp gửi quản lý khách sạn. Nhân viên truyền thông CSKH phải truy cập từng trang web hàng ngày, đọc hàng trăm đánh giá của khách bằng nhiều ngôn ngữ khác nhau, dịch sang tiếng Việt và copy các phàn nàn nghiêm trọng (như phòng bẩn, thái độ nhân viên kém) vào file báo cáo cuối ngày.Mất 3 - 4 tiếng/ngày của nhân viên để tổng hợp báo cáo thủ công. Độ trễ xử lý các phàn nàn khẩn cấp lên tới 24 - 48 giờ, khiến khách hàng đã rời đi trước khi khách sạn kịp xin lỗi hoặc khắc phục, làm giảm điểm đánh giá trung bình từ 4.5 xuống dưới 4.0, trực tiếp ảnh hưởng đến tỷ lệ đặt phòng tiếp theo (ước tính giảm 5% doanh số đặt phòng trực tuyến).|

---

## 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

### QUICK PROBLEM CARD #1 - Lê Thiên Khang
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

### QUICK PROBLEM CARD #2 - Lê Thiên Khang
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

### QUICK PROBLEM CARD #3 - Lê Thiên Khang
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

---

# =========================================================================
# 👤 PHẦN CÁ NHÂN 2: NGUYỄN THỤY NHƯ QUỲNH - MSSV: 2A202600557
# =========================================================================

## 🏛️ Bối cảnh: Tôi là ai?
Tôi là Quỳnh, AI Engineer tại Vin Smart Future. Nhóm chúng tôi được giao nhiệm vụ phối hợp với Khối Vận Hành của Vinhomes Grand Park để tìm kiếm các cơ hội tối ưu hóa bằng trí tuệ nhân tạo trong quá trình quản lý cư dân và vận hành đô thị thông minh.

Thông qua quá trình khảo sát thực tế và nghiên cứu quy trình xử lý hồ sơ cư dân tại Vinhomes Grand Park — một đại đô thị với hàng chục nghìn cư dân — tôi nhận thấy Ban Quản Lý đang phải xử lý khối lượng lớn các thủ tục hành chính như đăng ký thi công nội thất, cấp thẻ xe, booking thang máy chuyển đồ và đăng ký khách ra vào mỗi ngày.

Tuy nhiên, phần lớn quy trình hiện tại vẫn mang tính thủ công: cư dân tải biểu mẫu, điền giấy tờ, gửi file qua app/email, sau đó nhân viên Ban Quản Lý phải tự kiểm tra từng hồ sơ để phát hiện giấy tờ thiếu, sai biểu mẫu hoặc ảnh không hợp lệ. Điều này dẫn đến việc hồ sơ bị trả lại nhiều lần, thời gian xử lý kéo dài và cư dân phải liên tục bổ sung giấy tờ.

Trong quá trình quan sát workflow thực tế, tôi nhận ra vấn đề lớn nhất không nằm ở việc thiếu ứng dụng quản lý, mà nằm ở “administrative friction” — ma sát hành chính giữa cư dân và hệ thống vận hành. Đây chính là bài toán mà nhóm tôi mang vào buổi Lab hôm nay: xây dựng một hệ thống AI Copilot hỗ trợ pre-check hồ sơ và giảm tải quy trình xử lý thủ tục cư dân cho Vinhomes Grand Park.

---

## 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội (Cá nhân)

### 📝 List bài toán của tôi (Nguyễn Thụy Như Quỳnh):
| # | Lăng kính | Problem quan sát được | Ai đang đau? | Dấu hiệu thật |
|---|---|---|---|---|
| 1 | Tốn thời gian | Cư dân thường điền sai hoặc thiếu thông tin trong hồ sơ đăng ký thi công nội thất | Ban Quản Lý (BQL), cư dân | Hồ sơ bị trả đi trả lại nhiều lần, mất thời gian xử lý |
| 2 | Lặp lại | Nhân viên CSKH phải liên tục trả lời các câu hỏi giống nhau về giấy tờ và thủ tục cư dân | Nhân viên CSKH | Tốn nhiều thời gian support các câu hỏi lặp lại mỗi ngày |
| 3 | AI-upgrade | Quy trình đăng ký vé xe tháng và booking elevator vẫn làm thủ công qua giấy tờ/chat | Cư dân, BQL | Quy trình chậm, dễ sai sót và khó tracking trạng thái |
| 4 | Pain từ stakeholder | Cư dân phải xuống BQL nhiều lần chỉ để bổ sung giấy tờ còn thiếu | Cư dân | Nhiều complain về trải nghiệm thủ tục bất tiện |
| 5 | Tốn thời gian | Nhân viên BQL phải tự kiểm tra từng file PDF/hình ảnh cư dân gửi lên | Nhân viên BQL | Mất nhiều manpower để rà soát hồ sơ thủ công |

---

## 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards (Cá nhân)

### QUICK PROBLEM CARD #1 - Nguyễn Thụy Như Quỳnh
```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Cư dân Vinhomes thường nộp sai hoặc thiếu hồ sơ   │
│ đăng ký thi công nội thất, khiến Ban Quản Lý phải kiểm tra  │
│ và yêu cầu bổ sung thủ công nhiều lần.                      │
│                                                             │
│ Công ty thành viên: Vinhomes                                │
│                                                             │
│ Ai đang đau?                                                │
│ * Cư dân                                                    │
│ * CSKH cư dân                                               │
│ * Ban quản lý tòa nhà                                       │
│                                                             │
│ Workflow thủ công hiện tại:                                 │
│ 1. Cư dân tải form PDF ──> 2. Điền thủ công và gửi giấy tờ  │
│ qua app/email ──> 3. BQL kiểm tra từng file ──>             │
│ 4. Nếu thiếu → yêu cầu bổ sung ──> 5. Cư dân gửi lại hồ sơ  │
│                                                             │
│ Bước tốn thời gian/lỗi nhất? Bước 3-4 (10-15 phút/hồ sơ)    │
│ AI có thể hỗ trợ:                                           │
│ * Kiểm tra thiếu giấy tờ                                    │
│ * OCR đọc hồ sơ                                             │
│ * Draft checklist bổ sung                                   │
│ * Tóm tắt hồ sơ cho BQL                                     │
│                                                             │
│ Metric thành công:                                          │
│ * Giảm tỉ lệ hồ sơ bị trả từ 45% → dưới 15%                 │
│ * Giảm thời gian review từ 15 phút → dưới 3 phút            │
│                                                             │
│ Quick Architecture: [X] Rule + LLM Feature                  │
└─────────────────────────────────────────────────────────────┘
```

### QUICK PROBLEM CARD #2 - Nguyễn Thụy Như Quỳnh
```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Cư dân mới chuyển vào Vinhomes thường gặp khó     │
│ khăn khi hoàn tất các thủ tục move-in như đăng ký cư dân,  │
│ khai báo xe, booking thang máy chuyển đồ và kích hoạt dịch   │
│ vụ nội khu.                                                 │
│                                                             │
│ Công ty thành viên: Vinhomes                                │
│                                                             │
│ Ai đang đau?                                                │
│ * Cư dân mới                                                │
│ * CSKH cư dân                                               │
│ * Ban quản lý tòa nhà                                       │
│                                                             │
│ Workflow hiện tại:                                          │
│ 1. Cư dân nhận căn hộ ──> 2. Tự tìm hiểu thủ tục qua email/ │
│ app ──> 3. Điền nhiều form khác nhau ──> 4. Gửi hồ sơ cho    │
│ BQL ──> 5. BQL kiểm tra và phản hồi thủ công ──>             │
│ 6. Cư dân bổ sung nếu thiếu                                 │
│                                                             │
│ Bottleneck: Cư dân không hiểu quy trình, Thiếu giấy tờ,     │
│ Booking sai thời gian, CSKH trả lời lặp đi lặp lại          │
│                                                             │
│ Bước tốn thời gian/lỗi nhất? Bước 3-5 (⏱ 20-30 phút/cư dân)  │
│ AI có thể hỗ trợ:                                           │
│ * Personalized onboarding flow                              │
│ * Checklist động theo từng loại căn hộ                      │
│ * OCR đọc giấy tờ                                             │
│ * Draft form tự động                                        │
│ * Gợi ý lịch move-in phù hợp                                 │
│                                                             │
│ Metric thành công:                                          │
│ * Giảm 60% ticket hỗ trợ move-in                            │
│ * Giảm thời gian onboarding từ 2 ngày → vài giờ             │
│                                                             │
│ Quick Architecture: [X] Rule + LLM Feature                  │
└─────────────────────────────────────────────────────────────┘
```

### QUICK PROBLEM CARD #3 - Nguyễn Thụy Như Quỳnh
```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Ban quản lý Vinhomes nhận rất nhiều phản ánh về   │
│ sự cố nội khu (thang máy, nước, điện, tiếng ồn, đỗ xe),     │
│ nhưng việc tổng hợp và ưu tiên xử lý vẫn làm thủ công qua    │
│ hotline và group chat.                                      │
│                                                             │
│ Công ty thành viên: Vinhomes                                │
│                                                             │
│ Ai đang đau?                                                │
│ * Ban quản lý                                               │
│ * Kỹ thuật vận hành                                         │
│ * CSKH cư dân                                               │
│                                                             │
│ Workflow hiện tại:                                          │
│ 1. Cư dân gọi hotline/gửi app ──> 2. CSKH ghi nhận thủ công │
│ ──> 3. Chuyển ticket qua Zalo/group nội bộ ──> 4. Kỹ thuật  │
│ xác minh ──> 5. BQL ưu tiên xử lý theo kinh nghiệm cá nhân  │
│                                                             │
│ Bottleneck: Ticket bị trùng, Thiếu context, Không xác định  │
│ được severity, Escalation chậm                              │
│                                                             │
│ Bước tốn thời gian/lỗi nhất? Bước 2-4 (⏱ 10-15 phút/ticket)  │
│ AI có thể hỗ trợ:                                           │
│ * Gom nhóm ticket trùng lặp                                 │
│ * Tóm tắt sự cố                                             │
│ * Severity scoring                                          │
│ * Gợi ý đội xử lý phù hợp                                   │
│ * Predict escalation risk                                   │
│                                                             │
│ Metric thành công:                                          │
│ * Giảm 40% thời gian điều phối                              │
│ * Detect critical incident dưới 1 phút                      │
│                                                             │
│ Quick Architecture: [X] LLM Feature                         │
└─────────────────────────────────────────────────────────────┘
```

---

## 🗳️ Quyết định lựa chọn của nhóm (Phản ánh cá nhân Quỳnh):

Nhóm quyết định chọn bài toán **"Card #1 — Vinhomes PermitFlow AI: AI hỗ trợ xử lý hồ sơ thi công & thủ tục cư dân"** để thực hiện Deep-Dive.

### Lý do lựa chọn và loại bỏ các thẻ khác:
* **Card #2 (Resident Move-in Copilot):** Mặc dù pain point onboarding cư dân mới là có thật, nhưng workflow hiện tại vẫn phụ thuộc mạnh vào chính sách riêng của từng tòa nhà và từng loại căn hộ. Dữ liệu quy trình chưa đủ chuẩn hóa giữa các khu đô thị Vinhomes, khiến việc xây dựng AI flow tổng quát khó đạt độ chính xác cao trong giai đoạn prototype đầu tiên.
* **Card #3 (Facility Incident Summarizer):** Đây là bài toán vận hành hấp dẫn nhưng mức độ rủi ro escalation cao. Nếu AI phân loại sai severity của sự cố (ví dụ: mất điện diện rộng hoặc sự cố thang máy), hệ thống có thể ảnh hưởng trực tiếp đến SLA vận hành và trải nghiệm cư dân. Ngoài ra, nhiều phần của workflow hiện tại có thể xử lý tốt bằng rule-based ticket routing trước khi cần tới LLM reasoning phức tạp.

### Vì sao nhóm chọn Card #1:
Bài toán hồ sơ thi công nội thất và thủ tục cư dân có:
* Workflow rõ ràng, ổn định và lặp lại mỗi ngày
* Pain point thực tế cho cả cư dân và Ban Quản Lý
* Dữ liệu đầu vào có cấu trúc tương đối tốt (PDF, CCCD, checklist giấy tờ)
* Rủi ro vận hành thấp hơn so với incident management real-time
* Phù hợp triển khai theo mô hình “Rule + LLM + Human-in-the-loop”

Quan trọng nhất: AI không thay thế Ban Quản Lý Vinhomes, mà đóng vai trò “copilot” giúp pre-check hồ sơ, phát hiện thiếu giấy tờ, draft phản hồi bổ sung, giảm ma sát hành chính cho cư dân. Đây là bài toán có khả năng prototype nhanh, đo được hiệu quả rõ ràng và phù hợp với scope kỹ thuật của Vin Smart Future trong giai đoạn đầu.
