# Paper 1 Chi Tiết

## Tên paper đề xuất

### Tên chính

`Belief-State Grounding for Reliable AIOps Decision-Making under Partial Observability`

### Tên thay thế ngắn hơn

`Belief-State Grounding for AIOps Agents under Partial Observability`

## 1. Vai trò của Paper 1 trong toàn bộ luận án

Paper 1 là nền tảng của toàn bộ luận án. Nếu các paper sau nghiên cứu cách agent quyết định, phối hợp và kiểm soát mức tự động hóa, thì Paper 1 trả lời câu hỏi trước đó:

`Trước khi ra quyết định, agent có thực sự hiểu trạng thái vận hành hiện tại của hệ thống đến mức nào?`

Trong AIOps, một agent không nên hành động chỉ dựa trên một alert, một anomaly score hoặc một root-cause label đơn lẻ. Nó cần một biểu diễn trạng thái có cấu trúc, thể hiện:

- hệ thống đang có khả năng ở trạng thái nào
- service hoặc component nào có khả năng bị ảnh hưởng
- root cause giả thuyết là gì
- mức độ chắc chắn đến đâu
- bằng chứng nào ủng hộ
- bằng chứng nào mâu thuẫn
- còn thiếu loại thông tin nào

Do đó, Paper 1 không phải là một bài `anomaly detection` thông thường. Paper 1 là bài về:

`decision-ready operational state representation under uncertainty`

## 2. Abstract dự thảo

Modern AIOps systems rely on heterogeneous observability signals such as logs, metrics, traces, alerts, and incident histories to support operational decision-making in distributed systems. Existing methods typically optimize isolated tasks such as anomaly detection, log classification, or root-cause localization, producing scores or labels that are often insufficient for downstream agentic decision-making. In practice, an AIOps agent must reason under partial observability, delayed signals, noisy evidence, and conflicting observations before deciding whether to act, observe more, defer, or escalate.

This paper proposes a belief-state grounding framework for reliable AIOps decision-making under partial observability. Instead of producing a single anomaly score or root-cause label, the proposed framework constructs a structured operational belief state that includes incident hypotheses, affected services, root-cause candidates, calibrated uncertainty, supporting evidence, conflicting evidence, and missing-evidence indicators. The framework integrates multi-source observability signals through evidence-aware fusion and explicitly models uncertainty and evidence conflict. We evaluate the proposed approach on public AIOps datasets, with GAIA as the primary benchmark and additional stress tests using KPI and log anomaly datasets. Experiments assess state inference accuracy, uncertainty calibration, robustness under missing and conflicting evidence, and downstream decision utility. The expected contribution is a decision-ready state grounding mechanism that provides a stronger foundation for uncertainty-aware action gating and risk-budgeted autonomy in AIOps agents.

## 3. Vấn đề nghiên cứu

### 3.1. Vấn đề thực tế

Trong vận hành IT, một sự cố thường không được quan sát trực tiếp. Nó được suy ra từ nhiều tín hiệu:

- logs
- metrics
- traces
- alerts
- topology
- incident history

Các tín hiệu này thường:

- thiếu
- nhiễu
- trễ
- mâu thuẫn
- không đồng bộ theo thời gian

Ví dụ:

- metrics cho thấy latency tăng nhưng logs chưa có lỗi rõ ràng
- alert báo service A, nhưng trace cho thấy bottleneck ở service B
- log anomaly xuất hiện ở nhiều service nhưng chỉ một service là root cause
- incident history gợi ý lỗi cũ, nhưng trạng thái hiện tại đã khác

Trong bối cảnh đó, nếu agent chỉ nhận một score hoặc label, agent sẽ khó biết:

- có nên tin kết quả hiện tại không
- nên hỏi thêm dữ liệu nào
- có đủ điều kiện để hành động chưa
- có cần chuyển người không

### 3.2. Vấn đề khoa học

Khoảng trống khoa học là:

`AIOps thiếu một cơ chế biểu diễn trạng thái vận hành có cấu trúc, được hiệu chuẩn uncertainty và sẵn sàng cho quyết định downstream trong điều kiện quan sát không đầy đủ.`

Các phương pháp hiện tại thường trả về:

- anomaly score
- log label
- root-cause ranking
- alert priority

Nhưng chúng chưa trả về một `belief state` có thể dùng trực tiếp cho agentic decision loop.

## 4. Câu hỏi nghiên cứu của Paper 1

### RQ1.1

`Làm thế nào để hợp nhất logs, metrics, traces, alerts và topology thành một belief state thống nhất cho AIOps?`

### RQ1.2

`Làm thế nào để belief state phản ánh không chỉ giả thuyết trạng thái mà còn cả uncertainty, support evidence và conflict evidence?`

### RQ1.3

`Belief state có cấu trúc có cải thiện robustness và downstream decision utility so với score-only hoặc label-only baselines không?`

## 5. Core hypothesis

Giả thuyết trung tâm:

`A structured and calibrated belief state improves the reliability of downstream AIOps decisions compared with score-only or label-only observability pipelines.`

Giả thuyết phụ:

- H1: Multi-source belief grounding cải thiện state inference so với single-source baselines.
- H2: Explicit uncertainty calibration làm giảm overconfident errors.
- H3: Support/conflict evidence modeling cải thiện robustness khi dữ liệu thiếu hoặc mâu thuẫn.
- H4: Belief state có cấu trúc cải thiện downstream action-readiness so với anomaly score hoặc RCA label đơn lẻ.

## 6. Định nghĩa belief state

Paper đề xuất một `AIOps belief state` dưới dạng object có cấu trúc:

```json
{
  "incident_hypothesis": "latency_degradation | resource_saturation | dependency_failure | normal | unknown",
  "affected_services": [
    {"service": "service_A", "probability": 0.74},
    {"service": "service_B", "probability": 0.21}
  ],
  "root_cause_hypotheses": [
    {"component": "database", "probability": 0.62},
    {"component": "api_gateway", "probability": 0.27}
  ],
  "severity_estimate": "low | medium | high | critical",
  "uncertainty": 0.34,
  "supporting_evidence": [
    "metric_latency_spike_service_A",
    "trace_bottleneck_database"
  ],
  "conflicting_evidence": [
    "no_error_log_in_service_A"
  ],
  "missing_evidence": [
    "recent_deployment_history",
    "database_cpu_metric"
  ],
  "action_readiness": "low | medium | high"
}
```

### Ý nghĩa của từng trường

- `incident_hypothesis`: trạng thái vận hành hiện tại mà agent tin là khả dĩ nhất.
- `affected_services`: các service có khả năng bị ảnh hưởng.
- `root_cause_hypotheses`: phân phối xác suất trên các nguyên nhân khả dĩ.
- `severity_estimate`: mức độ nghiêm trọng dự kiến.
- `uncertainty`: độ bất định tổng hợp của belief.
- `supporting_evidence`: bằng chứng ủng hộ giả thuyết hiện tại.
- `conflicting_evidence`: bằng chứng mâu thuẫn hoặc làm giảm độ tin cậy.
- `missing_evidence`: thông tin còn thiếu và có thể cần query thêm.
- `action_readiness`: tín hiệu nối sang Paper 2, cho biết state hiện tại đã đủ sẵn sàng để ra quyết định hay chưa.

## 7. Novelty của Paper 1

Novelty không nằm ở việc dùng một kiến trúc deep learning phức tạp hơn. Novelty nằm ở bốn điểm:

1. Định nghĩa `decision-ready belief state` cho AIOps.
2. Mô hình hóa đồng thời support evidence, conflict evidence và missing evidence.
3. Kết hợp uncertainty calibration vào operational state grounding.
4. Đánh giá state không chỉ bằng classification accuracy mà còn bằng robustness và downstream decision utility.

## 8. Phương pháp đề xuất

### 8.1. Tổng quan pipeline

```text
Logs      -> Log Encoder      \
Metrics   -> Metric Encoder    \
Traces    -> Trace Encoder      -> Evidence Fusion -> Belief State Decoder
Alerts    -> Alert Encoder     /
Topology  -> Graph Encoder    /
History   -> History Encoder /
```

### 8.2. Input

Tại thời điểm `t`, agent nhận tập quan sát:

```text
O_t = {L_t, M_t, T_t, A_t, G, H_t}
```

Trong đó:

- `L_t`: logs
- `M_t`: metrics time series
- `T_t`: traces
- `A_t`: alerts
- `G`: topology hoặc dependency graph
- `H_t`: incident history hoặc runbook context

### 8.3. Output

Mô hình học một mapping:

```text
f(O_<=t) -> b_t
```

Trong đó `b_t` là belief state có cấu trúc.

### 8.4. Các module chính

#### Log Encoder

Mục tiêu:

- chuyển log templates hoặc log messages thành vector evidence
- phát hiện log bất thường hoặc log liên quan đến incident

Có thể dùng:

- log template embedding
- sentence transformer
- lightweight transformer
- TF-IDF + classifier làm baseline mạnh đơn giản

#### Metric Encoder

Mục tiêu:

- encode time-series windows
- phát hiện trend, spike, degradation

Có thể dùng:

- TCN
- LSTM/GRU
- Transformer time-series encoder
- statistical features baseline

#### Trace Encoder

Mục tiêu:

- biểu diễn latency path, dependency bottleneck, service interaction

Có thể dùng:

- graph aggregation
- path-level features
- service dependency encoder

#### Topology Encoder

Mục tiêu:

- đưa dependency graph vào reasoning
- tránh nhầm service bị ảnh hưởng với root cause

Có thể dùng:

- GNN
- adjacency-aware attention
- graph propagation

#### Evidence Fusion

Mục tiêu:

- hợp nhất nhiều nguồn evidence
- gán trọng số nguồn theo reliability
- phát hiện conflict giữa nguồn

Có thể dùng:

- gated fusion
- cross-attention
- evidence graph fusion
- mixture-of-experts

#### Belief State Decoder

Sinh ra:

- incident hypothesis
- affected services
- root-cause distribution
- severity
- uncertainty
- support/conflict/missing evidence
- action readiness

## 9. Loss function đề xuất

Paper có thể dùng multi-objective loss:

```text
L = L_state
  + λ1 L_root_cause
  + λ2 L_calibration
  + λ3 L_evidence
  + λ4 L_consistency
```

Trong đó:

- `L_state`: loss cho incident type hoặc state class
- `L_root_cause`: loss cho root cause ranking hoặc localization
- `L_calibration`: calibration objective, ví dụ Brier/NLL/temperature scaling penalty
- `L_evidence`: loss cho evidence attribution nếu có proxy label
- `L_consistency`: consistency khi mask/missing modality hoặc khi evidence conflict

Nếu không có evidence label đầy đủ, có thể dùng weak supervision:

- evidence từ anomaly windows
- service-level labels
- dependency graph propagation
- attention attribution regularization
- perturbation-based evidence validation

## 10. Dataset và cách dùng

### 10.1. Dataset chính: GAIA

Nguồn:

`https://github.com/CloudWise-OpenSource/GAIA-DataSet`

Vai trò:

- dataset chính cho multi-source grounding
- có metrics, logs, traces, anomaly injection
- phù hợp để xây incident episodes

Sử dụng cho:

- state inference
- affected service prediction
- root cause localization
- robustness under missing modalities

### 10.2. KPI-Anomaly-Detection

Nguồn:

`https://github.com/NetManAIOps/KPI-Anomaly-Detection`

Vai trò:

- benchmark phụ cho KPI time-series
- kiểm tra khả năng grounding khi chỉ có metrics
- stress test false alarms

### 10.3. Public Log Anomaly Datasets

Nguồn:

`https://github.com/ait-aecid/anomaly-detection-log-datasets`

Dùng các bộ:

- HDFS
- BGL
- OpenStack
- Thunderbird

Vai trò:

- kiểm tra generalization trên log-only setting
- benchmark phụ cho log grounding

## 11. Experimental Tasks

### Task 1: Incident State Inference

Input:

- multi-source observability window

Output:

- incident type hoặc state class

Metrics:

- accuracy
- macro F1
- AUROC nếu binary/one-vs-rest

### Task 2: Root-Cause Hypothesis Ranking

Input:

- logs + metrics + traces + topology

Output:

- ranked list of root-cause services/components

Metrics:

- top-1 accuracy
- top-k accuracy
- MRR
- NDCG

### Task 3: Uncertainty Calibration

Input:

- model prediction distribution

Output:

- calibrated confidence

Metrics:

- ECE
- Brier score
- NLL
- reliability diagram
- risk-coverage curve

### Task 4: Evidence Robustness

Stress conditions:

- remove logs
- remove metrics
- delay traces
- inject noisy alerts
- mask topology edges
- create conflicting evidence

Metrics:

- performance drop
- calibration degradation
- conflict detection accuracy
- missing-evidence detection quality

### Task 5: Downstream Decision Utility

Input:

- belief state từ Paper 1

Downstream proxy:

- action readiness prediction
- hoặc một simple action gating policy

Compare:

- policy dùng anomaly score
- policy dùng RCA label
- policy dùng proposed belief state

Metrics:

- safe action readiness accuracy
- false-ready rate
- unnecessary-not-ready rate
- downstream risk proxy

## 12. Baselines

### 12.1. Single-source baselines

- log-only classifier
- metric-only anomaly detector
- trace-only RCA

### 12.2. Simple fusion baselines

- feature concatenation + MLP
- majority/score fusion
- early fusion transformer

### 12.3. Task-specific baselines

- anomaly detection baseline
- RCA ranking baseline
- log anomaly baseline

### 12.4. Uncertainty baselines

- softmax confidence
- temperature scaling
- MC dropout
- deep ensemble

### 12.5. Representation baselines

- score-only output
- label-only output
- RCA-only output
- proposed structured belief state

## 13. Ablation Study

Bắt buộc có các ablation sau:

1. Không dùng topology.
2. Không dùng trace.
3. Không dùng log evidence.
4. Không dùng metric evidence.
5. Không dùng uncertainty calibration.
6. Không dùng conflict modeling.
7. Không dùng missing-evidence indicator.
8. Thay structured decoder bằng plain classifier.

Mục tiêu ablation:

- xác định thành phần nào thực sự cần thiết
- chứng minh structured belief state không chỉ là packaging đẹp
- chứng minh uncertainty/conflict modeling có tác động thật

## 14. Expected Results

Paper kỳ vọng chứng minh:

1. Belief-state grounding cải thiện state inference so với single-source và simple fusion baselines.
2. Calibration tốt hơn softmax confidence hoặc uncalibrated fusion.
3. Robustness tốt hơn khi thiếu hoặc mâu thuẫn evidence.
4. Belief state giúp downstream action-readiness tốt hơn anomaly score hoặc RCA label.

Kết quả quan trọng nhất không nhất thiết là accuracy cao nhất tuyệt đối. Kết quả quan trọng hơn là:

`proposed belief state gives better calibrated and more decision-useful operational state estimates under partial observability.`

## 15. Cấu trúc paper đề xuất

### Abstract

- nêu vấn đề partial observability trong AIOps
- nói gap của score/label-only methods
- đề xuất belief-state grounding
- tóm tắt evaluation và kết quả chính

### 1. Introduction

Nội dung:

- AIOps cần quyết định dưới dữ liệu không hoàn hảo
- anomaly/RCA riêng lẻ không đủ cho agentic decision
- cần belief state
- contribution list

### 2. Related Work

Nhóm tài liệu:

- AIOps anomaly detection
- log analysis
- root-cause analysis
- multi-modal observability fusion
- uncertainty calibration
- agentic AI / decision-making under uncertainty

### 3. Problem Formulation

Nội dung:

- định nghĩa observability signals
- định nghĩa latent operational state
- định nghĩa belief state
- định nghĩa learning/evaluation objective

### 4. Method

Nội dung:

- architecture overview
- encoders
- evidence fusion
- uncertainty/conflict modeling
- belief state decoder

### 5. Experiments

Nội dung:

- datasets
- tasks
- baselines
- metrics
- implementation details

### 6. Results

Nội dung:

- main performance
- calibration results
- robustness results
- downstream utility
- ablation

### 7. Discussion

Nội dung:

- ý nghĩa với Agentic AIOps
- limitation
- liên kết sang Paper 2

### 8. Conclusion

Nội dung:

- belief-state grounding là nền tảng cho reliable AIOps agents

## 16. Reviewer Risk và cách phòng thủ

### Risk 1: Reviewer nói đây chỉ là multi-modal fusion

Phòng thủ:

- nhấn vào belief state có cấu trúc
- nhấn vào support/conflict/missing evidence
- nhấn vào calibration và downstream utility

### Risk 2: Reviewer hỏi ground truth của belief state ở đâu

Phòng thủ:

- belief state là operational abstraction
- dùng proxy labels: incident type, affected service, root cause
- đánh giá thêm downstream decision utility

### Risk 3: Reviewer nói method quá phức tạp

Phòng thủ:

- có simple baselines mạnh
- có ablation
- chứng minh component nào cần thiết

### Risk 4: Reviewer nói dataset không đủ production-realistic

Phòng thủ:

- dùng GAIA làm main benchmark
- thêm stress tests
- giới hạn claim ở offline evaluated AIOps

## 17. Minimum Viable Paper

Nếu muốn làm bản paper khả thi nhất, không nên ôm quá nhiều. MVP gồm:

1. GAIA là dataset chính.
2. Output belief state gồm:
   - incident hypothesis
   - affected/root-cause service
   - uncertainty
   - support/conflict evidence
   - action readiness
3. So sánh với:
   - log-only
   - metric-only
   - concat fusion
   - RCA-only
4. Experiments:
   - state inference
   - root-cause ranking
   - calibration
   - missing modality stress test
   - simple downstream action readiness

Đây là phạm vi đủ tốt để viết một paper đầu tiên, không bị quá lớn.

## 18. One-sentence pitch

`This paper proposes a structured, calibrated, and evidence-aware belief state for AIOps agents, enabling more reliable downstream decisions under partial and conflicting observability.`

## 19. Kết luận

Paper 1 nên được định vị là bài nền tảng về `operational state grounding`, không phải bài cải tiến anomaly detection. Nếu làm đúng, paper này sẽ tạo ra object trung tâm cho toàn bộ luận án: `belief state`. Các paper sau sẽ dùng object này để nghiên cứu action gating, coordination và risk-budgeted autonomy.

Điểm quan trọng nhất cần giữ là:

`Không bán Paper 1 như một model mới. Hãy bán Paper 1 như một cách biểu diễn và grounding trạng thái vận hành có uncertainty, evidence và decision utility.`
