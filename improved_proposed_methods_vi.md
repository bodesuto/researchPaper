# Phương Pháp Đề Xuất Cải Tiến Cho 4 Paper CAMAS

## 1. Mục tiêu của file này

File này chỉ tập trung vào phần quan trọng nhất của toàn bộ roadmap: `phương pháp đề xuất cải tiến`.

Mục tiêu không phải là nhắc lại proposal, mà là trả lời rất rõ cho từng paper:

- phương pháp gốc của literature đang dừng ở đâu
- mình phải cải tiến chính xác ở đâu
- cải tiến nào là lõi
- cải tiến nào chỉ là phụ trợ
- phương pháp cuối cùng phải được mô tả như thế nào để đủ sức thành contribution Q1

Nguyên tắc của file này:

- chỉ nói về `method`
- không lan man sang phần roadmap tổng quát
- mỗi paper có một phương pháp cải tiến trung tâm

## 2. Cách hiểu đúng về “phương pháp đề xuất cải tiến”

Một phương pháp đề xuất cải tiến mạnh không phải là:

- ghép nhiều kỹ thuật mạnh lại với nhau

Mà là:

- xác định đúng một điểm yếu thật của phương pháp nền
- thay đổi logic mô hình hóa hoặc logic ra quyết định tại đúng điểm yếu đó
- chứng minh thay đổi đó tạo ra lợi ích mà phương pháp nền không có

Vì vậy, với mỗi paper, bạn phải tách rất rõ:

- `phương pháp nền`
- `điểm yếu kỹ thuật của phương pháp nền`
- `phần cải tiến mới`
- `logic vì sao phần cải tiến đó tạo ra gain`

## 3. Paper 1 - Phương pháp đề xuất cải tiến

## 3.1. Phương pháp nền của literature

Phương pháp nền gần nhất là:

- semantic retrieval
- KG-RAG
- dual-memory knowledge graph với observability support

Trong các phương pháp này, semantic memory cung cấp tri thức nền, còn observability memory cung cấp log/trace/execution data để grounding tốt hơn.

## 3.2. Điểm yếu của phương pháp nền

Phương pháp nền vẫn có ba điểm yếu kỹ thuật quan trọng:

### Điểm yếu 1: Observability mới chỉ được dùng như evidence bổ sung

Nghĩa là:

- observability giúp support reasoning
- nhưng chưa thực sự có quyền phủ định reasoning

Trong maintenance, đây là thiếu sót lớn, vì log/trace mới nhất có thể bác bỏ một kết luận đúng về mặt tri thức nền nhưng sai về mặt vận hành.

### Điểm yếu 2: Retrieval chưa có semantics theo thời gian

Phần lớn retrieval hiện tại thiên về:

- relevance theo nội dung
- similarity theo query

nhưng chưa xét đầy đủ:

- fact validity theo thời điểm
- stale evidence
- event recency
- source freshness

### Điểm yếu 3: Đầu ra của nhận thức chưa đủ giàu ngữ nghĩa để dùng cho loop sau

Nếu output chỉ là:

- answer
- diagnosis
- action suggestion

thì Coordination và Alignment rất khó dùng lại một cách chuẩn hóa.

## 3.3. Phương pháp cải tiến đề xuất

Phương pháp cải tiến cho Paper 1 nên được định nghĩa là:

`Conflict-Validated Temporal Dual-Memory Grounding`

hay viết đầy đủ hơn:

`An observability-grounded dual-memory knowledge graph with temporal evidence retrieval and semantic-observability conflict validation for industrial maintenance reasoning.`

## 3.4. Cấu trúc phương pháp cải tiến

Phương pháp này gồm 4 khối chính.

### Khối 1: Semantic Memory

Semantic memory giữ:

- cấu trúc thiết bị
- quan hệ thành phần
- causal links
- maintenance procedures
- fault-action mappings

Vai trò:

- làm knowledge prior
- cung cấp semantic candidate facts

### Khối 2: Observability Memory

Observability memory không chỉ là kho log thô. Nó phải được chuẩn hóa thành graph evidence có cấu trúc:

- entity
- event type
- timestamp
- source
- reliability
- execution outcome
- state transition

Vai trò:

- cung cấp operational truth proxy
- hỗ trợ kiểm định trạng thái hiện tại

### Khối 3: Temporal Evidence Retrieval

Đây là cải tiến đầu tiên.

Retrieval không chỉ tính theo semantic similarity, mà phải theo hàm tổng hợp:

- semantic relevance
- entity match
- temporal recency
- source reliability
- execution consistency

Ý nghĩa kỹ thuật:

- cùng một evidence đúng về mặt nội dung nhưng quá cũ thì phải bị giảm trọng số
- evidence mới nhưng nguồn yếu thì không được ưu tiên tuyệt đối
- evidence đã từng dẫn tới successful execution phải được tăng trọng số

### Khối 4: Semantic-Observability Conflict Validation

Đây là cải tiến mạnh nhất.

Thay vì chỉ lấy evidence để hỗ trợ answer, hệ phải kiểm tra các dạng conflict:

- semantic fact vs current operational state conflict
- recommended action vs recent execution history conflict
- diagnosis vs sensor/event transition conflict
- plan vs currently observed availability conflict

Conflict phải tác động trực tiếp tới:

- evidence ranking
- grounded state construction
- uncertainty score
- final recommendation confidence

## 3.5. Đầu ra chuẩn hóa của phương pháp

Phương pháp Paper 1 phải sinh ra đầu ra chuẩn hóa gồm:

- `grounded_state`
- `evidence_set`
- `inconsistency_score`
- `uncertainty_score`

Đây không chỉ là đầu ra evaluation, mà còn là output chuẩn để Coordination và Integration dùng lại.

## 3.6. Đóng góp kỹ thuật mới thật sự

Đóng góp kỹ thuật mới không phải là:

- dùng dual-memory

Mà là:

- biến observability từ evidence phụ thành tín hiệu kiểm định vận hành bắt buộc
- biến temporal validity thành điều kiện của grounding
- biến conflict thành thành phần cấu trúc của reasoning

## 3.7. Câu mô tả phương pháp nên dùng

`Phương pháp đề xuất xây dựng một dual-memory knowledge graph có neo observability, trong đó evidence được truy xuất theo ngữ nghĩa và hiệu lực thời gian, sau đó được kiểm định thông qua cơ chế semantic-observability conflict validation để tạo grounded state có thể truy vết bằng chứng và lượng hóa độ bất nhất của suy luận.`

## 4. Paper 2 - Phương pháp đề xuất cải tiến

## 4.1. Phương pháp nền của literature

Phương pháp nền mạnh nhất là:

- graph-based MARL cho FJSP
- MAMHSAN
- MD-MDP
- attention-enhanced heterogeneous graph embedding

## 4.2. Điểm yếu của phương pháp nền

### Điểm yếu 1: Chưa tách rõ chiến lược và tác nghiệp

Phần lớn framework hiện có tối ưu scheduling bằng một policy tương đối phẳng, dù có graph encoder mạnh.

Nhưng trong dynamic FJSP, cần tách:

- `strategy-level coordination`
- `dispatch-level execution`

Nếu không tách, policy thường phản ứng tốt cục bộ nhưng thiếu điều chỉnh chiến lược khi perturbation lớn.

### Điểm yếu 2: Context adaptation chưa thành logic điều phối

Graph representation thường mạnh ở:

- nắm cấu trúc

nhưng chưa đủ mạnh ở:

- thay đổi hành vi theo context shift

Ví dụ:

- khi máy hỏng
- khi due-date pressure tăng
- khi hàng đợi mất cân bằng

policy cần đổi logic quyết định, không chỉ đổi embedding nhẹ.

### Điểm yếu 3: Robustness dưới perturbation chưa là trung tâm phương pháp

Nhiều bài báo cáo kết quả trên benchmark chuẩn, nhưng chưa chứng minh mạnh:

- phương pháp nào thực sự bền hơn dưới dynamic perturbation

## 4.3. Phương pháp cải tiến đề xuất

Phương pháp cải tiến cho Paper 2 nên được định nghĩa là:

`Hierarchical Context-Adaptive Graph Coordination`

hoặc đầy đủ:

`A hierarchical graph-based multi-agent coordination framework with context-adaptive state representation for dynamic FJSP under perturbations.`

## 4.4. Cấu trúc phương pháp cải tiến

Phương pháp này gồm 4 khối chính.

### Khối 1: Heterogeneous Graph State Modeling

Mô hình hóa FJSP bằng graph gồm:

- job nodes
- operation nodes
- machine nodes
- precedence edges
- compatibility edges
- resource contention edges
- temporal state features

Vai trò:

- giữ được cấu trúc scheduling
- tạo input nhất quán cho policy phân cấp

### Khối 2: Master Policy

Đây là cải tiến lõi.

Master policy không chọn action thấp tầng trực tiếp, mà chọn:

- scheduling strategy
- dispatch priority mode
- bottleneck focus
- subgoal

Ví dụ:

- ưu tiên giảm tardiness
- ưu tiên giải bottleneck machine
- ưu tiên giữ balance utilization

Vai trò:

- biến coordination từ phản ứng cục bộ thành điều phối chiến lược

### Khối 3: Worker Policies

Worker agents thực hiện:

- machine assignment
- operation dispatch
- local sequencing

theo chiến lược mà master policy đã chọn.

Vai trò:

- xử lý action chi tiết
- cho phép thực thi linh hoạt ở tầng thấp

### Khối 4: Context-Adaptive Representation

Đây là cải tiến quan trọng thứ hai.

Biểu diễn trạng thái không được cố định sau graph encoding, mà phải được điều chỉnh theo:

- due-date pressure
- machine congestion
- breakdown status
- tardiness risk
- system imbalance

Nếu dùng LRMP, thì LRMP phải được định vị đúng là:

- `state-conditioned representation adapter`

không phải novelty độc lập ngang với hierarchy.

## 4.5. Vai trò của MD-MDP

MD-MDP nên được giữ như:

- framework formulation support

không nên là novelty chính, trừ khi bạn thật sự phát triển tiếp nó.

Cách dùng đúng:

- action có nhiều chiều
- reward có nhiều mục tiêu
- hierarchy dùng MD-MDP để chọn và phân giải tradeoff

## 4.6. Đóng góp kỹ thuật mới thật sự

Đóng góp kỹ thuật mới của Paper 2 phải là:

- đưa `decision hierarchy` vào graph-based coordination
- làm cho context shift ảnh hưởng trực tiếp tới chiến lược điều phối
- chứng minh hierarchy tạo gain dưới perturbation

Nếu không chứng minh được tầng master policy có hành vi khác nhau theo context, bài sẽ rất yếu.

## 4.7. Câu mô tả phương pháp nên dùng

`Phương pháp đề xuất mô hình hóa dynamic FJSP bằng heterogeneous graph và bổ sung một cơ chế điều phối phân cấp, trong đó master policy chọn chiến lược điều độ theo ngữ cảnh hệ thống, còn worker policies thực hiện dispatch cục bộ dựa trên biểu diễn graph thích ứng theo perturbation.`

## 5. Paper 3 - Phương pháp đề xuất cải tiến

## 5.1. Phương pháp nền của literature

Phương pháp nền hiện có tách làm hai nhóm:

- RLHF/CoRLHF: mạnh về preference alignment
- safe RL/constrained RL: mạnh về feasibility và safety

## 5.2. Điểm yếu của phương pháp nền

### Điểm yếu 1: Reward thường bị scalar hóa quá sớm

Nhiều phương pháp nhét mọi thứ vào:

- một reward scalar
- cộng utility với penalty

Điều này rất yếu trong cyber-physical systems vì:

- utility và safety không cùng bản chất
- scalar penalty thường không mô hình được hard constraints rõ

### Điểm yếu 2: Preference learning và feasibility learning bị tách rời

RLHF-style work hỏi:

- con người thích trajectory nào

Safe RL hỏi:

- trajectory nào khả thi

Smart grid cần cả hai.

### Điểm yếu 3: Human preference thật khó thu thập ở quy mô lớn

Nếu cố bám RLHF theo nghĩa nguyên bản, Paper 3 sẽ gần như không khả thi.

## 5.3. Phương pháp cải tiến đề xuất

Phương pháp cải tiến nên được định nghĩa là:

`Constraint-Aware Preference-Guided Policy Optimization`

hoặc đầy đủ:

`A dual-head preference-feasibility reward modeling framework with Lagrangian constrained policy optimization for safe smart grid control.`

## 5.4. Cấu trúc phương pháp cải tiến

Phương pháp này gồm 4 khối chính.

### Khối 1: Preference Generation Protocol

Không dùng human feedback quy mô lớn ngay từ đầu.

Thay vào đó:

- simulated expert preference
- utility-safety-aware trajectory ranking
- expert-rule consistency checking
- human validation subset nhỏ

Vai trò:

- tạo preference signal khả thi
- giữ bài ở mức làm được

### Khối 2: Dual-Head Reward Model

Đây là lõi kỹ thuật mạnh nhất.

Reward model phải có:

- `utility head`
- `safety head`

Utility head học:

- preference ranking
- economic objective
- operational desirability

Safety head học:

- violation likelihood
- infeasibility risk
- constraint margin risk

Điểm quan trọng:

- hai đầu này không được collapse thành một scalar quá sớm

### Khối 3: Constraint-Aware Policy Update

Policy update phải dùng:

- Lagrangian constrained optimization

Vai trò:

- utility head kéo policy theo preference
- safety head giữ policy trong không gian khả thi

Đây là chỗ biến bài từ reward engineering thành constrained optimization thật.

### Khối 4: Utility-Safety Frontier Analysis

Đây là phần phương pháp đánh giá nhưng thực ra là một phần không thể thiếu của contribution.

Bạn phải report:

- frontier giữa utility và safety

chứ không chỉ report một điểm.

Lý do:

- nếu không có frontier, reviewer sẽ nói đây chỉ là tuning tradeoff.

## 5.5. Đóng góp kỹ thuật mới thật sự

Đóng góp kỹ thuật mới của Paper 3 không phải:

- “áp RLHF vào smart grid”

Mà là:

- tách utility preference khỏi feasibility
- ghép hai loại tín hiệu đó trong constrained policy update
- thiết kế preference protocol khả thi cho cyber-physical domain

## 5.6. Câu mô tả phương pháp nên dùng

`Phương pháp đề xuất xây dựng một reward model hai đầu để tách utility preference khỏi safety feasibility, sau đó cập nhật policy bằng Lagrangian constrained optimization nhằm tối ưu utility dưới hard constraints thay vì scalar hóa utility và safety vào cùng một reward đơn.`

## 6. Paper 4 - Phương pháp đề xuất cải tiến

## 6.1. Phương pháp nền của literature

Phương pháp nền hiện có thường là:

- module pipelines
- integrated systems không formalized interfaces
- closed-loop claims nhưng thiếu feedback semantics

## 6.2. Điểm yếu của phương pháp nền

### Điểm yếu 1: Interface chưa có semantics đủ rõ

Nhiều hệ chỉ nói:

- perception output feeds coordination

nhưng không chỉ ra:

- uncertainty đi đâu
- conflict signal đi đâu
- reward/constraint signal quay về thế nào

### Điểm yếu 2: Feedback chỉ là khái niệm, chưa thành protocol

Không có:

- trigger conditions
- required feedback signals
- update semantics

thì closed-loop chỉ là một sơ đồ.

### Điểm yếu 3: Thiếu metric ở cấp kiến trúc

Nếu không đo `closed-loop gain`, bạn không chứng minh được architecture contribution.

## 6.3. Phương pháp cải tiến đề xuất

Phương pháp cải tiến cho Paper 4 nên được định nghĩa là:

`Closed-Loop Feedback-Semantic Integration Protocol`

hoặc đầy đủ:

`A closed-loop cognitive multi-agent protocol with standardized interfaces, mandatory feedback semantics, and event-triggered re-grounding.`

## 6.4. Cấu trúc phương pháp cải tiến

Phương pháp gồm 4 khối chính.

### Khối 1: Standardized Interface Layer

Perception output:

- grounded_state
- evidence_set
- inconsistency_score
- uncertainty_score

Coordination output:

- action_candidates
- policy_distribution
- context_embedding
- coordination_confidence

Alignment output:

- updated_reward_model
- updated_constraint_model
- policy_update_signal
- risk_aware_prior

### Khối 2: Mandatory Feedback Semantics

Feedback từ Alignment không phải optional.

Nó phải bắt buộc trả:

- risk-aware prior
- policy update signal
- constraint update

để:

- perception điều chỉnh retrieval/conflict sensitivity
- coordination điều chỉnh action filtering

### Khối 3: Event-Triggered Re-Grounding

Đây là kỹ thuật cải tiến mạnh thứ hai của Paper 4.

Re-grounding được kích hoạt nếu:

- uncertainty vượt ngưỡng
- conflict score tăng
- near-violation xuất hiện
- safety head cảnh báo risk tăng

Điểm mạnh:

- loop không chỉ là periodic update
- loop có semantics theo risk

### Khối 4: Closed-Loop Gain Evaluation

Bạn phải định nghĩa rõ:

- gain của full feedback loop so với full no-feedback pipeline

Nếu không, Paper 4 không có methodological core.

## 6.5. Đóng góp kỹ thuật mới thật sự

Đóng góp kỹ thuật mới của Paper 4 là:

- formal hóa feedback semantics giữa 3 module
- biến uncertainty/conflict/safety thành tín hiệu vòng lặp
- chứng minh loop tạo gain đo được

Không phải:

- “ghép 3 module”

## 6.6. Câu mô tả phương pháp nên dùng

`Phương pháp đề xuất chuẩn hóa interface và feedback semantics giữa grounded perception, adaptive coordination và safe alignment, đồng thời đưa vào cơ chế event-triggered re-grounding để biến loop phản hồi từ mức pipeline khái niệm thành protocol có thể kiểm chứng bằng closed-loop gain.`

## 7. Bảng chốt phương pháp cải tiến

| Paper | Phương pháp gốc | Điểm yếu kỹ thuật | Phương pháp cải tiến mới | Lõi contribution |
|---|---|---|---|---|
| Paper 1 | Dual-memory grounding | chưa có temporal validity và conflict semantics mạnh | Conflict-Validated Temporal Dual-Memory Grounding | temporal conflict-aware operational grounding |
| Paper 2 | Graph-attention MARL | chưa có strategic decomposition rõ | Hierarchical Context-Adaptive Graph Coordination | strategy-dispatch hierarchy under perturbation |
| Paper 3 | CoRLHF + constrained RL rời rạc | utility và safety bị scalar hóa hoặc tách rời | Constraint-Aware Preference-Guided Policy Optimization | dual-head reward + constrained policy update |
| Paper 4 | one-way integration | thiếu interface semantics và measurable loop gain | Closed-Loop Feedback-Semantic Integration Protocol | mandatory feedback + event-triggered re-grounding |

## 8. Kết luận cuối

Nếu bạn muốn CAMAS có cơ hội thành các paper Q1, thì phần “phương pháp đề xuất cải tiến” phải được viết đúng theo logic sau:

- `Paper 1`: không phải thêm observability vào retrieval, mà là biến conflict và thời gian thành logic grounding.
- `Paper 2`: không phải thêm một encoder mạnh hơn, mà là tách chiến lược khỏi dispatch dưới dynamic perturbation.
- `Paper 3`: không phải mang RLHF sang smart grid, mà là tách utility khỏi safety và tối ưu chúng dưới hard constraints.
- `Paper 4`: không phải ghép module, mà là formal hóa feedback protocol và chứng minh nó tạo gain đo được.

Đó mới là các cải tiến phương pháp đủ mạnh để kể thành technical contribution ở mức Q1.
