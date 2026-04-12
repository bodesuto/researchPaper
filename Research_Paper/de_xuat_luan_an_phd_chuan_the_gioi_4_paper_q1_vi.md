# Đề Xuất Luận Án PhD Chuẩn Quốc Tế Từ 4 Paper Q1

## 1. Tên luận án đề xuất

### Tên tiếng Việt

`CAMAS: Kiến Trúc Đa Tác Nhân Nhận Thức Closed-Loop Cho Grounded Perception, Adaptive Coordination Và Safe Alignment Trong Các Hệ Kỹ Thuật Phức Tạp`

### Tên tiếng Anh

`CAMAS: A Closed-Loop Cognitive Multi-Agent Architecture for Grounded Perception, Adaptive Coordination, and Safe Alignment in Complex Engineering Systems`

### Phiên bản ngắn gọn để dùng trong paper/proposal

`Closed-Loop Cognitive Multi-Agent Systems for Reliable Decision-Making in Complex Engineering Domains`

## 2. Luận điểm trung tâm của luận án

Luận án này xuất phát từ một nhận định cốt lõi:

`Các tác nhân AI trong hệ kỹ thuật phức tạp thường thất bại không phải vì thiếu một mô hình mạnh hơn, mà vì chúng ra quyết định từ các module rời rạc: nhận thức không được neo vào trạng thái vận hành thật, điều phối không thích ứng với nhiễu động động, và tối ưu policy không tách rõ utility khỏi ràng buộc an toàn.`

Từ đó, luận án đề xuất CAMAS như một kiến trúc nghiên cứu có 4 lớp đóng góp:

1. `Grounded Perception`: tạo trạng thái nhận thức có bằng chứng vận hành và kiểm tra mâu thuẫn.
2. `Adaptive Coordination`: dùng trạng thái đó để điều phối đa tác nhân dưới môi trường động.
3. `Safe Alignment`: tối ưu policy theo preference nhưng vẫn tôn trọng hard constraints.
4. `Closed-Loop Integration`: chứng minh feedback giữa ba lớp trên tạo lợi ích hệ thống đo được.

Luận điểm khoa học:

`Reliability in industrial multi-agent decision-making requires not merely stronger perception, coordination, or alignment modules in isolation, but a closed-loop architecture in which operational evidence, adaptive strategy, and safety constraints continuously inform one another through measurable feedback semantics.`

Dịch sát nghĩa:

`Độ tin cậy của hệ đa tác nhân công nghiệp không chỉ đến từ từng module nhận thức, điều phối hoặc căn chỉnh mạnh hơn, mà đến từ một kiến trúc closed-loop trong đó bằng chứng vận hành, chiến lược thích ứng và ràng buộc an toàn liên tục phản hồi cho nhau thông qua các ngữ nghĩa feedback đo được.`

## 2.1. Abstract đề xuất của toàn luận án

### Abstract tiếng Việt

Các hệ đa tác nhân ứng dụng trong bảo trì công nghiệp, điều độ sản xuất linh hoạt và điều hành năng lượng ngày càng đòi hỏi khả năng ra quyết định đáng tin cậy trong môi trường động, không chắc chắn và bị ràng buộc chặt bởi các điều kiện vận hành. Tuy nhiên, phần lớn các phương pháp hiện tại vẫn tối ưu từng thành phần riêng lẻ như nhận thức, điều phối hoặc an toàn chính sách, trong khi thiếu một khung kiến trúc thống nhất để liên kết các thành phần này thành một vòng phản hồi khép kín có thể đo lường. Luận án này đề xuất CAMAS, một kiến trúc đa tác nhân nhận thức closed-loop cho các hệ kỹ thuật phức tạp, nhằm giải quyết đồng thời bốn khoảng trống khoa học. Thứ nhất, luận án xây dựng cơ chế grounded perception dựa trên dual-memory reasoning có temporal evidence retrieval và semantic-observability conflict validation để giảm suy luận không được neo vào dữ liệu vận hành trong bảo trì công nghiệp. Thứ hai, luận án đề xuất cơ chế adaptive coordination phân cấp cho dynamic flexible job shop scheduling, tách rõ chiến lược điều độ tầng cao khỏi hành động dispatch tầng thấp để tăng khả năng phục hồi trước nhiễu động. Thứ ba, luận án phát triển một khung safe alignment cho smart grid control bằng cách tách utility preference khỏi safety feasibility thông qua dual-head reward modeling và constrained policy optimization. Thứ tư, luận án thiết kế giao thức closed-loop integration chuẩn hóa interface và feedback semantics giữa ba lớp trên, đồng thời đo lường closed-loop gain so với các pipeline một chiều. Về mặt khoa học, luận án đóng góp một cách nhìn mới về độ tin cậy trong hệ đa tác nhân công nghiệp: reliability không phải là thuộc tính của từng module riêng lẻ mà là thuộc tính xuất hiện từ tương tác có cấu trúc giữa operational grounding, adaptive coordination và safe alignment. Về mặt thực nghiệm, luận án xây dựng các benchmark, stress tests, ablation studies và giao thức đánh giá liên miền để chứng minh giá trị của từng đóng góp và của toàn bộ kiến trúc. Kết quả kỳ vọng là tạo ra một nền tảng nghiên cứu có thể dẫn tới bốn công bố Q1 độc lập nhưng tích lũy, đồng thời hình thành một luận án PhD có tính hệ thống, chiều sâu phương pháp luận và giá trị ứng dụng cao cho các hệ kỹ thuật phức tạp.

### Abstract tiếng Anh

Multi-agent systems deployed in industrial maintenance, flexible manufacturing, and smart grid operations increasingly require reliable decision-making under uncertainty, dynamic perturbations, and hard operational constraints. However, most existing approaches optimize perception, coordination, or safety in isolation, while lacking a unified architectural framework that connects these components through measurable closed-loop feedback. This dissertation proposes CAMAS, a closed-loop cognitive multi-agent architecture for complex engineering systems, to address four scientific gaps. First, it develops an operationally grounded perception framework based on dual-memory reasoning with temporal evidence retrieval and semantic-observability conflict validation to reduce unsupported maintenance reasoning. Second, it introduces a hierarchical adaptive coordination framework for dynamic flexible job shop scheduling, explicitly separating high-level scheduling strategy from low-level dispatch actions to improve robustness under perturbations. Third, it formulates a safe alignment framework for smart grid control by separating utility preference from safety feasibility through dual-head reward modeling and constrained policy optimization. Fourth, it designs a closed-loop integration protocol that standardizes interfaces and feedback semantics across the three layers and measures the architectural gain of closed-loop interaction over open-loop pipelines. Scientifically, the dissertation advances a new perspective on reliability in industrial multi-agent systems: reliability is not merely a property of stronger individual modules, but an emergent property of structured interaction among operational grounding, adaptive coordination, and safe alignment. Empirically, the dissertation contributes benchmarks, stress tests, ablation protocols, and cross-domain evaluation settings to validate each contribution and the integrated architecture. The expected outcome is a coherent PhD thesis capable of yielding four Q1-level publications while establishing a rigorous research foundation for reliable AI-driven decision-making in complex engineering domains.

## 2.2. Contribution bullets ngắn gọn

### Đóng góp tổng quát của luận án

- Đề xuất một khung kiến trúc closed-loop cho hệ đa tác nhân nhận thức trong các miền kỹ thuật phức tạp.
- Tái định nghĩa reliability như một thuộc tính xuất hiện từ tương tác giữa grounding, coordination và alignment.
- Chuẩn hóa interface, feedback semantics và closed-loop gain để đo lợi ích kiến trúc ở cấp hệ thống.
- Xây dựng một chuỗi 4 đóng góp độc lập nhưng tích lũy, đủ mạnh để hình thành một luận án PhD có cấu trúc rõ và khả năng công bố quốc tế cao.

### Đóng góp kỹ thuật theo từng paper

- `Paper 1`: conflict-validated temporal grounding cho industrial maintenance agents.
- `Paper 2`: strategy-dispatch decomposed hierarchical coordination cho dynamic FJSP.
- `Paper 3`: utility-feasibility separated preference-guided optimization cho safe smart grid control.
- `Paper 4`: event-triggered closed-loop integration protocol với metric closed-loop gain.

## 3. Vì sao đây là luận án PhD, không chỉ là 4 bài rời rạc

Một luận án PhD chuẩn quốc tế cần có:

- một vấn đề trung tâm có ý nghĩa khoa học
- một gap xuyên suốt literature
- một chuỗi đóng góp tích lũy
- một phương pháp luận nhất quán
- bằng chứng thực nghiệm đủ mạnh
- khả năng khái quát hóa có kiểm soát

CAMAS đạt cấu trúc đó nếu 4 paper được viết theo quan hệ sau:

| Thành phần | Câu hỏi khoa học | Paper |
|---|---|---|
| Perception | Làm sao biết trạng thái mà agent dùng để ra quyết định có thật sự được neo vào vận hành hiện tại? | Paper 1 |
| Coordination | Làm sao dùng trạng thái đó để điều phối nhiều tác nhân khi môi trường thay đổi? | Paper 2 |
| Alignment | Làm sao tối ưu policy mà không vi phạm ràng buộc vật lý/an toàn? | Paper 3 |
| Integration | Khi ba lớp trên phản hồi cho nhau, hệ có tốt hơn pipeline một chiều không? | Paper 4 |

Như vậy, 4 paper không phải 4 nhánh rời rạc. Chúng trả lời 4 câu hỏi liên tiếp của cùng một vấn đề:

`Làm thế nào để xây dựng một hệ đa tác nhân công nghiệp có khả năng ra quyết định đáng tin cậy trong môi trường động, không chắc chắn và bị ràng buộc?`

## 4. Nỗi đau thực tế và khoảng trống khoa học

## 4.1. Nỗi đau 1: Agent trả lời hợp lý nhưng sai với trạng thái vận hành thật

Trong bảo trì công nghiệp, lỗi nguy hiểm không phải là câu trả lời vô nghĩa. Lỗi nguy hiểm hơn là:

- khuyến nghị nghe hợp lý
- khớp với tri thức nền
- nhưng không được log, trace hoặc sensor hiện tại hỗ trợ

Ví dụ:

- quy trình bảo trì chuẩn nói một hành động là hợp lệ
- nhưng trạng thái thiết bị hiện tại đã thay đổi
- agent vẫn khuyến nghị theo tri thức cũ

Đây là dạng `operational hallucination`.

Gap:

- RAG/KG-RAG cải thiện factual grounding
- dual-memory cải thiện evidence support
- nhưng chưa coi `temporal validity` và `semantic-observability conflict` là tín hiệu xác thực bắt buộc

Paper 1 giải gap này.

## 4.2. Nỗi đau 2: Scheduler tốt trong benchmark tĩnh nhưng yếu khi môi trường nhiễu động

Trong sản xuất linh hoạt, bài toán không chỉ là tìm lịch tốt trên dữ liệu tĩnh. Hệ thực tế phải phản ứng khi:

- máy hỏng
- đơn hàng gấp xuất hiện
- deadline thay đổi
- thời gian xử lý dao động

Nhiều phương pháp graph MARL mạnh ở representation nhưng vẫn thiếu một câu trả lời rõ:

`Khi nào hệ cần đổi chiến lược, và khi nào chỉ cần đổi dispatch cục bộ?`

Gap:

- graph-attention MARL biểu diễn tốt quan hệ job-operation-machine
- nhưng chưa tách rõ tầng chiến lược và tầng thực thi dưới perturbation động

Paper 2 giải gap này.

## 4.3. Nỗi đau 3: Policy tối ưu utility nhưng không thể triển khai vì vi phạm constraints

Trong smart grid và cyber-physical systems, một policy có return cao nhưng vi phạm safety constraints là policy không dùng được.

Vấn đề không phải chỉ là thêm penalty. Vấn đề là:

- utility preference và safety feasibility là hai loại tín hiệu khác bản chất
- nếu trộn chúng vào một reward scalar, hệ có thể học trade-off sai

Gap:

- safe RL xử lý feasibility nhưng thường thiếu preference-guided utility modeling
- preference-based optimization xử lý utility nhưng thường không bảo đảm hard constraints

Paper 3 giải gap này.

## 4.4. Nỗi đau 4: Module mạnh riêng lẻ nhưng hệ tổng thể vẫn yếu

Một hệ công nghiệp có thể có:

- module perception tốt
- module coordination tốt
- module safety tốt

Nhưng nếu ba module này không phản hồi cho nhau, hệ vẫn có thể thất bại.

Ví dụ:

- perception phát hiện evidence conflict nhưng coordination không nhận được uncertainty
- coordination gần vi phạm constraint nhưng perception không re-ground
- alignment thấy risk tăng nhưng không truyền risk prior ngược lại tầng quyết định

Gap:

- nhiều architecture hiện nay là one-way pipeline
- thiếu interface chuẩn
- thiếu feedback semantics
- thiếu metric đo closed-loop gain

Paper 4 giải gap này.

## 5. Khung tư duy sáng tạo dùng để thiết kế luận án

Phần này dùng trực tiếp hai skill:

- `creative-thinking-for-research`
- `brainstorming-research-ideas`

Mục tiêu là tránh biến luận án thành “ghép nhiều kỹ thuật”.

## 5.1. Problem-first thinking

Luận án không bắt đầu từ kỹ thuật như graph, attention, memory, RLHF hay MARL.  
Luận án bắt đầu từ failure modes:

1. Agent nhận thức sai vì thiếu operational grounding.
2. Agent điều phối yếu vì thiếu strategy adaptation.
3. Agent tối ưu nguy hiểm vì không tách utility và safety.
4. Hệ tổng thể yếu vì thiếu feedback loop.

Đây là lý do CAMAS có tính PhD: nó xử lý một lớp thất bại có hệ thống.

## 5.2. Tension and contradiction hunting

Mỗi paper giải một tension rõ:

| Paper | Tension |
|---|---|
| Paper 1 | Semantic plausibility ↔ Operational validity |
| Paper 2 | Global scheduling strategy ↔ Local dispatch responsiveness |
| Paper 3 | Economic utility ↔ Safety feasibility |
| Paper 4 | Modular independence ↔ Closed-loop system reliability |

Một paper Q1 mạnh phải cho thấy:

- tension này là thật
- prior work xử lý chưa đủ
- method của bạn giải tension bằng cơ chế cụ thể

## 5.3. Problem reformulation

Luận án reformulate 4 vấn đề:

- hallucination không chỉ là factual error, mà là `operationally unsupported reasoning`
- scheduling không chỉ là action selection, mà là `strategy-dispatch decomposition`
- alignment không phải RLHF, mà là `preference-guided constrained control`
- integration không phải ghép module, mà là `measurable feedback semantics`

Đây là điểm giúp luận án có chiều sâu hơn extension thông thường.

## 5.4. Constraint manipulation

Các constraint không bị xem là phiền phức phụ, mà là một phần của contribution:

- temporal validity trong Paper 1
- perturbation trong Paper 2
- hard safety constraints trong Paper 3
- feedback triggers trong Paper 4

Luận án biến constraints thành nguồn novelty.

## 5.5. Decomposition and recomposition

CAMAS decomposes reliable decision-making thành 3 chức năng:

- perception
- coordination
- alignment

Sau đó recomposes chúng bằng:

- interface
- feedback semantics
- closed-loop gain

Đây là logic kiến trúc của toàn luận án.

## 6. Research questions

## 6.1. Câu hỏi nghiên cứu tổng quát

`How can cognitive multi-agent systems make reliable decisions in complex engineering domains when their observations are uncertain, environments are dynamic, and policies must satisfy hard operational constraints?`

Tiếng Việt:

`Làm thế nào để các hệ đa tác nhân nhận thức ra quyết định đáng tin cậy trong các miền kỹ thuật phức tạp khi quan sát không chắc chắn, môi trường biến đổi động, và policy phải thỏa mãn các ràng buộc vận hành cứng?`

## 6.2. Câu hỏi nghiên cứu cụ thể

### RQ1

`How can industrial agents distinguish semantically plausible reasoning from operationally grounded reasoning?`

Paper 1 trả lời bằng:

- temporal evidence retrieval
- semantic-observability conflict validation
- grounded state scoring

### RQ2

`How can multi-agent schedulers separate strategic adaptation from local dispatch under dynamic perturbations?`

Paper 2 trả lời bằng:

- strategy-dispatch hierarchy
- heterogeneous graph state
- dynamic FJSP robustness protocol

### RQ3

`How can preference-guided policy optimization improve utility while preserving feasibility under hard constraints?`

Paper 3 trả lời bằng:

- dual-head utility/safety modeling
- constrained policy update
- utility-safety frontier evaluation

### RQ4

`Does closed-loop feedback among perception, coordination, and alignment produce measurable system-level gains over open-loop pipelines?`

Paper 4 trả lời bằng:

- standardized interfaces
- event-triggered feedback
- closed-loop gain metric

## 7. Tổng quan 4 paper trong luận án

| Paper | Tên rút gọn | Đóng góp trung tâm | Domain | Metric chính |
|---|---|---|---|---|
| Paper 1 | Grounded Perception | Conflict-validated temporal grounding | Industrial maintenance | Hallucination rate |
| Paper 2 | Adaptive Coordination | Strategy-dispatch decomposition | Dynamic FJSP | Makespan / tardiness |
| Paper 3 | Safe Alignment | Utility-feasibility separation | Smart grid | Safety violation rate |
| Paper 4 | Closed-Loop Integration | Event-triggered closed-loop gain | Cross-domain slices | Closed-loop gain |

## 8. Paper 1 chi tiết

## 8.1. Tên bài

`Observability-Grounded Conflict-Validated Dual-Memory Reasoning for Industrial Maintenance Agents`

## 8.2. Problem

Industrial maintenance agents often generate recommendations that are semantically plausible but operationally unsupported because they rely on static knowledge or retrieved documents without validating them against current observability evidence.

## 8.3. Gap

Existing RAG, KG-RAG and dual-memory systems improve grounding, but they do not make temporal validity and semantic-observability conflicts first-class validation signals.

## 8.4. Novelty statement

`We propose conflict-validated temporal grounding, a dual-memory reasoning framework that treats observability evidence not only as support but also as a validator capable of invalidating semantically plausible maintenance recommendations.`

## 8.5. Method

Paper 1 gồm 4 module:

1. `Semantic memory`
   - equipment taxonomy
   - maintenance procedures
   - component relations
   - operational rules

2. `Observability memory`
   - logs
   - traces
   - sensor states
   - execution history
   - timestamps
   - source reliability

3. `Temporal evidence retrieval`
   - semantic relevance
   - entity consistency
   - recency
   - validity window
   - source reliability

4. `Conflict validation`
   - semantic claim extraction
   - observability evidence matching
   - conflict relation detection
   - inconsistency scoring
   - uncertainty scoring

## 8.6. Hypotheses

### H1.1

Temporal evidence retrieval reduces stale-evidence hallucinations compared with semantic-only retrieval.

### H1.2

Conflict validation reduces unsupported recommendations compared with dual-memory retrieval without conflict checking.

### H1.3

Inconsistency and uncertainty scores correlate with real maintenance reasoning errors.

## 8.7. Baselines

- vector RAG
- KG-RAG
- semantic-only KG
- dual-memory without temporal retrieval
- dual-memory without conflict validation
- maintenance reasoning agent without observability grounding

## 8.8. Metrics

- hallucination rate based on evidence trace
- evidence grounding score
- factual consistency
- inconsistency detection accuracy
- maintenance task success rate

## 8.9. Stress tests

- missing logs
- noisy logs
- stale evidence
- conflicting evidence
- wrong entity mapping

## 8.10. Expected contribution to thesis

Paper 1 tạo output chuẩn:

```text
grounded_state = {
  evidence_set,
  temporal_validity,
  inconsistency_score,
  uncertainty_score,
  supported_claims,
  unsupported_claims
}
```

Output này là input tự nhiên cho Paper 4.

## 9. Paper 2 chi tiết

## 9.1. Tên bài

`Strategy-Dispatch Decomposed Hierarchical Graph Coordination for Dynamic Flexible Job Shop Scheduling`

## 9.2. Problem

Dynamic FJSP requires agents to adapt scheduling strategy and dispatch actions under disruptions, but flat MARL and graph-only methods often entangle strategic adaptation with local action selection.

## 9.3. Gap

Existing graph-attention MARL methods improve representation, but do not explicitly separate high-level scheduling strategy from low-level dispatch execution under dynamic perturbations.

## 9.4. Novelty statement

`We propose a strategy-dispatch decomposed coordination framework that uses hierarchical graph-based multi-agent policies to separate strategic adaptation from local dispatch decisions in dynamic FJSP.`

## 9.5. Method

Paper 2 gồm 4 phần:

1. `Heterogeneous graph state`
   - job nodes
   - operation nodes
   - machine nodes
   - resource constraint nodes
   - dynamic perturbation attributes

2. `Strategy-level master policy`
   - chooses scheduling mode
   - sets subgoals
   - adjusts priority regime
   - reacts to global perturbation

3. `Dispatch-level worker policies`
   - assign machines
   - sequence operations
   - update local decisions

4. `Dynamic robustness protocol`
   - machine breakdown
   - urgent job arrival
   - due-date shift
   - processing-time uncertainty

## 9.6. Hypotheses

### H2.1

Strategy-dispatch decomposition improves robustness under perturbation compared with flat graph MARL.

### H2.2

Hierarchy contributes independent gains beyond graph representation.

### H2.3

Context-adaptive graph state improves recovery speed after dynamic disruptions.

## 9.7. Baselines

- dispatch heuristics
- single-agent RL
- flat MARL
- MAMHSAN-like graph-attention MARL
- hierarchy without graph
- graph without hierarchy
- graph + attention without context adaptation

## 9.8. Metrics

- makespan
- total tardiness
- machine utilization
- rescheduling cost
- convergence stability
- perturbation recovery time

## 9.9. Stress tests

- machine breakdown
- urgent job arrival
- due-date shift
- dynamic processing time
- partial observability

## 9.10. Expected contribution to thesis

Paper 2 tạo output chuẩn:

```text
coordination_state = {
  strategy_signal,
  dispatch_actions,
  context_embedding,
  perturbation_status,
  scheduling_uncertainty,
  recovery_cost
}
```

Output này liên kết với Paper 4 qua feedback loop.

## 10. Paper 3 chi tiết

## 10.1. Tên bài

`Constraint-Aware Preference-Guided Optimization for Safe Smart Grid Control`

## 10.2. Problem

In smart grid control, policies that optimize economic utility may be infeasible or unsafe if they violate hard physical constraints, while preference-based optimization alone does not guarantee feasibility.

## 10.3. Gap

Safe RL handles constraints but often lacks preference-guided utility modeling; preference optimization models utility but usually does not enforce hard feasibility constraints.

## 10.4. Novelty statement

`We propose a constraint-aware preference-guided optimization framework that separates utility preference from safety feasibility through dual-head reward modeling and constrained policy updates.`

## 10.5. Method

Paper 3 gồm 4 phần:

1. `Utility preference head`
   - economic objective
   - cost/profit trade-off
   - operator preference
   - expert ranking

2. `Safety feasibility head`
   - line capacity
   - voltage limits
   - load balance
   - reserve constraints
   - violation prediction

3. `Preference data protocol`
   - rule-based expert ranking
   - simulator-generated preference pairs
   - small expert/human validation subset

4. `Constrained policy update`
   - Lagrangian update
   - safety budget
   - utility-safety frontier

## 10.6. Hypotheses

### H3.1

Separating utility and feasibility improves utility-safety trade-off compared with scalar penalty rewards.

### H3.2

Preference-guided utility modeling improves operating cost without increasing safety violations.

### H3.3

Constrained updates reduce violation rate more reliably than preference-only optimization.

## 10.7. Baselines

- constrained RL
- safe RL
- penalty-based reward shaping
- preference-only optimization
- safety-only optimization
- dual-head without constrained update

## 10.8. Metrics

- safety violation rate
- feasibility rate
- operating cost
- profit/return
- load shedding
- utility-safety frontier
- robustness under uncertainty

## 10.9. Stress tests

- load surge
- renewable fluctuation
- line outage
- demand uncertainty
- adversarial demand pattern

## 10.10. Expected contribution to thesis

Paper 3 tạo output chuẩn:

```text
alignment_state = {
  utility_score,
  safety_score,
  violation_risk,
  constraint_margin,
  policy_update_signal,
  risk_aware_prior
}
```

Output này là tín hiệu feedback chính cho Paper 4.

## 11. Paper 4 chi tiết

## 11.1. Tên bài

`Event-Triggered Closed-Loop Integration for Cognitive Multi-Agent Systems in Complex Engineering Domains`

## 11.2. Problem

Perception, coordination and alignment modules are often evaluated independently or connected as one-way pipelines, leaving unclear whether feedback among them produces measurable system-level reliability gains.

## 11.3. Gap

Existing agent architectures lack standardized interfaces, feedback semantics and controlled evaluation protocols for measuring closed-loop benefits across perception, coordination and alignment layers.

## 11.4. Novelty statement

`We propose an event-triggered closed-loop integration protocol that standardizes interfaces among grounded perception, adaptive coordination and safe alignment, and measures system-level closed-loop gain over open-loop pipelines.`

## 11.5. Method

Paper 4 gồm 4 phần:

1. `Interface specification`
   - grounded_state
   - coordination_state
   - alignment_state
   - shared uncertainty/risk schema

2. `Feedback semantics`
   - perception-to-coordination: uncertainty-aware state
   - coordination-to-alignment: strategy and risk exposure
   - alignment-to-perception: risk-aware re-grounding request
   - alignment-to-coordination: constraint-aware policy prior

3. `Event-triggered feedback`
   - high uncertainty
   - evidence conflict
   - near-constraint violation
   - perturbation spike
   - degraded performance

4. `Closed-loop gain measurement`
   - open-loop vs closed-loop
   - pairwise integration vs full integration
   - fixed-interval feedback vs event-triggered feedback
   - overhead-aware gain

## 11.6. Hypotheses

### H4.1

Closed-loop feedback improves system robustness compared with open-loop pipelines.

### H4.2

Event-triggered feedback achieves better gain-overhead trade-off than fixed-interval feedback.

### H4.3

Uncertainty, conflict and near-violation triggers explain most of the closed-loop gains.

## 11.7. Baselines

- open-loop pipeline
- pairwise integration
- full system without feedback
- fixed-interval feedback
- random feedback trigger
- feedback without uncertainty propagation

## 11.8. Metrics

- closed-loop gain
- task success rate
- robustness
- safety violation
- recovery time
- latency overhead
- compute overhead

## 11.9. Closed-loop gain definition

Một định nghĩa có thể dùng:

```text
CLG = ((P_closed - P_open) / |P_open|)
      - lambda_latency * Overhead_latency
      - lambda_compute * Overhead_compute
```

Trong đó:

- `P_closed`: performance tổng hợp của hệ closed-loop
- `P_open`: performance của pipeline open-loop
- `Overhead_latency`: overhead thời gian
- `Overhead_compute`: overhead tính toán
- `lambda_latency`, `lambda_compute`: trọng số phạt overhead

Nếu domain cần multi-objective:

```text
P = w_task * TaskSuccess
    + w_robust * Robustness
    - w_safety * SafetyViolation
    - w_cost * OperatingCost
```

Điểm quan trọng:

- công thức phải được chốt trước experiment chính
- không được chọn trọng số sau khi thấy kết quả

## 11.10. Expected contribution to thesis

Paper 4 chứng minh luận điểm chính của luận án:

`Reliable industrial agents require closed-loop interaction between grounded perception, adaptive coordination and safe alignment, not merely independent improvements to each module.`

## 12. Logic liên kết giữa 4 paper

## 12.1. Luồng thông tin chính

```text
Paper 1:
Raw operational evidence
  -> grounded_state
  -> uncertainty/conflict scores

Paper 2:
grounded/contextual state
  -> strategy signal
  -> dispatch actions
  -> perturbation response

Paper 3:
strategy/action trajectory
  -> utility/safety evaluation
  -> risk-aware policy update
  -> constraint-aware prior

Paper 4:
uncertainty + conflict + risk + perturbation
  -> event-triggered feedback
  -> closed-loop gain
```

## 12.2. Conceptual dependency

| From | To | What transfers |
|---|---|---|
| Paper 1 | Paper 4 | grounded_state, uncertainty, conflict |
| Paper 2 | Paper 4 | strategy signal, context embedding, perturbation status |
| Paper 3 | Paper 4 | safety risk, constraint margin, policy prior |
| Paper 4 | Thesis | evidence that closed-loop architecture matters |

## 12.3. Không phụ thuộc quá mức

Mỗi paper vẫn phải độc lập:

- Paper 1 có thể nộp riêng ở track AI/maintenance/knowledge systems
- Paper 2 có thể nộp riêng ở scheduling/RL/optimization track
- Paper 3 có thể nộp riêng ở energy AI/safe RL/control track
- Paper 4 có thể nộp riêng ở AI systems/multi-agent systems track

Điểm tích hợp chỉ được dùng để tạo luận án, không làm từng paper mất độc lập.

## 13. Contribution map của toàn luận án

## 13.1. Methodological contributions

1. Conflict-validated temporal grounding.
2. Strategy-dispatch decomposed coordination.
3. Utility-feasibility separated preference optimization.
4. Event-triggered closed-loop integration.

## 13.2. Empirical contributions

1. Maintenance hallucination benchmark with operational evidence.
2. Dynamic FJSP perturbation protocol.
3. Smart grid utility-safety frontier evaluation.
4. Open-loop vs closed-loop architecture benchmark.

## 13.3. Conceptual contributions

1. Reframing hallucination as operational unsupportedness.
2. Reframing scheduling adaptation as strategy-dispatch decomposition.
3. Reframing alignment as utility-feasibility separation.
4. Reframing integration as measurable feedback semantics.

## 14. Evaluation plan tổng thể

## 14.1. Evaluation philosophy

Luận án không chỉ hỏi:

- method có score cao hơn không?

Mà hỏi:

- method sửa failure mode nào?
- failure mode đó có quan trọng không?
- thành phần novelty có thật sự tạo gain không?
- gain có bền dưới stress test không?
- overhead có chấp nhận được không?

## 14.2. Evaluation matrix

| Paper | Main comparison | Ablation | Stress test | Error analysis |
|---|---|---|---|---|
| Paper 1 | RAG/KG-RAG/dual-memory | no temporal, no conflict | stale/noisy/conflicting evidence | unsupported recommendation types |
| Paper 2 | MAMHSAN-like/flat MARL | no hierarchy, no graph, no context | breakdown/urgent/due shift | failure to recover after perturbation |
| Paper 3 | constrained RL/safe RL | no utility head, no safety head, no Lagrangian | load/renewable/line uncertainty | violation source analysis |
| Paper 4 | open-loop/no-feedback | no trigger, no uncertainty, fixed feedback | conflict/risk/perturbation spikes | feedback failure categories |

## 15. Tiêu chuẩn “đủ Q1” cho từng paper

## 15.1. Paper 1 đủ Q1 khi

- hallucination rate được operationalize rõ
- conflict validation tạo gain riêng
- temporal validity tạo gain riêng
- stress test chứng minh robust
- error analysis có ý nghĩa vận hành

## 15.2. Paper 2 đủ Q1 khi

- hierarchy tạo gain riêng
- dynamic FJSP protocol đủ nặng
- MAMHSAN-like baseline được so sánh công bằng
- strategy-dispatch decomposition giải thích được kết quả

## 15.3. Paper 3 đủ Q1 khi

- utility-safety frontier tốt hơn constrained RL
- violation giảm mà utility không sụp
- preference data protocol đáng tin
- hard constraints không bị biến thành soft penalty đơn giản

## 15.4. Paper 4 đủ Q1 khi

- closed-loop gain rõ
- feedback trigger có ablation riêng
- overhead được tính thật
- architecture không claim quá rộng

## 16. Cấu trúc luận án đề xuất

## Chapter 1: Introduction

- industrial AI decision-making problem
- reliability gap
- why modular AI pipelines fail
- CAMAS overview
- research questions
- contributions

## Chapter 2: Background and Literature Review

- cognitive multi-agent systems
- RAG/KG grounding and hallucination
- graph MARL and scheduling
- safe RL and preference optimization
- AI systems integration and feedback architectures

## Chapter 3: Operationally Grounded Perception

Dựa trên Paper 1.

Nội dung:

- operational hallucination
- dual-memory grounding
- temporal retrieval
- conflict validation
- maintenance evaluation

## Chapter 4: Adaptive Multi-Agent Coordination

Dựa trên Paper 2.

Nội dung:

- dynamic FJSP
- graph state representation
- strategy-dispatch hierarchy
- perturbation robustness

## Chapter 5: Constraint-Aware Safe Alignment

Dựa trên Paper 3.

Nội dung:

- utility vs safety tension
- preference-guided control
- dual-head reward modeling
- constrained policy update
- smart grid evaluation

## Chapter 6: Closed-Loop CAMAS Integration

Dựa trên Paper 4.

Nội dung:

- interface specification
- feedback semantics
- event-triggered re-grounding
- risk-aware feedback
- closed-loop gain

## Chapter 7: Cross-Paper Synthesis

Chương này rất quan trọng để luận án không giống tuyển tập paper.

Nội dung:

- what each layer contributes to reliability
- when closed-loop helps
- when closed-loop does not help
- limits of cross-domain generalization
- design principles for future industrial agents

## Chapter 8: Conclusion and Future Work

- summary
- limitations
- deployment pathway
- future research

## 16.1. Chapter summary cho hội đồng

### Chapter 1: Introduction

Chương này xác lập bài toán trung tâm của luận án: vì sao các hệ AI công nghiệp hiện nay vẫn thiếu độ tin cậy dù từng module riêng lẻ ngày càng mạnh. Chương này trình bày bối cảnh ứng dụng, nỗi đau thực tế, research questions, giả thuyết tổng quát, đóng góp chính và cấu trúc của toàn luận án.

### Chapter 2: Background and Literature Review

Chương này tổng hợp nền tảng học thuật liên quan đến grounded reasoning, graph-based multi-agent coordination, safe/constrained optimization, và integration trong agent architectures. Mục tiêu là chỉ ra rằng literature hiện tại mạnh ở các module riêng lẻ nhưng còn thiếu một lý thuyết và giao thức đo lường closed-loop reliability.

### Chapter 3: Operationally Grounded Perception

Chương này phát triển nền tảng cho nhận thức đáng tin cậy trong công nghiệp. Trọng tâm là temporal evidence retrieval và semantic-observability conflict validation. Chương này chứng minh rằng observability không chỉ là evidence hỗ trợ, mà còn là cơ chế phủ định các suy luận ngữ nghĩa có vẻ hợp lý nhưng sai với trạng thái vận hành thật.

### Chapter 4: Adaptive Multi-Agent Coordination

Chương này nghiên cứu điều phối đa tác nhân trong dynamic FJSP bằng chiến lược phân cấp. Đóng góp chính là tách quyết định chiến lược điều độ tầng cao khỏi dispatch tầng thấp, từ đó nâng khả năng phục hồi trước breakdown, urgent jobs và due-date shift. Chương này trả lời cách agent thích ứng khi môi trường thay đổi liên tục.

### Chapter 5: Constraint-Aware Safe Alignment

Chương này giải quyết tension giữa utility và safety trong smart grid control. Đóng góp trung tâm là tách utility preference khỏi safety feasibility, thay vì trộn chúng vào một reward scalar. Chương này cung cấp nền tảng để tối ưu policy vừa hiệu quả vừa triển khai được trong miền cyber-physical có hard constraints.

### Chapter 6: Closed-Loop CAMAS Integration

Chương này tổng hợp ba lớp trước thành một kiến trúc có phản hồi. Trọng tâm không phải là ghép module, mà là chuẩn hóa interface, feedback semantics và định nghĩa closed-loop gain. Chương này kiểm chứng xem phản hồi liên tầng có thực sự tạo ra lợi ích hệ thống hay không.

### Chapter 7: Cross-Paper Synthesis

Chương này là phần biến luận án từ “4 paper tốt” thành “một đóng góp PhD hoàn chỉnh”. Nó tổng hợp các nguyên lý thiết kế chung, chỉ ra khi nào closed-loop có ích, khi nào không có ích, và rút ra các design principles cho reliable multi-agent systems trong các hệ kỹ thuật phức tạp.

### Chapter 8: Conclusion and Future Work

Chương cuối cùng tóm lược các đóng góp, nhấn mạnh giới hạn của luận án, đề xuất lộ trình triển khai thực tế và chỉ ra các hướng nghiên cứu mở sau tiến sĩ.

## 17. Lộ trình 4 năm

## Năm 1: Paper 1 và nền thực nghiệm

Mục tiêu:

- hoàn thành Paper 1
- xây evidence-grounding benchmark
- định nghĩa operational hallucination
- tạo reusable code cho evidence, logging, evaluation

Kết quả kỳ vọng:

- 1 manuscript Q1-ready
- benchmark/protocol có thể dùng lại cho Paper 4

## Năm 2: Paper 2

Mục tiêu:

- hoàn thành dynamic FJSP framework
- dựng MAMHSAN-like baseline
- chứng minh hierarchy tạo gain

Kết quả kỳ vọng:

- 1 manuscript Q1-ready
- coordination interface cho Paper 4

## Năm 3: Paper 3

Mục tiêu:

- hoàn thành safe smart-grid control formulation
- dựng constrained RL baseline
- chứng minh utility-safety frontier

Kết quả kỳ vọng:

- 1 manuscript Q1-ready
- safety/risk interface cho Paper 4

## Năm 4: Paper 4 và luận án

Mục tiêu:

- hoàn thành closed-loop integration
- viết synthesis chapter
- đồng bộ terminology
- chuẩn bị defense

Kết quả kỳ vọng:

- 1 manuscript Q1-ready
- full dissertation

## 17.1. Timeline dạng bảng

| Giai đoạn | Mốc thời gian | Mục tiêu chính | Deliverables |
|---|---|---|---|
| Giai đoạn 1 | Tháng 1-6 | Khóa problem framing, literature, benchmark cho Paper 1 | literature review, metric definition, benchmark draft |
| Giai đoạn 2 | Tháng 7-12 | Hoàn thiện Paper 1 và submission vòng 1 | Paper 1 manuscript, codebase perception, evaluation protocol |
| Giai đoạn 3 | Tháng 13-18 | Xây framework và baseline cho Paper 2 | dynamic FJSP simulator, baseline runs, hierarchy protocol |
| Giai đoạn 4 | Tháng 19-24 | Hoàn thiện Paper 2 và submission vòng 1 | Paper 2 manuscript, perturbation benchmark, ablation suite |
| Giai đoạn 5 | Tháng 25-30 | Reformulate và triển khai Paper 3 | smart grid setup, constrained RL baselines, preference protocol |
| Giai đoạn 6 | Tháng 31-36 | Hoàn thiện Paper 3 và submission vòng 1 | Paper 3 manuscript, utility-safety frontier study |
| Giai đoạn 7 | Tháng 37-42 | Chuẩn hóa interface và triển khai Paper 4 | interface specification, feedback engine, CLG metric |
| Giai đoạn 8 | Tháng 43-48 | Hoàn thiện Paper 4, synthesis và luận án | Paper 4 manuscript, thesis chapters, defense-ready dissertation |

## 17.2. Timeline dạng Gantt rút gọn

```text
Năm 1:
  Q1-Q2  Literature + framing + benchmark Paper 1
  Q3-Q4  Experiments + viết + nộp Paper 1

Năm 2:
  Q1-Q2  Baseline + simulator + framework Paper 2
  Q3-Q4  Experiments + viết + nộp Paper 2

Năm 3:
  Q1-Q2  Reformulation + setup Paper 3
  Q3-Q4  Experiments + viết + nộp Paper 3

Năm 4:
  Q1-Q2  Interface + feedback protocol + Paper 4
  Q3     Viết synthesis chapters
  Q4     Hoàn tất luận án và defense
```

## 17.3. Expected publications table

| Publication ID | Working title | Loại đóng góp | Mức ưu tiên | Thời điểm kỳ vọng |
|---|---|---|---:|---|
| P1 | Observability-Grounded Conflict-Validated Dual-Memory Reasoning for Industrial Maintenance Agents | Grounded perception | 1 | Cuối năm 1 / đầu năm 2 |
| P2 | Strategy-Dispatch Decomposed Hierarchical Graph Coordination for Dynamic Flexible Job Shop Scheduling | Adaptive coordination | 2 | Cuối năm 2 |
| P3 | Constraint-Aware Preference-Guided Optimization for Safe Smart Grid Control | Safe alignment | 3 | Cuối năm 3 |
| P4 | Event-Triggered Closed-Loop Integration for Cognitive Multi-Agent Systems in Complex Engineering Domains | Closed-loop integration | 4 | Cuối năm 4 |
| Optional Workshop / Survey | Reliability Principles for Cognitive Multi-Agent Systems in Complex Engineering Domains | Survey / positioning | Phụ | Trong 4 năm nếu cần |

## 18. Rủi ro và cách giảm rủi ro

## 18.1. Rủi ro Paper 1

Rủi ro:

- conflict validation bị xem như heuristic reranking

Cách giảm:

- formalize conflict types
- chứng minh conflict ảnh hưởng trực tiếp đến decision acceptance
- error analysis theo unsupported, stale, contradicted recommendation

## 18.2. Rủi ro Paper 2

Rủi ro:

- hierarchy không tạo gain đủ rõ

Cách giảm:

- thiết kế perturbation nặng
- chọn metric recovery time
- chứng minh flat MARL phản ứng chậm hơn

## 18.3. Rủi ro Paper 3

Rủi ro:

- preference data bị reviewer nghi ngờ

Cách giảm:

- dùng simulator rule-based expert
- thêm expert/human validation subset
- không claim human-scale RLHF

## 18.4. Rủi ro Paper 4

Rủi ro:

- integration bị xem là engineering demo

Cách giảm:

- đóng góp chính là protocol + metric + feedback semantics
- ablation feedback rõ
- overhead analysis rõ

## 18.5. Limitations và fallback plans cho hội đồng

### Limitation 1: Cross-domain breadth có thể bị xem là quá rộng

Vấn đề:

- maintenance, FJSP và smart grid là ba domain khác nhau
- hội đồng có thể hỏi liệu luận án có bị phân tán hay không

Fallback plan:

- nhấn mạnh ba domain này chỉ là `domain slices` đại diện cho ba chức năng khác nhau
- giữ đóng góp chính ở mức mechanism và interface, không claim universal generalization
- nếu cần, thu hẹp narrative chính về `complex engineering systems with operational evidence, dynamic perturbations, and hard constraints`

### Limitation 2: Paper 3 là bài có rủi ro cao nhất

Vấn đề:

- preference data trong smart grid khó thuyết phục nếu không thiết kế tốt

Fallback plan:

- dùng rule-based expert preferences + human validation subset
- nếu preference data yếu, pivot contribution sang `constraint-aware dual-head safe optimization` và giảm độ phụ thuộc vào preference claim
- giữ utility-safety frontier là evaluation trung tâm

### Limitation 3: Paper 4 có thể bị xem là engineering integration

Vấn đề:

- nếu không có metric và protocol đủ chặt, integration dễ bị đánh giá là demo

Fallback plan:

- viết Paper 4 như một paper về `protocol + measurement`
- chốt closed-loop gain trước thí nghiệm
- nếu cross-domain full integration quá nặng, dùng `domain-slice integration evaluation` thay vì một full-stack system duy nhất

### Limitation 4: Khả năng tái lập baseline mạnh

Vấn đề:

- một số baseline SOTA có thể khó reproduce hoặc code không ổn định

Fallback plan:

- chọn baseline có code public, được cộng đồng dùng rộng
- công khai tiêu chí chọn baseline ngay trong proposal
- nếu baseline không tái lập đúng, dùng 2-3 baseline mạnh thay vì phụ thuộc một SOTA duy nhất

### Limitation 5: Khối lượng 4 paper Q1 là rất nặng

Vấn đề:

- hội đồng có thể nghi ngờ tính khả thi của 4 bài Q1 trong một PhD

Fallback plan:

- nhấn mạnh đây là `target profile`, không phải cam kết hành chính cứng
- cấu trúc luận án vẫn đứng được với:
  - 2 bài rất mạnh
  - 1 bài mạnh vừa
  - 1 bài integration có điều kiện
- roadmap được thiết kế để tối đa hóa xác suất 4 Q1, nhưng vẫn bảo vệ được luận án nếu 1 bài chuyển thành Q2 rất mạnh

### Limitation 6: Công thức closed-loop gain có thể bị tranh luận

Vấn đề:

- hội đồng có thể hỏi weighting trong metric này có chủ quan không

Fallback plan:

- chốt metric trước khi chạy thí nghiệm
- báo cáo sensitivity analysis theo nhiều bộ trọng số
- trình bày cả metric thành phần lẫn metric tổng hợp

## 18.6. Phản biện trước 4 nhóm giáo sư đầu ngành AI

### Giáo sư thiên về machine learning foundation sẽ hỏi

- novelty kỹ thuật thực nằm ở đâu, hay chỉ là ghép kỹ thuật?

Cách trả lời:

- mỗi paper có đúng một novelty trung tâm
- contribution là reformulation của problem và mechanism, không phải cộng module

### Giáo sư thiên về systems / AI systems sẽ hỏi

- đóng góp hệ thống là gì ngoài việc tích hợp?

Cách trả lời:

- Paper 4 đóng góp interface, feedback semantics và closed-loop gain
- cả luận án định nghĩa reliability như thuộc tính hệ thống, không phải thuộc tính module

### Giáo sư thiên về domain applications sẽ hỏi

- tính thực tế và benchmark có đủ sát vận hành không?

Cách trả lời:

- mỗi paper gắn với pain point thật và có stress tests gần vận hành
- không đánh giá bằng score chung chung
- đánh giá bằng failure modes có ý nghĩa thực tế

### Giáo sư thiên về optimization / control sẽ hỏi

- Paper 3 có thực sự mới hơn reward shaping hay safe RL chuẩn không?

Cách trả lời:

- novelty nằm ở việc tách utility preference khỏi safety feasibility
- dual-head modeling và constrained update tạo một formulation khác reward scalar hóa
- utility-safety frontier là bằng chứng trung tâm

## 19. Tiêu chí chọn venue

## 19.1. Paper 1

Phù hợp với:

- AI in engineering
- knowledge-based systems
- intelligent maintenance
- applied AI systems

## 19.2. Paper 2

Phù hợp với:

- scheduling
- operations research with AI
- multi-agent RL
- intelligent manufacturing

## 19.3. Paper 3

Phù hợp với:

- smart grid AI
- safe RL
- energy systems optimization
- cyber-physical control

## 19.4. Paper 4

Phù hợp với:

- multi-agent systems
- AI systems
- autonomous agents
- industrial AI architecture

## 20. Điều kiện để luận án đạt chuẩn thế giới

Luận án đạt chuẩn thế giới nếu thỏa 7 điều kiện:

1. Có một problem framing mạnh:
   `reliable decision-making in complex engineering systems`

2. Có 4 contribution độc lập nhưng tích lũy:
   perception, coordination, alignment, integration

3. Có novelty không dựa vào ghép module:
   mỗi paper có một cơ chế trung tâm

4. Có evaluation nghiêm ngặt:
   baseline mạnh, ablation, stress test, error analysis

5. Có synthesis:
   giải thích vì sao closed-loop đáng nghiên cứu

6. Có giới hạn rõ:
   không overclaim universal generalization

7. Có artifact/protocol tái sử dụng:
   benchmark, metric, interface, evaluation scripts

## 21. Câu chuyện cuối cùng khi bảo vệ luận án

Khi bảo vệ, không nên nói:

`Tôi làm 4 paper: một paper về maintenance, một paper về FJSP, một paper về smart grid, một paper về integration.`

Nên nói:

`Luận án của tôi nghiên cứu cách xây dựng hệ đa tác nhân công nghiệp đáng tin cậy dưới uncertainty, dynamic perturbation và hard constraints. Tôi chứng minh rằng reliability không thể đạt được bằng một module đơn lẻ. Nó cần một chuỗi closed-loop: nhận thức phải được grounded bằng evidence vận hành, điều phối phải tách strategy khỏi dispatch để thích ứng, policy phải tách utility khỏi feasibility để an toàn, và toàn hệ phải có feedback semantics đo được để cải thiện robustness.`

Đây là câu chuyện PhD.

## 22. Kết luận

Roadmap 4 paper Q1 khả thi nhất không phải là làm 4 bài càng nhiều kỹ thuật càng tốt.  
Roadmap đúng là làm 4 bài có vai trò khoa học rõ:

- `Paper 1`: trả lời câu hỏi agent biết gì là đúng với vận hành thật
- `Paper 2`: trả lời câu hỏi agent điều phối thế nào khi môi trường đổi
- `Paper 3`: trả lời câu hỏi agent tối ưu thế nào mà vẫn an toàn
- `Paper 4`: trả lời câu hỏi feedback giữa các lớp có tạo gain hệ thống không

Nếu giữ được logic này, luận án không chỉ là tập hợp 4 công bố, mà là một đóng góp có cấu trúc về:

`closed-loop reliability for cognitive multi-agent systems in complex engineering domains`.

Đây là hướng đủ mạch lạc, đủ sâu và đủ khả thi để nhắm đến một luận án PhD đạt chuẩn quốc tế.
