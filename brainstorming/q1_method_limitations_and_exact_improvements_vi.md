# Q1 Method Limitations Và Exact Improvements Cho 4 Paper CAMAS

## 1. Mục tiêu của file này

File này được viết để trả lời chính xác câu hỏi:

- phương pháp cũ đang yếu ở đâu
- bạn phải cải tiến chính xác phần nào
- cải tiến nào là lõi
- cải tiến nào chỉ là phụ
- vì sao cải tiến đó đủ mạnh để thành novelty ở mức Q1

Đây là file dùng để chốt `methodological contribution`.

Mỗi paper được phân tích theo đúng cấu trúc:

1. phương pháp cũ gần nhất
2. hạn chế cốt lõi của phương pháp cũ
3. exact improvements
4. cải tiến lõi và cải tiến phụ
5. expected gain
6. vì sao đủ profile Q1
7. nếu không có cải tiến đó thì bài sẽ yếu ở đâu

## 2. Paper 1 - Perception

## 2.1. Phương pháp cũ gần nhất

Phương pháp gần nhất trong literature là:

- semantic retrieval
- KG-RAG
- dual-memory grounding với observability support

Paper gần nhất bạn đang bám là:

- `Addressing hallucinations in generative AI agents using observability and dual memory knowledge graphs`

## 2.2. Hạn chế cốt lõi của phương pháp cũ

### Hạn chế 1: Observability mới dừng ở mức nguồn evidence hỗ trợ

Trong phương pháp cũ, observability giúp tăng grounding nhưng chưa được nâng lên thành:

- nguồn kiểm định bắt buộc
- nguồn bác bỏ kết luận sai

Nói cách khác, observability chủ yếu `support`, chưa `invalidate`.

Trong maintenance, đây là điểm yếu vì:

- tri thức nền có thể đúng về logic nhưng sai với trạng thái thiết bị hiện tại
- nếu observability không có quyền phủ định, tác nhân vẫn có thể grounded sai

### Hạn chế 2: Retrieval chưa đủ semantics theo thời gian

Phương pháp cũ mạnh ở semantic relevance nhưng chưa đủ mạnh ở:

- fact validity theo thời điểm
- stale logs
- event freshness
- temporal decay

Trong maintenance, bằng chứng cũ có thể nguy hiểm gần như bằng bằng chứng sai.

### Hạn chế 3: Chưa có conflict semantics như một tầng reasoning riêng

Phương pháp cũ có thể dùng cả semantic memory và observability memory, nhưng chưa biến:

- semantic-observability conflict

thành một thành phần mô hình hóa có tác dụng trực tiếp lên:

- grounded state
- uncertainty
- recommendation confidence

### Hạn chế 4: Hallucination chưa được operationalize đủ chặt trong industrial maintenance

Nếu hallucination chỉ được xem như factual wrong answer, bài sẽ yếu trong công nghiệp.

Phương pháp cũ chưa đẩy mạnh định nghĩa:

- recommendation không có evidence support
- recommendation mâu thuẫn với execution history
- recommendation bỏ qua conflict vận hành đang tồn tại

## 2.3. Exact improvements đề xuất

### Improvement 1: Temporal Evidence Retrieval

Thay vì retrieval chủ yếu theo semantic similarity, đề xuất mới thêm một hàm retrieval dựa trên:

- semantic relevance
- entity consistency
- temporal recency
- source reliability
- execution consistency

Điểm cải tiến chính xác là:

- `time` không còn là metadata phụ, mà trở thành một chiều bắt buộc để đánh giá validity của evidence

### Improvement 2: Semantic-Observability Conflict Validation

Thêm một tầng kiểm định explicit để phát hiện:

- semantic fact đúng về mặt domain nhưng bị observability hiện tại bác bỏ
- recommendation mâu thuẫn với log/trace gần nhất
- action đề xuất trái với execution history đã xác thực

Điểm cải tiến chính xác là:

- conflict không còn là hiện tượng phụ
- conflict trở thành `decision signal`

### Improvement 3: Grounded State With Operational Uncertainty

Thay đầu ra từ answer/diagnosis đơn thuần sang:

- grounded_state
- evidence_set
- inconsistency_score
- uncertainty_score

Điểm cải tiến chính xác là:

- output không chỉ để trả lời user
- output còn là structured state cho các module sau

### Improvement 4: Maintenance-Specific Hallucination Formalization

Thiết kế định nghĩa hallucination theo 3 điều kiện:

- unsupported by evidence
- contradicted by observability
- inconsistent with execution history

Điểm cải tiến chính xác là:

- metric được neo vào semantics vận hành, không còn là factual correctness chung chung

## 2.4. Cải tiến lõi và cải tiến phụ

### Cải tiến lõi

- `Semantic-Observability Conflict Validation`

Đây là novelty trung tâm mạnh nhất của Paper 1.

### Cải tiến phụ nhưng quan trọng

- temporal evidence retrieval
- grounded state with uncertainty semantics
- maintenance-specific hallucination formalization

## 2.5. Expected gain

Cải tiến này được kỳ vọng tạo ra:

- giảm hallucination rate rõ hơn dual-memory retrieval thông thường
- tăng evidence grounding score
- tăng robustness khi log thiếu hoặc bằng chứng mâu thuẫn
- tăng độ tin cậy khi đưa recommendation bảo trì

## 2.6. Vì sao đủ profile Q1

Contribution đủ mạnh ở mức Q1 vì:

- nó không chỉ thêm một memory mới
- nó thay đổi bản chất grounding từ retrieval-based support sang conflict-validated operational grounding
- nó mở ra một câu hỏi thực nghiệm mới:
  - khi semantic memory và observability xung đột, hệ nên grounded thế nào?

Đây là thay đổi ở mức semantics của phương pháp, không phải tuning của phương pháp cũ.

## 2.7. Nếu không có cải tiến đó thì bài yếu ở đâu

Nếu bỏ conflict validation, Paper 1 sẽ chỉ còn là:

- một dual-memory retrieval variant

và rất dễ bị reviewer đánh giá là:

- incremental extension của paper observability cũ

## 3. Paper 2 - Coordination

## 3.1. Phương pháp cũ gần nhất

Phương pháp gần nhất là:

- graph-based scheduling RL
- MAMHSAN
- attention-enhanced heterogeneous graph embedding
- MD-MDP for FJSP

## 3.2. Hạn chế cốt lõi của phương pháp cũ

### Hạn chế 1: Chưa có strategic hierarchy rõ

Phương pháp cũ rất mạnh ở:

- state representation
- feature extraction
- collaborative action selection

Nhưng chưa đủ rõ ở:

- strategy-level decision making
- dispatch-level execution separation

Điều này làm policy dễ phản ứng tốt cục bộ nhưng thiếu khả năng đổi chiến lược khi perturbation lớn xảy ra.

### Hạn chế 2: Context adaptation chưa trực tiếp chi phối policy hierarchy

Graph encoder mạnh không đồng nghĩa với policy biết đổi chiến lược khi:

- máy hỏng
- due-date pressure tăng
- hệ mất cân bằng tài nguyên

Nếu context adaptation chỉ nằm ở embedding mà không tác động lên strategy layer, contribution dễ yếu.

### Hạn chế 3: Robustness chưa phải trục kiểm chứng trung tâm

Nhiều phương pháp cũ chứng minh tốt trên benchmark chuẩn, nhưng chưa chứng minh đủ rằng:

- hierarchy hay context adaptation giúp dưới dynamic perturbation

### Hạn chế 4: Quá nhiều thành phần mạnh nhưng chưa tách được ai là nguồn tạo gain chính

MAMHSAN-like papers thường có:

- graph
- attention
- MD-MDP
- MARL

Nếu bài của bạn tiếp tục cộng thêm hierarchy và LRMP mà không tách rõ vai trò, reviewer sẽ xem là tổ hợp incremental.

## 3.3. Exact improvements đề xuất

### Improvement 1: Strategy-Dispatch Decomposition

Thêm một `master policy` để chọn:

- scheduling strategy
- subgoal
- dispatch priority mode

và `worker policies` để chọn:

- machine assignment
- operation dispatch
- sequencing action

Điểm cải tiến chính xác là:

- chuyển bài toán từ flat action optimization sang hierarchical coordination

### Improvement 2: Context-Adaptive Graph Representation

Thêm một tầng context adaptation để graph representation thay đổi theo:

- due-date pressure
- bottleneck severity
- machine breakdown state
- queue congestion

Nếu dùng LRMP, LRMP phải làm đúng vai trò này.

Điểm cải tiến chính xác là:

- representation không chỉ encode state
- representation còn điều chỉnh cách policy đọc state theo context

### Improvement 3: Dynamic Perturbation-Centered Evaluation

Đưa dynamic perturbation từ phần phụ thành phần cốt lõi của bài:

- machine breakdown
- urgent job arrival
- due-date shift
- processing-time uncertainty

Điểm cải tiến chính xác là:

- chuyển tiêu chuẩn “model tốt” từ benchmark score sang perturbation robustness

### Improvement 4: Hierarchy-Aware Action/Reward Structuring

Nếu giữ MD-MDP, bạn phải dùng nó để:

- phân giải reward/action giữa tầng chiến lược và tầng tác nghiệp

Điểm cải tiến chính xác là:

- MD-MDP không chỉ là formulation cũ được bê lại
- nó trở thành khung hỗ trợ cho hierarchy

## 3.4. Cải tiến lõi và cải tiến phụ

### Cải tiến lõi

- `Strategy-Dispatch Decomposition`

### Cải tiến phụ

- context-adaptive graph representation
- LRMP nếu có ích
- hierarchy-aware reward/action structuring

## 3.5. Expected gain

Cải tiến này được kỳ vọng tạo ra:

- giảm makespan và tardiness trong dynamic FJSP
- tăng robustness dưới perturbation
- đổi chiến lược scheduling linh hoạt hơn so với flat MARL

## 3.6. Vì sao đủ profile Q1

Contribution đủ mạnh ở mức Q1 vì:

- nó không chỉ thêm encoder
- nó thay đổi cấu trúc decision process
- nó mở ra câu hỏi thực nghiệm mới:
  - strategy-level coordination có tạo gain riêng dưới perturbation không?

Đó là contribution ở mức policy structure, không chỉ feature extraction.

## 3.7. Nếu không có cải tiến đó thì bài yếu ở đâu

Nếu không có hierarchy, Paper 2 rất dễ rơi thành:

- MAMHSAN + context adapter

và sẽ bị reviewer xem là một incremental graph-MARL extension.

## 4. Paper 3 - Alignment

## 4.1. Phương pháp cũ gần nhất

Phương pháp gần nhất là:

- CoRLHF cho policy-reward co-optimization
- constrained RL/safe RL cho control
- graph RL cho unit commitment

## 4.2. Hạn chế cốt lõi của phương pháp cũ

### Hạn chế 1: Utility và safety thường bị scalar hóa vào cùng một reward

Đây là hạn chế nghiêm trọng nhất.

Khi utility và safety bị ép vào một scalar reward:

- tradeoff trở nên khó diễn giải
- hard constraints dễ biến thành penalty mềm
- policy có thể tối ưu utility bằng cách đánh đổi safety ngầm

### Hạn chế 2: Preference learning và feasibility learning chưa được hợp nhất

RLHF-style methods học:

- cái gì được ưu tiên

Safe RL học:

- cái gì được phép

Nhưng trong smart grid, cần biết đồng thời:

- trajectory nào tốt
- trajectory nào khả thi

### Hạn chế 3: CoRLHF không được thiết kế cho cyber-physical control

Các điểm khác biệt lớn:

- action/state semantics khác
- hard constraints vật lý thật
- reward safety không thể chỉ là preference

### Hạn chế 4: Human preference thật khó thu thập ở quy mô đủ lớn

Nếu không giải quyết điểm này, Paper 3 rất dễ không khả thi.

## 4.3. Exact improvements đề xuất

### Improvement 1: Dual-Head Reward Model

Thay scalar reward bằng:

- utility head
- safety head

Điểm cải tiến chính xác là:

- utility preference và feasibility được mô hình hóa tách biệt

### Improvement 2: Preference Generation Protocol for Cyber-Physical Systems

Xây một giao thức preference thực dụng:

- simulated expert preference
- utility-safety-aware ranking
- rule-consistency filtering
- human validation subset

Điểm cải tiến chính xác là:

- giải quyết bài toán preference realism mà không cần human data lớn

### Improvement 3: Lagrangian Constrained Policy Optimization

Thêm constrained optimizer để:

- utility head kéo policy theo preference
- safety head giữ policy trong vùng khả thi

Điểm cải tiến chính xác là:

- hard constraints không còn là penalty phụ

### Improvement 4: Utility-Safety Frontier Reporting

Báo cáo frontier thay vì một điểm scalar result.

Điểm cải tiến chính xác là:

- biến contribution thành controllable tradeoff optimization, không chỉ reward tuning

## 4.4. Cải tiến lõi và cải tiến phụ

### Cải tiến lõi

- `Dual-Head Reward Model + Lagrangian Constrained Update`

### Cải tiến phụ

- simulated preference protocol
- human validation subset
- frontier reporting

## 4.5. Expected gain

Cải tiến này được kỳ vọng tạo ra:

- giảm safety violation so với constrained RL baseline
- giữ utility tốt hơn reward-penalty scalarization
- tạo utility-safety frontier tốt hơn preference-only hoặc safety-only baseline

## 4.6. Vì sao đủ profile Q1

Contribution đủ mạnh ở mức Q1 vì:

- nó xử lý đúng giao điểm mà literature hiện còn tách rời:
  - preference utility
  - hard-constraint safety
- nó thay đổi logic mô hình hóa reward
- nó đưa safety từ reward engineering sang constrained optimization

Đây là methodological contribution thực chất, không phải đổi domain đơn thuần.

## 4.7. Nếu không có cải tiến đó thì bài yếu ở đâu

Nếu không có dual-head + constrained update, Paper 3 sẽ rất dễ trở thành:

- constrained RL with a more complicated reward

và sẽ không đủ mới ở mức Q1.

## 5. Paper 4 - Integration

## 5.1. Phương pháp cũ gần nhất

Phương pháp gần nhất trong literature thường là:

- integrated pipelines
- cognitive architectures
- modular agent systems

Nhưng đa số thiếu:

- interface semantics
- feedback semantics
- measurable architectural gain

## 5.2. Hạn chế cốt lõi của phương pháp cũ

### Hạn chế 1: Module interaction chưa được formalize

Nhiều phương pháp chỉ mô tả:

- module A feeds module B

nhưng không formalize:

- output object
- uncertainty propagation
- conflict propagation
- risk propagation

### Hạn chế 2: Feedback loop thiếu semantics

Nếu feedback không có:

- trigger
- required signals
- effect on downstream/upstream modules

thì closed-loop chỉ là khái niệm.

### Hạn chế 3: Chưa có metric để đo gain ở cấp kiến trúc

Nếu chỉ báo end-to-end performance, reviewer không biết:

- gain đến từ method nào
- gain đến từ loop thật hay chỉ do thêm module

### Hạn chế 4: Nhiều system papers bị yếu vì không tách được novelty kiến trúc với novelty thuật toán

Paper 4 của bạn rất dễ dính rủi ro này nếu không khóa claim.

## 5.3. Exact improvements đề xuất

### Improvement 1: Standardized Interface Layer

Formalize interface của 3 module:

- perception output
- coordination output
- alignment output

Điểm cải tiến chính xác là:

- biến module interaction thành đối tượng mô hình hóa rõ

### Improvement 2: Mandatory Feedback Semantics

Quy định rõ feedback tối thiểu từ Alignment phải trả lại:

- policy_update_signal
- updated_constraint_model
- risk_aware_prior

Điểm cải tiến chính xác là:

- feedback không còn là optional
- feedback trở thành primitive của kiến trúc

### Improvement 3: Event-Triggered Re-Grounding

Thiết kế trigger theo:

- high uncertainty
- high conflict
- near-violation
- rising risk

Điểm cải tiến chính xác là:

- loop trở thành event-driven protocol, không chỉ periodic pipeline

### Improvement 4: Closed-Loop Gain Metric

Định nghĩa rõ:

- closed-loop gain = performance(full feedback loop) - performance(full no-feedback pipeline)

hoặc một biến thể có chuẩn hóa theo overhead.

Điểm cải tiến chính xác là:

- kiến trúc có metric riêng, không phụ thuộc hoàn toàn vào metric của từng module

## 5.4. Cải tiến lõi và cải tiến phụ

### Cải tiến lõi

- `Mandatory Feedback Semantics + Closed-Loop Gain`

### Cải tiến phụ

- standardized interface layer
- event-triggered re-grounding
- overhead analysis

## 5.5. Expected gain

Cải tiến này được kỳ vọng tạo ra:

- grounded state tốt hơn ở vòng sau
- action filtering tốt hơn khi risk tăng
- safety-aware decision quality tốt hơn so với pipeline không feedback
- architectural gain đo được

## 5.6. Vì sao đủ profile Q1

Contribution đủ mạnh ở mức Q1 vì:

- nó không chỉ tích hợp module
- nó formalize feedback như một contribution kiến trúc
- nó có metric riêng để đo giá trị của loop

Nếu làm đúng, đây là system-method paper chứ không phải system engineering paper.

## 5.7. Nếu không có cải tiến đó thì bài yếu ở đâu

Nếu không có feedback semantics và closed-loop gain metric, Paper 4 sẽ chỉ còn là:

- integration of three modules

và rất dễ bị reviewer xếp xuống mức engineering integration.

## 6. Bảng chốt cuối cùng

| Paper | Phương pháp cũ yếu ở đâu | Exact improvement | Lõi hay phụ | Nếu thiếu thì bài yếu ở đâu |
|---|---|---|---|---|
| Paper 1 | observability chỉ support, chưa invalidate | semantic-observability conflict validation | lõi | chỉ còn dual-memory variant |
| Paper 1 | retrieval chưa xét validity theo thời gian | temporal evidence retrieval | phụ quan trọng | dễ grounded theo stale evidence |
| Paper 2 | chưa tách strategy khỏi dispatch | strategy-dispatch decomposition | lõi | chỉ còn graph-MARL incremental |
| Paper 2 | context shift chưa chi phối policy hierarchy | context-adaptive representation | phụ quan trọng | hierarchy khó tạo gain rõ |
| Paper 3 | utility và safety bị scalar hóa | dual-head reward model | lõi | dễ thành reward engineering |
| Paper 3 | hard constraints chưa đi vào optimizer thật | Lagrangian constrained update | lõi | safety chỉ là penalty mềm |
| Paper 3 | preference khó khả thi | simulated preference protocol | phụ quan trọng | khó triển khai thật |
| Paper 4 | interaction chưa formalize | standardized interfaces | phụ quan trọng | integration mơ hồ |
| Paper 4 | feedback chưa có semantics | mandatory feedback protocol | lõi | closed-loop chỉ là sơ đồ |
| Paper 4 | thiếu metric kiến trúc | closed-loop gain metric | lõi | không chứng minh được architecture value |

## 7. Kết luận cuối

Để các paper có cửa Q1, bạn phải nhìn contribution theo đúng cách sau:

- `Paper 1`: điểm mới thật là conflict-validated operational grounding.
- `Paper 2`: điểm mới thật là strategic hierarchy trong graph-based dynamic coordination.
- `Paper 3`: điểm mới thật là utility-safety separation dưới constrained policy optimization.
- `Paper 4`: điểm mới thật là feedback semantics có closed-loop gain đo được.

Nếu giữ đúng các trục này, mỗi paper sẽ có một methodological core đủ sắc để không bị chìm thành tổ hợp kỹ thuật incremental.
