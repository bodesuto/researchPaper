# Lịch Trình Chi Tiết 4 Năm Cho Nghiên Cứu Sinh CAMAS

## 1. Mục tiêu của file này

File này xây một lịch trình chi tiết 4 năm cho lộ trình nghiên cứu sinh xoay quanh CAMAS. Mục tiêu là giúp bạn biết:

- từng năm phải đạt mốc gì
- từng quý phải làm gì
- từng giai đoạn phải tạo ra đầu ra nào
- khi nào nên đọc, khi nào nên code, khi nào nên viết paper, khi nào nên tích hợp
- rủi ro nào cần tránh nếu muốn vừa làm luận án, vừa tối đa hóa cơ hội công bố

File này được viết theo logic:

- làm luận án tiến sĩ trước
- bài báo là các khối bằng chứng của luận án
- không dàn đều mọi thứ trong 4 năm
- ưu tiên kết quả sớm ở năm 1-2
- để năm 3-4 cho tích hợp, hoàn thiện, bảo vệ

## 2. Nguyên tắc dùng timeline này

### Nguyên tắc 1

Timeline này là `khung chuẩn để kiểm soát tiến độ`, không phải lịch cứng tuyệt đối theo ngày.

### Nguyên tắc 2

Mỗi giai đoạn chỉ được coi là hoàn thành khi có:

- đầu ra bằng file
- bảng kết quả
- draft
- hoặc bản thảo nộp thật

### Nguyên tắc 3

Nếu một giai đoạn kỹ thuật chưa đạt tiêu chí tối thiểu, không nên mở rộng sang giai đoạn sau chỉ để “giữ tiến độ bề mặt”.

### Nguyên tắc 4

Trong 4 năm, mục tiêu đúng không phải là “cùng lúc làm 4 paper”, mà là:

- năm 1 khóa bài toán và tạo nền
- năm 2 ra kết quả module mạnh nhất
- năm 3 mở rộng sang module khó và tích hợp
- năm 4 hoàn thiện bài tích hợp, luận án và bảo vệ

## 3. Bức tranh tổng quát 4 năm

### Năm 1

Mục tiêu:

- khóa proposal
- khóa hướng nghiên cứu
- xây nền literature, dữ liệu, baseline
- bắt đầu và cố gắng chốt Paper 1

### Năm 2

Mục tiêu:

- hoàn thiện và nộp Paper 1
- làm sâu Paper 2
- chuẩn bị hạ tầng cho Paper 3

### Năm 3

Mục tiêu:

- hoàn thiện Paper 2
- làm Paper 3 theo hướng thực dụng
- bắt đầu tích hợp Paper 4

### Năm 4

Mục tiêu:

- hoàn thiện Paper 4
- hoàn thiện luận án
- chỉnh sửa theo phản biện
- bảo vệ

## 4. Timeline chi tiết theo từng năm và từng quý

## Năm 1: Khóa nền và tạo kết quả đầu tiên

## Quý 1 của Năm 1

### Mục tiêu chính

- chốt đề tài
- chốt problem statement
- chốt roadmap 4 paper
- đọc sâu literature nền

### Việc phải làm

1. Đọc và chốt version chính của proposal.
2. Chốt 4 RQ và 4 hypothesis.
3. Chốt domain neo:
   - Paper 1: Maintenance
   - Paper 2: FJSP
   - Paper 3: Smart Grid
   - Paper 4: Integration
4. Tạo literature tracking file.
5. Tạo file so sánh 4 paper để tránh overlap novelty.
6. Tạo các file outline cho từng paper.
7. Làm rõ nỗi đau nghiên cứu và ứng dụng công nghiệp.

### Đầu ra bắt buộc

- proposal version ổn định
- literature tracking template
- publication mapping rõ
- 4 paper outlines ở mức đủ định hướng

### Rủi ro cần tránh

- đổi đề tài liên tục
- đọc quá nhiều nhưng chưa chốt problem và gap
- chưa tách rõ 4 paper mà đã nói tới 4 Q1

## Quý 2 của Năm 1

### Mục tiêu chính

- chuẩn bị hạ tầng nghiên cứu
- bắt đầu Paper 1 bằng dữ liệu và baseline

### Việc phải làm

1. Tạo cấu trúc thư mục nghiên cứu.
2. Tạo template lưu config, result, ablation, robustness.
3. Chốt schema dữ liệu cho Paper 1.
4. Thu thập dữ liệu maintenance, MAKG hoặc tri thức nền tương đương.
5. Làm sạch dữ liệu.
6. Chạy baseline đơn giản đầu tiên cho Paper 1.

### Đầu ra bắt buộc

- `schema_maintenance.md`
- `data_cleaning_report_paper1.md`
- baseline thô đầu tiên của Paper 1

### Rủi ro cần tránh

- nhảy vào mô hình mới khi dữ liệu còn chưa sạch
- chọn quá nhiều nguồn dữ liệu maintenance cùng lúc
- chưa có baseline mà đã thêm architecture mới

## Quý 3 của Năm 1

### Mục tiêu chính

- xây lõi phương pháp cho Paper 1

### Việc phải làm

1. Xây semantic memory.
2. Xây observability memory.
3. Xây temporal retrieval.
4. Xây conflict validation.
5. Định nghĩa grounded output.
6. Chạy main experiment của Paper 1.

### Đầu ra bắt buộc

- version đầu của mô hình Paper 1
- bảng kết quả main experiment

### Rủi ro cần tránh

- thêm quá nhiều thành phần ngoài lõi
- chưa định nghĩa hallucination rõ
- chưa xác định baseline mạnh nhất của Paper 1

## Quý 4 của Năm 1

### Mục tiêu chính

- hoàn thiện Paper 1 ở mức draft mạnh
- chuẩn bị nền cho Paper 2

### Việc phải làm

1. Chạy ablation Paper 1.
2. Chạy stress test Paper 1.
3. Viết draft Paper 1.
4. Xin phản hồi từ thầy/nhóm.
5. Chọn benchmark và protocol ban đầu cho Paper 2.

### Đầu ra bắt buộc

- draft Paper 1
- benchmark protocol draft của Paper 2

### Mốc quyết định

Cuối năm 1, bạn phải trả lời được:

- Paper 1 có đủ mạnh để nộp không?
- novelty của Paper 1 đã thật sự sắc chưa?

## Năm 2: Ra bài mạnh và mở rộng sang coordination

## Quý 1 của Năm 2

### Mục tiêu chính

- chỉnh và nộp Paper 1
- bắt đầu chính thức Paper 2

### Việc phải làm

1. Sửa Paper 1 theo góp ý.
2. Chốt venue phù hợp cho Paper 1.
3. Nộp Paper 1.
4. Chốt benchmark FJSP cho Paper 2.
5. Chạy heuristic baselines cho Paper 2.
6. Chạy RL/MARL baseline cơ bản cho Paper 2.

### Đầu ra bắt buộc

- bản nộp Paper 1
- baseline table đầu tiên của Paper 2

### Rủi ro cần tránh

- dừng hẳn Paper 1 sau khi nộp mà không giữ log chỉnh sửa
- bắt đầu Paper 2 quá tham với đủ mọi thành phần

## Quý 2 của Năm 2

### Mục tiêu chính

- xây core model của Paper 2

### Việc phải làm

1. Xây heterogeneous graph state modeling.
2. Xây master policy.
3. Xây worker policies.
4. Chạy version hierarchy + graph đầu tiên.
5. So sánh với flat MARL.

### Đầu ra bắt buộc

- core model Paper 2
- bảng so sánh flat vs hierarchy

### Rủi ro cần tránh

- thêm LRMP quá sớm
- thêm MD-MDP quá nặng trước khi có lõi hierarchy chạy ổn

## Quý 3 của Năm 2

### Mục tiêu chính

- làm sâu Paper 2
- chứng minh hierarchy là nguồn tạo gain

### Việc phải làm

1. Thêm context adaptation/LRMP nếu thực sự cần.
2. Chạy ablation:
   - no hierarchy
   - no graph
   - no context adaptation
3. Chạy perturbation robustness tests.
4. Phân tích hành vi tầng chiến lược.

### Đầu ra bắt buộc

- ablation table
- robustness table
- behavioral analysis của master policy

### Rủi ro cần tránh

- chỉ báo score mà không giải thích hierarchy học cái gì
- giữ LRMP dù không tạo chênh lệch

## Quý 4 của Năm 2

### Mục tiêu chính

- viết draft mạnh cho Paper 2
- chuẩn bị nền kỹ thuật cho Paper 3

### Việc phải làm

1. Viết draft Paper 2.
2. Xin phản hồi từ thầy/nhóm.
3. Chọn environment cho Paper 3:
   - IEEE 30
   - IEEE 118
4. Thiết kế safety metric và preference protocol sơ bộ.

### Đầu ra bắt buộc

- draft Paper 2
- `preference_label_protocol_paper3.md` draft
- `safety_label_protocol_paper3.md` draft

### Mốc quyết định

Cuối năm 2, bạn phải có:

- ít nhất 1 paper đã nộp
- 1 paper thứ hai ở mức draft mạnh
- nền Paper 3 đã rõ strategy

## Năm 3: Mở sang alignment và bắt đầu tích hợp

## Quý 1 của Năm 3

### Mục tiêu chính

- hoàn thiện và nộp Paper 2
- dựng baseline cho Paper 3

### Việc phải làm

1. Sửa Paper 2 theo góp ý.
2. Nộp Paper 2.
3. Chạy constrained RL baseline cho Paper 3.
4. Chạy safe RL baseline nếu cần.
5. Chốt hard constraints và utility objectives.

### Đầu ra bắt buộc

- bản nộp Paper 2
- baseline result đầu tiên của Paper 3

### Rủi ro cần tránh

- framing Paper 3 vẫn quá nặng RLHF
- chưa có constrained RL baseline mà đã build reward model hai đầu

## Quý 2 của Năm 3

### Mục tiêu chính

- xây lõi kỹ thuật cho Paper 3

### Việc phải làm

1. Xây simulated expert preference generator.
2. Xây utility head.
3. Xây safety head.
4. Xây dual-head reward model.
5. Tích hợp Lagrangian constrained update.

### Đầu ra bắt buộc

- version đầu của dual-head reward model
- utility/safety learning curves ban đầu

### Rủi ro cần tránh

- để reward model collapse thành scalar penalty phức tạp
- không kiểm tra simulated preference có hợp lý không

## Quý 3 của Năm 3

### Mục tiêu chính

- hoàn thiện thực nghiệm Paper 3
- chuẩn bị interface cho Paper 4

### Việc phải làm

1. Chạy main experiment Paper 3.
2. Chạy utility-safety frontier.
3. Chạy ablation no safety head/no utility head/no Lagrangian.
4. Chạy disturbance robustness.
5. Viết interface spec cho CAMAS.

### Đầu ra bắt buộc

- frontier của Paper 3
- ablation table của Paper 3
- `camas_interface_spec_vi.md`

### Rủi ro cần tránh

- chỉ report một điểm profit/safety mà không có frontier
- interface Paper 4 vẫn mơ hồ dù đã làm xong 3 module

## Quý 4 của Năm 3

### Mục tiêu chính

- bắt đầu Paper 4
- viết draft ban đầu cho Paper 3

### Việc phải làm

1. Viết draft Paper 3.
2. Xây open-loop baselines cho Paper 4.
3. Xây pairwise integration baselines.
4. Xây full pipeline no-feedback.

### Đầu ra bắt buộc

- draft Paper 3
- baseline architecture results cho Paper 4

### Mốc quyết định

Cuối năm 3, bạn phải có:

- Paper 1 đã nộp hoặc đang phản biện
- Paper 2 đã nộp hoặc ở mức rất gần nộp
- Paper 3 có draft
- Paper 4 đã có integration baseline

## Năm 4: Tích hợp, hoàn thiện luận án, bảo vệ

## Quý 1 của Năm 4

### Mục tiêu chính

- hoàn thiện closed-loop method cho Paper 4

### Việc phải làm

1. Thêm mandatory feedback protocol.
2. Thêm event-triggered re-grounding.
3. Chạy full closed-loop experiments.
4. So sánh full no-feedback vs full feedback.

### Đầu ra bắt buộc

- closed-loop gain table
- full feedback ablation results

### Rủi ro cần tránh

- closed-loop chỉ là sơ đồ mà không có gain đo được
- không có baseline full no-feedback

## Quý 2 của Năm 4

### Mục tiêu chính

- hoàn thiện Paper 4
- chỉnh Paper 3 nếu còn thiếu

### Việc phải làm

1. Chạy overhead analysis cho Paper 4.
2. Viết draft Paper 4.
3. Chỉnh lại Paper 3 theo phản hồi nội bộ.
4. Chốt notation thống nhất cho toàn luận án.

### Đầu ra bắt buộc

- draft Paper 4
- bản Paper 3 đủ để nộp nếu chưa nộp

### Rủi ro cần tránh

- Paper 4 overclaim quá rộng
- chưa tách rõ novelty kiến trúc với novelty module

## Quý 3 của Năm 4

### Mục tiêu chính

- viết bản thảo luận án đầy đủ

### Việc phải làm

1. Ghép 4 paper vào cấu trúc luận án.
2. Viết chương mở đầu, tổng quan và thảo luận tổng hợp.
3. Thống nhất notation, metric, hình, bảng.
4. Viết rõ hạn chế nghiên cứu và hướng tương lai.

### Đầu ra bắt buộc

- bản thảo luận án hoàn chỉnh đầu tiên

### Rủi ro cần tránh

- ghép 4 paper cơ học mà không có luận điểm thống nhất
- lặp lại novelty giữa các chương

## Quý 4 của Năm 4

### Mục tiêu chính

- chỉnh sửa luận án
- chuẩn bị bảo vệ

### Việc phải làm

1. Sửa luận án theo góp ý thầy.
2. Chuẩn bị slide bảo vệ.
3. Chuẩn bị câu trả lời phản biện học thuật.
4. Chuẩn bị hồ sơ nộp.

### Đầu ra bắt buộc

- luận án bản cuối
- slide bảo vệ
- bộ câu hỏi phản biện và câu trả lời

### Mốc cuối

Kết thúc năm 4, bạn cần đạt:

- luận án hoàn chỉnh
- tối thiểu 2-4 bài ở các mức nộp/phản biện/chấp nhận tùy tiến độ thực tế
- một câu chuyện nghiên cứu thống nhất và bảo vệ được

## 5. Bảng tổng hợp mốc 4 năm

| Năm | Trọng tâm | Đầu ra chính |
|---|---|---|
| Năm 1 | Chốt nền và làm Paper 1 | Proposal ổn định, baseline + draft Paper 1 |
| Năm 2 | Hoàn thiện Paper 1, làm sâu Paper 2 | Nộp Paper 1, draft mạnh Paper 2 |
| Năm 3 | Hoàn thiện Paper 2, làm Paper 3, bắt đầu Paper 4 | Nộp Paper 2, draft Paper 3, baseline integration |
| Năm 4 | Hoàn thiện Paper 4 và luận án | Draft/nộp Paper 4, luận án hoàn chỉnh, bảo vệ |

## 6. Những việc phải làm lặp đi lặp lại trong suốt 4 năm

Không phải mọi thứ chỉ diễn ra theo quý. Có một số việc bạn phải làm liên tục:

### Hàng tuần

- cập nhật literature tracking
- lưu config và kết quả thí nghiệm
- ghi research note
- cập nhật backlog câu hỏi mở

### Hàng tháng

- review tiến độ với thầy hoặc tự review
- so sánh tiến độ thật với timeline
- cắt bớt scope nếu thấy bị quá tải

### Sau mỗi đợt thực nghiệm lớn

- lưu baseline table
- lưu ablation table
- lưu robustness table
- viết error analysis

### Sau mỗi draft paper

- viết lại novelty statement
- kiểm tra overlap với các paper khác
- kiểm tra reviewer risks

## 7. Dấu hiệu bạn đang đi đúng tiến độ

- cuối năm 1 đã có draft Paper 1
- cuối năm 2 đã có ít nhất 1 bài nộp và 1 bài draft mạnh
- cuối năm 3 đã có 3 module rõ và bắt đầu integration thật
- đầu năm 4 đã có closed-loop result
- giữa năm 4 đã có bản luận án đầu tiên

## 8. Dấu hiệu bạn đang đi lệch

- hết năm 1 vẫn chưa khóa được dữ liệu và baseline cho Paper 1
- năm 2 vẫn còn đổi novelty của các paper liên tục
- Paper 2 và Paper 3 đều chưa có baseline mạnh nhưng đã quá nhiều module mới
- đến năm 4 mới bắt đầu nghĩ về integration
- luận án bị viết như 4 paper ghép cơ học

## 9. Kết luận cuối

Lịch trình 4 năm khả thi nhất cho CAMAS là:

- năm 1: khóa và dựng nền
- năm 2: tạo kết quả module mạnh đầu tiên
- năm 3: mở sang bài khó và tích hợp
- năm 4: chốt kiến trúc, hoàn thiện luận án và bảo vệ

Nếu bám đúng timeline này, bạn sẽ tránh được hai lỗi rất hay gặp ở nghiên cứu sinh:

- dàn đều quá nhiều ý tưởng ngay từ đầu
- để đến cuối mới nghĩ cách ghép chúng thành một luận án thống nhất

Timeline này giúp bạn đi theo hướng ngược lại:

- khóa luận điểm trước
- chứng minh từng module sau
- tích hợp có kiểm soát
- bảo vệ bằng một câu chuyện nghiên cứu rõ ràng
