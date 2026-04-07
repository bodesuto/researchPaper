# Kế Hoạch Cường Độ Tối Đa 2 Năm Cho 4 Paper Q1 Của CAMAS

## 1. Mục tiêu của file này

File này được viết theo đúng yêu cầu mới:

- hoàn thành trong `2 năm`
- `không giảm paper nào`
- cả `4 paper` đều phải đi theo profile `Q1`
- bạn chấp nhận dồn toàn bộ tâm trí và cường độ làm việc vào lộ trình này

Tôi phải nói thẳng ngay từ đầu:

- đây là lộ trình `rất căng`
- vẫn có thể thiết kế được
- nhưng chỉ khả thi nếu bạn làm theo chế độ `high-discipline, high-output, parallelized PhD execution`

Điều đó có nghĩa là:

- không được làm việc theo cảm hứng
- không được đọc lan man quá lâu
- không được để một paper kéo chậm cả pipeline
- phải có review tiến độ theo tháng
- phải chấp nhận chuẩn hóa công việc như một dự án R&D cường độ cao

## 2. Điều kiện tiên quyết để 2 năm và 4 Q1 là khả thi

Muốn giữ cả 4 paper và cùng nhắm Q1 trong 2 năm, bạn phải chấp nhận 6 điều kiện sau:

### Điều kiện 1

Paper 1 phải trở thành `paper mở đường cực mạnh`, gần như không được phép thất bại.

### Điều kiện 2

Paper 2 phải dùng chiến lược “reuse backbone, innovate at the right layer”, không được tự xây mọi thứ từ số 0.

### Điều kiện 3

Paper 3 phải được thiết kế cực thực dụng ngay từ đầu, nhưng vẫn phải đủ sắc để đứng profile Q1.

### Điều kiện 4

Paper 4 phải bắt đầu sớm hơn bình thường, không được để đến cuối mới tích hợp.

### Điều kiện 5

Bạn phải làm `song song có kiểm soát`, chứ không tuần tự hoàn toàn.

### Điều kiện 6

Mỗi tháng phải có deliverable thật:

- file
- bảng kết quả
- draft
- hoặc submission package

Nếu không giữ được 6 điều kiện này, kế hoạch 2 năm 4 Q1 sẽ vỡ.

## 3. Chiến lược tổng quát cho 24 tháng

Chiến lược đúng trong 2 năm không phải:

- làm xong Paper 1 rồi mới nghĩ tới Paper 2

Mà là:

- `Paper 1` là trục chính
- `Paper 2` được dựng nền song song từ rất sớm
- `Paper 3` chuẩn bị data/protocol song song nhưng code sâu sau
- `Paper 4` chuẩn hóa interface từ giữa năm 1, không đợi đến năm 2 mới nghĩ

Nói cách khác, bạn phải chạy 3 lớp công việc đồng thời:

1. `Main line`: Paper 1 -> Paper 2 -> Paper 4
2. `Shadow line`: chuẩn bị data/protocol cho Paper 3 từ sớm
3. `Thesis line`: duy trì proposal, notation, publication mapping, evidence log liên tục

## 4. Kiến trúc quản lý công việc bắt buộc

Bạn phải chia công việc thành 5 track cố định:

### Track A: Proposal và luận điểm luận án

- giữ proposal ổn định
- chốt novelty
- chống overlap giữa 4 paper

### Track B: Data và benchmark

- maintenance data
- FJSP benchmark
- smart grid environment

### Track C: Method implementation

- Paper 1 method
- Paper 2 method
- Paper 3 method
- Paper 4 protocol

### Track D: Evaluation

- baseline
- ablation
- robustness
- reviewer defense figures

### Track E: Writing

- abstract
- intro
- method
- experiments
- rebuttal-ready notes

Nếu bạn không tổ chức theo 5 track này, khối lượng 2 năm sẽ bị rối.

## 5. Timeline 24 tháng chi tiết

## Giai đoạn 1: Tháng 1-3

### Mục tiêu

- khóa tất cả các quyết định chiến lược
- dựng toàn bộ hạ tầng nghiên cứu
- bắt đầu Paper 1 ngay
- chuẩn bị benchmark cho Paper 2 và Paper 3 ngay từ đầu

### Việc phải làm trong 3 tháng đầu

#### 1. Khóa hoàn toàn proposal

- chốt `proposal_rewritten_vi.md`
- chốt 4 RQ
- chốt 4 novelty statements
- chốt 4 domain neo
- chốt thứ tự:
  - Paper 1
  - Paper 2
  - Paper 4
  - Paper 3

#### 2. Dựng toàn bộ hệ thống quản lý nghiên cứu

- literature tracking
- experiment tracking
- benchmark registry
- baseline registry
- draft registry

#### 3. Khởi động Paper 1 ở mức dữ liệu thật

- schema maintenance
- cleaning rules
- semantic memory schema
- observability memory schema
- entity mapping rules

#### 4. Khởi động Paper 2 ở mức benchmark

- chọn benchmark FJSP
- chốt state/action/reward preliminarily
- chạy 1 heuristic baseline đầu tiên

#### 5. Khởi động Paper 3 ở mức environment

- chọn IEEE 30/118
- chốt hard constraints
- chốt utility objective

### Đầu ra bắt buộc cuối tháng 3

- proposal chính thức
- 4 paper statements đã khóa
- maintenance schema
- FJSP benchmark protocol draft
- smart grid environment protocol draft

### KPI cuối tháng 3

- không còn đổi cấu trúc 4 paper
- đã có baseline đầu tiên cho Paper 2
- đã có raw pipeline cho Paper 1

## Giai đoạn 2: Tháng 4-6

### Mục tiêu

- biến Paper 1 thành paper có method chạy được
- dựng baseline đủ mạnh cho Paper 2
- chuẩn bị preference protocol cho Paper 3

### Việc phải làm

#### Paper 1

- semantic-only baseline
- retrieval-only baseline
- KG-RAG baseline
- build semantic memory
- build observability memory
- build temporal retrieval
- build conflict validation
- main experiment vòng 1

#### Paper 2

- heuristic baselines
- flat RL/MARL baseline
- graph-based baseline
- xác nhận benchmark khó đủ để publish

#### Paper 3

- thiết kế simulated expert preference protocol
- safety label protocol
- build constrained RL baseline environment

### Đầu ra bắt buộc cuối tháng 6

- Paper 1 có main results vòng 1
- Paper 2 có baseline table đầu tiên
- Paper 3 có label protocol

### KPI cuối tháng 6

- Paper 1 phải chứng minh được tín hiệu rằng conflict validation có ích
- Paper 2 phải biết baseline mạnh nhất là gì
- Paper 3 không còn mơ hồ về preference strategy

## Giai đoạn 3: Tháng 7-9

### Mục tiêu

- hoàn thiện Paper 1 ở mức submission-ready
- dựng core model của Paper 2
- chuẩn hóa interface sơ bộ cho Paper 4

### Việc phải làm

#### Paper 1

- ablation đầy đủ
- stress test:
  - missing logs
  - stale evidence
  - conflict evidence
  - noisy data
- error analysis
- viết draft full
- review nội bộ

#### Paper 2

- build heterogeneous graph state
- build hierarchy:
  - master policy
  - worker policies
- run flat vs hierarchy comparison

#### Paper 4

- định nghĩa interface:
  - perception output
  - coordination output
  - alignment output

### Đầu ra bắt buộc cuối tháng 9

- draft hoàn chỉnh Paper 1
- core model Paper 2 chạy được
- interface spec v1 cho Paper 4

### KPI cuối tháng 9

- Paper 1 phải ở mức nộp được trong 2-4 tuần
- Paper 2 phải có evidence đầu tiên rằng hierarchy có ích

## Giai đoạn 4: Tháng 10-12

### Mục tiêu

- nộp Paper 1
- tăng tốc Paper 2
- dựng baseline kiến trúc cho Paper 4

### Việc phải làm

#### Paper 1

- sửa cuối
- nộp bài

#### Paper 2

- run perturbation scenarios
- ablation:
  - no hierarchy
  - no graph
  - no context adaptation
- chỉ thêm LRMP nếu thực sự tạo gain

#### Paper 4

- build:
  - perception + coordination
  - coordination + alignment
  - full no-feedback pipeline skeleton

### Đầu ra bắt buộc cuối năm 1

- Paper 1 đã nộp
- Paper 2 có ablation table đầu tiên
- Paper 4 có architecture baseline skeleton

### Mốc bắt buộc cuối năm 1

Nếu tới cuối năm 1 mà chưa có:

- 1 paper đã nộp
- 1 paper có ablation mạnh
- 1 integration skeleton

thì 2 năm 4 Q1 sẽ rất khó giữ.

## Giai đoạn 5: Tháng 13-15

### Mục tiêu

- biến Paper 2 thành submission-ready
- dựng constrained RL baseline mạnh cho Paper 3
- nâng Paper 4 từ skeleton thành measurable protocol

### Việc phải làm

#### Paper 2

- final robustness runs
- strategy behavior analysis
- writing full draft
- internal review

#### Paper 3

- run constrained RL baseline
- run safe RL baseline nếu cần
- lock utility/safety metrics

#### Paper 4

- formalize mandatory feedback
- formalize event-triggered re-grounding conditions

### Đầu ra bắt buộc cuối tháng 15

- draft full Paper 2
- baseline tables Paper 3
- protocol v2 Paper 4

## Giai đoạn 6: Tháng 16-18

### Mục tiêu

- nộp Paper 2
- build dual-head core for Paper 3
- chạy full no-feedback và full feedback đầu tiên cho Paper 4

### Việc phải làm

#### Paper 2

- sửa cuối
- nộp bài

#### Paper 3

- build utility head
- build safety head
- integrate dual-head reward model
- start Lagrangian constrained update

#### Paper 4

- full no-feedback
- full feedback
- first closed-loop gain runs

### Đầu ra bắt buộc cuối tháng 18

- Paper 2 đã nộp
- dual-head reward model Paper 3 chạy được
- first closed-loop gain results Paper 4

### KPI giữa năm 2

Lúc này bạn phải có:

- 2 paper đã nộp
- 1 paper integration đã có core result
- 1 paper alignment đã có core model

## Giai đoạn 7: Tháng 19-21

### Mục tiêu

- hoàn thiện Paper 4 thành draft mạnh
- hoàn thiện thực nghiệm chính của Paper 3

### Việc phải làm

#### Paper 4

- feedback ablation
- pairwise integration comparison
- overhead analysis
- writing full draft

#### Paper 3

- utility-safety frontier
- ablation:
  - no utility head
  - no safety head
  - no Lagrangian
  - scalar reward baseline
- disturbance robustness

### Đầu ra bắt buộc cuối tháng 21

- draft Paper 4
- main experiment table Paper 3

### KPI cuối tháng 21

- Paper 4 phải đủ mạnh để là chapter integration chính
- Paper 3 phải có frontier đủ đẹp để viết bài

## Giai đoạn 8: Tháng 22-24

### Mục tiêu

- nộp hoặc chốt draft Paper 4
- chốt draft Paper 3
- viết luận án hoàn chỉnh
- chuẩn bị bảo vệ

### Việc phải làm

#### Paper 4

- sửa cuối
- nộp nếu kịp

#### Paper 3

- writing full draft
- internal review
- nếu không kịp nộp thì phải ở mức near-submission

#### Thesis

- ghép 4 paper thành luận án
- viết:
  - introduction
  - literature review
  - methodology integration
  - discussion
  - conclusion
- thống nhất notation
- chuẩn bị slide bảo vệ

### Đầu ra bắt buộc cuối tháng 24

- Paper 1: đã nộp / under review
- Paper 2: đã nộp / under review
- Paper 4: đã nộp hoặc very strong draft
- Paper 3: very strong draft hoặc nộp
- luận án hoàn chỉnh

## 6. Mức chuẩn Q1 cho từng paper trong kế hoạch 2 năm

## Paper 1

### Phải đạt

- conflict validation là nguồn tạo gain chính
- baseline maintenance/KG-RAG mạnh bị vượt
- stress tests tốt

### Không được phép yếu

- vì đây là paper nền và là bài mạnh nhất

## Paper 2

### Phải đạt

- hierarchy có gain rõ dưới perturbation
- MAMHSAN-like baseline hoặc graph-MARL mạnh bị vượt
- bài viết không loãng vì quá nhiều thành phần

### Có thể chấp nhận

- LRMP chỉ giữ nếu gain rõ

## Paper 3

### Phải đạt

- dual-head reward model tốt hơn scalar penalty
- constrained RL baseline bị vượt trên utility-safety frontier
- preference protocol đủ thuyết phục

### Không được làm

- overclaim RLHF quá mạnh

## Paper 4

### Phải đạt

- full feedback > full no-feedback
- feedback ablation rõ
- closed-loop gain có định nghĩa
- overhead được báo cáo

### Không được phép yếu

- vì đây là paper khóa luận điểm kiến trúc

## 7. Chế độ làm việc bắt buộc trong 2 năm

Để lịch trình này khả thi, bạn phải làm theo nhịp gần như bắt buộc:

### Mỗi tuần

- 1 buổi literature + note consolidation
- 3-4 buổi implementation/experiment
- 1 buổi result cleanup + figure/table
- 1 buổi writing

### Mỗi tháng

- review tiến độ theo KPI
- chốt paper nào đang là priority 1
- cắt ngay phần nào không tạo gain

### Mỗi quý

- phải có ít nhất một đầu ra cấp quý:
  - draft
  - table kết quả mạnh
  - submission

## 8. Những thứ tuyệt đối không được làm nếu muốn 2 năm 4 Q1

- không đọc thêm paper lan man mà không map vào gap hiện tại
- không đổi novelty của paper sau khi đã chốt
- không chase mọi kỹ thuật mới đọc được
- không để Paper 3 kéo chậm Paper 4
- không để integration dồn đến 6 tháng cuối
- không giữ những module phụ không tạo gain rõ

## 9. KPI 6 mốc sinh tử

## Mốc 1: Hết tháng 3

Phải có:

- proposal khóa xong
- framework quản lý nghiên cứu xong
- Paper 1 data pipeline khởi động

## Mốc 2: Hết tháng 6

Phải có:

- Paper 1 main results đầu tiên
- Paper 2 baseline table
- Paper 3 protocol rõ

## Mốc 3: Hết tháng 9

Phải có:

- draft Paper 1
- core model Paper 2
- interface spec v1

## Mốc 4: Hết tháng 12

Phải có:

- Paper 1 nộp
- Paper 2 ablation
- Paper 4 skeleton

## Mốc 5: Hết tháng 18

Phải có:

- Paper 2 nộp
- Paper 3 dual-head chạy được
- Paper 4 closed-loop gain đầu tiên

## Mốc 6: Hết tháng 24

Phải có:

- 2 paper đã nộp chắc chắn
- 2 paper còn lại ở mức nộp hoặc near-submission mạnh
- luận án hoàn chỉnh

## 10. Kết luận cuối

Nếu bạn thật sự chấp nhận chế độ cường độ tối đa trong 2 năm và không giảm paper nào, thì chiến lược đúng là:

- Paper 1 phải là mũi xuyên phá
- Paper 2 phải reuse backbone và tập trung đúng hierarchy
- Paper 3 phải thực dụng nhưng vẫn đủ sắc
- Paper 4 phải được bắt đầu sớm và giữ vai trò khóa luận điểm kiến trúc

Nói ngắn gọn:

- `6 tháng đầu`: sinh tồn bằng Paper 1
- `12 tháng đầu`: phải có 1 bài nộp và 1 bài tăng tốc
- `18 tháng`: phải có 2 bài nộp và integration có kết quả
- `24 tháng`: phải có luận án hoàn chỉnh và 4 paper ở trạng thái mạnh

Đây là kịch bản cực khó, nhưng nếu làm đúng cách, nó là kịch bản khả thi nhất để giữ mục tiêu `2 năm + 4 paper Q1-profile + ra industry sau đó`.
