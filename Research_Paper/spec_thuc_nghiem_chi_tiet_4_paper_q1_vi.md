# Spec Thực Nghiệm Chi Tiết Cho 4 Paper Q1

## 1. Mục tiêu của tài liệu này

Tài liệu này không chỉ mô tả ý tưởng.  
Mục tiêu của nó là biến 4 đề xuất nghiên cứu thành các `spec thực nghiệm có thể triển khai trực tiếp`, để khi đọc xong bạn có thể:

- chọn bài nào làm trước
- biết cần chuẩn bị dữ liệu gì
- biết baseline nào phải chạy
- biết phải đo metric gì
- biết cần làm ablation nào
- biết thứ tự chạy thí nghiệm ra sao
- biết điều kiện nào đủ để nói bài có tín hiệu Q1

Nguyên tắc xây spec này:

- mỗi paper chỉ có `một novelty trung tâm`
- mọi thực nghiệm phải phục vụ việc chứng minh novelty đó
- không được làm thí nghiệm chỉ để “có thêm số”
- stress test và error analysis là bắt buộc

## 2. Cách dùng tài liệu này

Mỗi paper sẽ được trình bày theo đúng thứ tự:

1. `Mục tiêu thực nghiệm`
2. `Novelty cần chứng minh`
3. `Input / Output`
4. `Dữ liệu / simulator`
5. `Pipeline triển khai`
6. `Baselines`
7. `Ablations`
8. `Stress tests`
9. `Metrics`
10. `Bảng chạy thí nghiệm theo thứ tự`
11. `Tiêu chí thành công`
12. `Rủi ro và cách pivot`

## 3. Paper 1: Grounded Perception

## 3.1. Tên bài

`Observability-Grounded Conflict-Validated Dual-Memory Reasoning for Industrial Maintenance Agents`

## 3.2. Mục tiêu thực nghiệm

Chứng minh rằng:

- reasoning grounded bằng observability tốt hơn semantic-only grounding
- `temporal retrieval` giúp giảm lỗi do evidence cũ
- `conflict validation` giúp giảm khuyến nghị không được trạng thái vận hành hỗ trợ

## 3.3. Novelty duy nhất cần chứng minh

`conflict-validated temporal grounding`

Nếu thí nghiệm không chứng minh được novelty này, bài sẽ yếu.

## 3.4. Problem formulation

### Input

- `Query / task`
  - ví dụ: chẩn đoán nguyên nhân lỗi, khuyến nghị hành động bảo trì, xác nhận trạng thái thiết bị
- `Semantic memory`
  - ontology thiết bị
  - SOP / manual
  - quan hệ component-subsystem
  - rules
- `Observability memory`
  - logs
  - traces
  - sensor readings
  - alarms/events
  - execution history
  - timestamps

### Output

```json
{
  "answer": "...",
  "evidence_set": [...],
  "supported_claims": [...],
  "unsupported_claims": [...],
  "inconsistency_score": 0.0,
  "uncertainty_score": 0.0
}
```

## 3.5. Dữ liệu / benchmark cần chuẩn bị

Bạn có 3 lựa chọn, theo thứ tự ưu tiên thực tế:

### Lựa chọn A: synthetic maintenance benchmark

Dựng benchmark bán mô phỏng từ:

- asset taxonomy
- fault templates
- logs templates
- sensor event templates
- maintenance procedures

Ưu điểm:

- dễ kiểm soát stale evidence, missing logs, conflicting evidence
- rất phù hợp để đánh giá novelty

Nhược điểm:

- reviewer có thể hỏi realism

### Lựa chọn B: industrial logs + manually curated knowledge base

Nguồn:

- public predictive maintenance datasets
- public machinery fault datasets
- SOP / maintenance text

Ưu điểm:

- realism cao hơn

Nhược điểm:

- cần công sức map entity và align evidence

### Lựa chọn C: hybrid benchmark

Kết hợp:

- public logs/sensor data
- synthetic contradiction injection
- curated knowledge graph

Đây là lựa chọn tốt nhất nếu đủ thời gian.

## 3.6. Pipeline triển khai

### Bước 1: semantic memory builder

Xây graph hoặc structure lưu:

- machine type
- subsystem
- component relation
- fault-cause relation
- maintenance procedure
- rule constraints

### Bước 2: observability memory builder

Chuẩn hóa:

- timestamps
- event types
- source IDs
- reliability score
- machine/entity mapping

### Bước 3: temporal evidence retriever

Scoring gợi ý:

```text
Score(evidence) =
  w1 * semantic_relevance
  + w2 * entity_match
  + w3 * recency_score
  + w4 * validity_window_score
  + w5 * source_reliability
```

### Bước 4: claim extraction

Từ answer / reasoning chain, tách các claim như:

- thiết bị X đang lỗi Y
- nguyên nhân là Z
- hành động khuyến nghị là A

### Bước 5: conflict validation

So sánh claim với evidence:

- `supported`
- `unsupported`
- `contradicted`
- `stale-supported`

### Bước 6: grounded decision output

Sinh:

- answer
- evidence_set
- inconsistency_score
- uncertainty_score

## 3.7. Baselines bắt buộc

1. `Semantic-only KG`
2. `Vector RAG`
3. `KG-RAG`
4. `Dual-memory without temporal retrieval`
5. `Dual-memory without conflict validation`

## 3.8. Ablations bắt buộc

1. bỏ `temporal retrieval`
2. bỏ `conflict validation`
3. bỏ `source reliability`
4. chỉ dùng observability memory
5. chỉ dùng semantic memory

## 3.9. Stress tests bắt buộc

1. `missing logs`
2. `noisy logs`
3. `stale evidence`
4. `conflicting evidence`
5. `entity mapping corruption`

## 3.10. Metrics

### Metric headline

- `hallucination_rate`

Định nghĩa gợi ý:

```text
hallucination_rate =
  (# unsupported_or_contradicted_claims) / (# total_claims)
```

### Metric phụ

- evidence grounding precision
- evidence grounding recall
- inconsistency detection F1
- maintenance task success
- calibration of uncertainty score

## 3.11. Thứ tự chạy thí nghiệm

### Run group P1-A: benchmark sanity

1. chạy semantic-only
2. chạy vector RAG
3. kiểm tra metric có phân biệt được lỗi thật không

### Run group P1-B: baseline core

4. chạy KG-RAG
5. chạy dual-memory no-temporal
6. chạy dual-memory no-conflict

### Run group P1-C: method full

7. chạy full method
8. so sánh trên benchmark sạch

### Run group P1-D: ablation

9. no temporal
10. no conflict
11. no reliability

### Run group P1-E: stress

12. stale evidence
13. conflicting evidence
14. noisy logs
15. missing logs

## 3.12. Tiêu chí thành công

Paper 1 có tín hiệu mạnh nếu:

- full method tốt hơn `dual-memory no-conflict`
- temporal retrieval cải thiện rõ trên stale-evidence setting
- conflict validation cải thiện rõ trên contradictory-evidence setting
- uncertainty score tương quan với error

## 3.13. Rủi ro và pivot

### Rủi ro

Conflict validation chỉ giống reranking.

### Pivot

Nếu gain nhỏ, tăng trọng tâm vào:

- conflict type taxonomy
- unsupported vs contradicted reasoning analysis
- calibration của uncertainty score

## 4. Paper 2: Adaptive Coordination

## 4.1. Tên bài

`Strategy-Dispatch Decomposed Hierarchical Graph Coordination for Dynamic Flexible Job Shop Scheduling`

## 4.2. Mục tiêu thực nghiệm

Chứng minh rằng:

- phân rã strategy-dispatch tạo gain riêng
- hierarchy tăng robustness khi có perturbation
- graph representation chỉ là support, không phải novelty chính

## 4.3. Novelty duy nhất cần chứng minh

`strategy-dispatch decomposition`

## 4.4. Problem formulation

### Input

- jobs
- operations
- machines
- processing times
- constraints
- current perturbation state

### Output

```json
{
  "strategy_signal": "...",
  "dispatch_actions": [...],
  "context_embedding": [...],
  "rescheduling_cost": 0.0,
  "recovery_time": 0.0
}
```

## 4.5. Dữ liệu / simulator

Nên dùng:

- benchmark FJSP chuẩn
- simulator dynamic FJSP có thể inject perturbation

Tối thiểu cần hỗ trợ:

- machine breakdown
- urgent job arrival
- due-date shift
- processing-time uncertainty

## 4.6. Pipeline triển khai

### Bước 1: graph state encoder

Node types:

- job
- operation
- machine
- optional constraint/resource nodes

Edge types:

- precedence
- machine eligibility
- assignment
- queue relation

### Bước 2: strategy-level policy

Chọn:

- scheduling mode
- objective bias
- subgoal / priority regime

Ví dụ strategy choices:

- minimize tardiness mode
- minimize makespan mode
- recovery mode after breakdown
- urgent-order mode

### Bước 3: dispatch-level policies

Thực hiện:

- machine assignment
- operation sequencing
- local dispatch update

### Bước 4: dynamic adaptation loop

Khi perturbation tới:

- update context embedding
- re-evaluate strategy
- apply dispatch revision

## 4.7. Baselines bắt buộc

1. heuristic dispatch rules
2. single-agent RL
3. flat MARL
4. MAMHSAN-like graph-attention MARL
5. hierarchy without graph
6. graph without hierarchy

## 4.8. Ablations bắt buộc

1. bỏ hierarchy
2. giữ hierarchy nhưng bỏ graph
3. giữ graph nhưng strategy fixed
4. không context adaptation
5. master policy bị random hóa

## 4.9. Stress tests bắt buộc

1. machine breakdown
2. urgent jobs
3. due-date shift
4. processing-time drift
5. partial observability

## 4.10. Metrics

### Metric headline

- makespan
- total tardiness

### Metric phụ

- machine utilization
- recovery time after perturbation
- rescheduling cost
- convergence stability
- robustness score under perturbation

## 4.11. Thứ tự chạy thí nghiệm

### Run group P2-A: static sanity

1. heuristic
2. flat RL
3. graph RL

### Run group P2-B: dynamic baseline

4. flat MARL dynamic
5. MAMHSAN-like baseline

### Run group P2-C: hierarchy core

6. hierarchy without graph
7. full hierarchy + graph

### Run group P2-D: ablation

8. no hierarchy
9. no context adaptation
10. fixed strategy

### Run group P2-E: perturbation stress

11. breakdown
12. urgent jobs
13. due-date shift
14. mixed perturbation

## 4.12. Tiêu chí thành công

Paper 2 có tín hiệu mạnh nếu:

- full model vượt `MAMHSAN-like` trên dynamic settings
- hierarchy tạo gain rõ hơn static setting
- recovery time giảm đáng kể dưới perturbation
- fixed-strategy version kém rõ so với adaptive hierarchy

## 4.13. Rủi ro và pivot

### Rủi ro

Hierarchy không tạo gain đủ rõ.

### Pivot

Nếu hierarchy yếu, đổi trọng tâm sang:

- strategy-switching under perturbation
- recovery-aware coordination
- perturbation-conditioned scheduling regime selection

## 5. Paper 3: Safe Alignment

## 5.1. Tên bài

`Constraint-Aware Preference-Guided Optimization for Safe Smart Grid Control`

## 5.2. Mục tiêu thực nghiệm

Chứng minh rằng:

- tách utility và feasibility tốt hơn scalar reward
- preference signal giúp tăng utility mà không tăng violation
- constrained update tốt hơn soft penalty

## 5.3. Novelty duy nhất cần chứng minh

`utility-feasibility separation`

## 5.4. Problem formulation

### Input

- grid state
- demand
- renewable forecast
- line/load states
- reserve requirement
- preference signals / ranking

### Output

```json
{
  "action": "...",
  "utility_score": 0.0,
  "safety_score": 0.0,
  "violation_risk": 0.0,
  "constraint_margin": 0.0
}
```

## 5.5. Dữ liệu / simulator

Nên chọn một domain cụ thể:

- unit commitment
hoặc
- economic dispatch

Tốt nhất:

- IEEE test systems
- simulator có support uncertainty injection

## 5.6. Pipeline triển khai

### Bước 1: constrained environment

Chuẩn hóa:

- state
- action
- utility objective
- hard constraints

### Bước 2: preference pair generation

Sinh preference từ:

- expert rules
- simulator outcomes
- ranking theo utility-safety trade-off

Ví dụ:

- trajectory A > trajectory B nếu
  - utility tốt hơn
  - và không tăng violation

### Bước 3: dual-head reward model

- utility head
- safety/feasibility head

### Bước 4: constrained policy update

Sử dụng:

- Lagrangian update
hoặc
- constrained optimization equivalent

### Bước 5: frontier evaluation

Vẽ:

- utility vs safety violation
- compare baselines

## 5.7. Baselines bắt buộc

1. constrained RL
2. safe RL
3. penalty-based reward shaping
4. preference-only optimization
5. safety-only optimization
6. dual-head without constrained update

## 5.8. Ablations bắt buộc

1. bỏ utility head
2. bỏ safety head
3. bỏ constrained update
4. bỏ preference
5. scalarize utility+safety thành một reward

## 5.9. Stress tests bắt buộc

1. load surge
2. renewable fluctuation
3. line outage
4. demand uncertainty
5. adversarial condition shift

## 5.10. Metrics

### Metric headline

- safety violation rate

### Metric phụ

- feasibility rate
- operating cost
- return / profit
- load shedding
- utility-safety frontier area
- robustness under uncertainty

## 5.11. Thứ tự chạy thí nghiệm

### Run group P3-A: environment sanity

1. heuristic / rules baseline
2. constrained RL baseline

### Run group P3-B: scalar reward family

3. penalty-based baseline
4. safe RL baseline

### Run group P3-C: preference family

5. preference-only
6. dual-head no-constrained update
7. full method

### Run group P3-D: ablation

8. no utility head
9. no safety head
10. no preference

### Run group P3-E: stress

11. load surge
12. renewable fluctuation
13. line outage
14. mixed uncertainty

## 5.12. Tiêu chí thành công

Paper 3 có tín hiệu mạnh nếu:

- full method giảm violation so với scalar reward baselines
- utility không giảm mạnh khi violation giảm
- dual-head vượt scalarization
- frontier utility-safety tốt hơn constrained RL

## 5.13. Rủi ro và pivot

### Rủi ro

Preference data không đủ thuyết phục.

### Pivot

Nếu preference yếu, chuyển trọng tâm sang:

- dual-head constrained optimization
- explicit feasibility modeling
- risk-aware safe policy learning

Giữ preference như support signal thay vì novelty chính.

## 6. Paper 4: Closed-Loop Integration

## 6.1. Tên bài

`Event-Triggered Closed-Loop Integration for Cognitive Multi-Agent Systems in Complex Engineering Domains`

## 6.2. Mục tiêu thực nghiệm

Chứng minh rằng:

- closed-loop feedback tốt hơn open-loop pipeline
- event-triggered feedback tốt hơn fixed-interval feedback
- uncertainty, conflict và near-violation là các trigger hữu ích thật

## 6.3. Novelty duy nhất cần chứng minh

`event-triggered closed-loop gain`

## 6.4. Problem formulation

### Input

- grounded_state từ Paper 1
- coordination_state từ Paper 2
- alignment_state từ Paper 3

### Output

```json
{
  "feedback_signal": "...",
  "trigger_type": "...",
  "closed_loop_gain": 0.0,
  "latency_overhead": 0.0,
  "compute_overhead": 0.0
}
```

## 6.5. Dữ liệu / evaluation setup

Không cần một full-stack system quá nặng ngay từ đầu.  
Có thể đánh giá theo `domain slices`:

- maintenance slice cho uncertainty/conflict
- scheduling slice cho perturbation response
- smart-grid slice cho near-violation / safety

## 6.6. Pipeline triển khai

### Bước 1: interface specification

Chuẩn hóa các field:

- uncertainty_score
- inconsistency_score
- strategy_signal
- perturbation_status
- violation_risk
- constraint_margin

### Bước 2: trigger engine

Trigger khi:

- uncertainty vượt ngưỡng
- evidence conflict tăng
- perturbation spike
- near-constraint violation

### Bước 3: feedback routing

Ví dụ:

- alignment -> coordination: risk-aware prior
- coordination -> perception: request re-grounding
- perception -> coordination: uncertainty-aware decision gate

### Bước 4: performance comparison

So sánh:

1. open-loop
2. pairwise integration
3. full integration without feedback
4. fixed-interval feedback
5. event-triggered feedback

## 6.7. Baselines bắt buộc

1. open-loop pipeline
2. pairwise integration
3. no-feedback full system
4. fixed-interval feedback
5. random trigger feedback

## 6.8. Ablations bắt buộc

1. bỏ uncertainty trigger
2. bỏ conflict trigger
3. bỏ near-violation trigger
4. bỏ risk-aware prior
5. thay event-trigger bằng periodic trigger

## 6.9. Stress tests bắt buộc

1. uncertainty spike
2. evidence conflict burst
3. sudden perturbation
4. near-violation episode
5. mixed trigger scenario

## 6.10. Metrics

### Metric headline

- closed-loop gain

### Metric phụ

- task success
- robustness
- safety violation
- recovery time
- trigger precision
- latency overhead
- compute overhead

## 6.11. Công thức closed-loop gain gợi ý

```text
CLG = NormalizedPerformanceGain
      - alpha * LatencyOverhead
      - beta * ComputeOverhead
```

Trong đó:

```text
NormalizedPerformanceGain =
  (P_closed - P_open) / max(|P_open|, epsilon)
```

## 6.12. Thứ tự chạy thí nghiệm

### Run group P4-A: interface sanity

1. kiểm tra output Paper 1-3 map được vào schema chung

### Run group P4-B: baseline integration

2. open-loop
3. pairwise
4. full no-feedback

### Run group P4-C: feedback variants

5. fixed-interval feedback
6. random trigger
7. event-triggered full

### Run group P4-D: trigger ablation

8. no uncertainty trigger
9. no conflict trigger
10. no near-violation trigger

### Run group P4-E: stress

11. uncertainty burst
12. perturbation burst
13. safety-risk burst
14. mixed burst

## 6.13. Tiêu chí thành công

Paper 4 có tín hiệu mạnh nếu:

- event-triggered closed-loop vượt full no-feedback
- fixed-interval kém hơn event-triggered ở gain-overhead trade-off
- ít nhất 2 trigger types có gain riêng rõ

## 6.14. Rủi ro và pivot

### Rủi ro

Closed-loop gain không rõ hoặc overhead quá cao.

### Pivot

Nếu full integration quá nặng:

- chuyển sang `protocol paper`
- nhấn mạnh interface + trigger semantics + gain measurement trên domain slices

## 7. Bảng ưu tiên thực hiện

| Paper | Mức khả thi | Mức rủi ro | Nên làm trước? | Lý do |
|---|---:|---:|---:|---|
| Paper 1 | Cao | Thấp | Có | dễ khóa metric và novelty nhất |
| Paper 2 | Khá cao | Vừa | Có | mạnh nếu hierarchy tạo gain rõ |
| Paper 3 | Khá | Vừa đến cao | Sau | cần chốt formulation thật chặt |
| Paper 4 | Có điều kiện | Vừa | Sau cùng | phụ thuộc interface 3 bài trước |

## 8. Kế hoạch chạy thực tế trong 12 tuần đầu

## Tuần 1-2

- chốt benchmark / synthetic setup cho Paper 1
- chốt metric hallucination_rate
- dựng semantic memory + observability memory prototype

## Tuần 3-4

- chạy baseline Paper 1
- chạy full method Paper 1 bản đơn giản
- kiểm tra conflict validation có tín hiệu không

## Tuần 5-6

- dựng dynamic FJSP simulator / baseline
- chạy heuristic và flat MARL cho Paper 2

## Tuần 7-8

- dựng hierarchy prototype cho Paper 2
- kiểm tra gain dưới breakdown / urgent job setting

## Tuần 9-10

- chọn environment cho Paper 3
- dựng constrained RL baseline
- thiết kế preference protocol

## Tuần 11-12

- chạy Paper 3 baseline family
- quyết định có giữ framing dual-head + preference không

## 9. Điều quan trọng nhất khi triển khai

Đừng làm theo kiểu:

- paper nào cũng code full system ngay từ đầu

Phải làm theo kiểu:

- mỗi paper có `minimal experiment` để chứng minh novelty trước

### Minimal experiment cho từng paper

#### Paper 1

Chỉ cần chứng minh:

- stale evidence và conflicting evidence làm baseline gãy
- full method sửa được

#### Paper 2

Chỉ cần chứng minh:

- trong dynamic perturbation setting, hierarchy tốt hơn flat policy

#### Paper 3

Chỉ cần chứng minh:

- dual-head + constrained update tốt hơn scalar reward

#### Paper 4

Chỉ cần chứng minh:

- event-triggered feedback tốt hơn no-feedback và fixed-interval

## 10. Kết luận

Nếu bạn cần thứ `đọc xong có thể bắt tay làm ngay`, thì trọng tâm không phải là đọc thêm thật nhiều proposal, mà là:

- chốt novelty
- chốt metric
- chốt baseline
- chốt minimal experiment

Tài liệu này đã chuyển 4 hướng nghiên cứu thành 4 `spec thực nghiệm` theo đúng logic đó.

Nói ngắn gọn:

- `Paper 1`: làm ngay được
- `Paper 2`: làm ngay sau khi có simulator động
- `Paper 3`: làm được nếu khóa environment và preference protocol
- `Paper 4`: chỉ làm khi output 3 bài trước đủ rõ

Đây là mức chi tiết đủ để bạn bắt đầu triển khai, thử nghiệm và so sánh trực tiếp thay vì chỉ dừng ở mức ý tưởng.
