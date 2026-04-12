# Paper 2 Chi Tiết

## Tên paper đề xuất

### Tên chính

`Uncertainty-Aware Action Gating for Reliable AIOps Agents`

### Tên thay thế

`Act, Defer, Observe, or Escalate: Decision Gating for AIOps under Uncertainty`

## 1. Vai trò của Paper 2 trong toàn bộ luận án

Nếu Paper 1 trả lời câu hỏi `agent đang biết gì`, thì Paper 2 trả lời câu hỏi:

`Khi agent chưa biết đủ chắc chắn, agent nên làm gì tiếp theo?`

Đây là paper bản lề của luận án, vì nó chuyển từ `state representation` sang `decision policy`. Trong thực tế AIOps, nhiều sai lầm không đến từ việc hệ thống hoàn toàn không nhìn ra vấn đề, mà đến từ việc hệ:

- hành động quá sớm
- chờ quá lâu
- hỏi thêm dữ liệu không cần thiết
- escalate quá nhiều
- hoặc escalate quá muộn

Do đó, Paper 2 không nghiên cứu hành động theo nghĩa control thấp tầng, mà nghiên cứu:

`high-level operational action gating under uncertainty`

## 2. Abstract dự thảo

Operational AI systems increasingly require more than anomaly detection or root-cause ranking: they must decide whether to act, wait, gather more information, or escalate to humans. In AIOps, these choices are made under partial observability, delayed evidence, and asymmetric costs of false actions versus delayed interventions. Existing pipelines often force a prediction-based response without explicitly modeling action deferral, evidence gathering, or escalation. This creates a gap between predictive confidence and safe operational decision-making.

This paper proposes an uncertainty-aware action gating framework for reliable AIOps agents. Given a structured operational belief state, the proposed framework selects among four high-level actions: `act`, `defer`, `observe_more`, and `escalate`. The decision policy is conditioned on calibrated uncertainty, incident severity, evidence sufficiency, and risk-sensitive action costs. We formulate action gating as a bounded-risk decision problem and evaluate it on incident episodes derived from public AIOps datasets. Experiments compare the proposed framework against reactive and threshold-based baselines, measuring safe success, false automation, delayed escalation cost, and downstream risk. The expected contribution is a decision policy that better aligns AIOps automation with uncertainty and operational risk.

## 3. Vấn đề nghiên cứu

### 3.1. Vấn đề thực tế

Trong vận hành IT, sau khi có bằng chứng ban đầu, agent thường đứng trước bốn lựa chọn:

- `act`
- `defer`
- `observe_more`
- `escalate`

Ví dụ:

- một alert cho thấy latency tăng ở service A
- metrics và trace gợi ý database saturation
- logs lại chưa có lỗi rõ ràng

Nếu agent `act` ngay bằng rollback hoặc restart, có thể gây gián đoạn không cần thiết. Nếu agent `defer` quá lâu, sự cố có thể lan rộng. Nếu agent `observe_more` quá nhiều lần, thời gian khôi phục bị chậm. Nếu agent `escalate` quá sớm, chi phí nhân sự tăng và mất lợi ích của tự động hóa.

Khoảng trống ở đây là:

`AIOps thiếu một policy ra quyết định cấp cao có nhận thức bất định và cost asymmetry.`

### 3.2. Vấn đề khoa học

Các pipeline hiện tại thường dùng:

- threshold trên anomaly score
- confidence threshold đơn giản
- rule-based escalation

Nhưng chúng không giải quyết đầy đủ các yếu tố:

- uncertainty có được hiệu chuẩn hay không
- evidence hiện tại đã đủ cho hành động chưa
- chi phí của false action và delayed action khác nhau ra sao
- khi nào nên mua thêm thông tin bằng `observe_more`

## 4. Câu hỏi nghiên cứu của Paper 2

### RQ2.1

`Làm thế nào để chuyển belief state thành quyết định cấp cao giữa act, defer, observe_more và escalate?`

### RQ2.2

`Làm thế nào để policy phản ánh đúng cost asymmetry giữa false action, delayed action và unnecessary escalation?`

### RQ2.3

`Liệu một action gating policy có nhận thức uncertainty có cải thiện safe success so với threshold-based baselines không?`

## 5. Core hypothesis

`A risk-sensitive action gating policy conditioned on a structured belief state yields safer and more efficient AIOps decisions than reactive or threshold-based alternatives.`

## 6. Action space và semantics

### `act`

Hệ đủ tin rằng nên đưa ra khuyến nghị hoặc thực hiện hành động mô phỏng.

Ví dụ:

- recommend rollback
- recommend restart
- recommend scaling
- auto-open ticket với runbook cụ thể

### `defer`

Hệ quyết định chưa làm gì ngay, chờ evidence tự đến trong vài bước tiếp theo.

### `observe_more`

Hệ chủ động yêu cầu thêm thông tin:

- query thêm log window
- query thêm trace span
- query dependency state
- query deployment history

### `escalate`

Hệ chuyển cho human operator hoặc on-call engineer.

## 7. Novelty của Paper 2

1. Action gating 4 chiều thay vì action/no-action nhị phân.
2. Policy có điều kiện trên structured belief state, không chỉ anomaly score.
3. Cost-sensitive decision-making dưới uncertainty.
4. Evaluation bằng safe success, false automation và delayed escalation cost.

## 8. Problem formulation

Tại thời điểm `t`, agent có belief state `b_t` từ Paper 1.

Policy:

```text
π(a_t | b_t, r_t, c)
```

Trong đó:

- `a_t ∈ {act, defer, observe_more, escalate}`
- `b_t`: belief state
- `r_t`: remaining risk budget hoặc risk state
- `c`: cost profile

Objective:

```text
maximize safe_success
subject to cumulative_risk <= budget
```

## 9. Phương pháp đề xuất

### 9.1. Decision policy options

#### Option A: Cost-sensitive classifier

Đơn giản, dễ làm, phù hợp bản đầu.

#### Option B: Contextual bandit

Tự nhiên hơn cho `observe_more`.

Khuyến nghị:

Nên bắt đầu bằng `Option A` và dùng `Option B` như hướng mở rộng.

### 9.2. Feature set cho gating

- incident hypothesis confidence
- uncertainty
- severity estimate
- root-cause entropy
- evidence conflict score
- missing-evidence score
- number of observe_more steps already used
- remaining risk budget
- elapsed decision time

### 9.3. Confidence is not enough

Paper cần nhấn mạnh:

`confidence != readiness`

## 10. Experimental environment

### 10.1. Episode design

Mỗi episode gồm:

1. incident xuất hiện
2. agent nhận initial evidence
3. agent có thể observe_more tối đa K lần
4. ở mỗi bước, agent chọn hành động
5. episode kết thúc khi:
   - act
   - escalate
   - hết horizon

### 10.2. Transition after observe_more

Nếu chọn `observe_more`, environment trả về:

- thêm log chunk
- thêm metric window
- trace mới
- deployment info

## 11. Reward / Cost model

Ví dụ:

```text
Cost(act_wrong)            = 10
Cost(act_correct)          = 0
Cost(defer_each_step)      = 1
Cost(observe_more_each)    = 0.5
Cost(unnecessary_escalate) = 2
Cost(missed_incident)      = 12
Cost(late_escalation)      = 6
```

## 12. Baselines

- Reactive act-now
- Confidence threshold
- Two-stage threshold
- Human-escalate-always
- Score-only gating
- Proposed belief-state-based gating

## 13. Metrics

### Primary metrics

- `safe success rate`
- `bounded-risk success rate`
- `expected operational cost`

### Secondary metrics

- false automation rate
- delayed escalation cost
- unnecessary escalation rate
- average number of observations
- average time-to-decision

## 14. Ablations

1. Không dùng uncertainty.
2. Không dùng conflict score.
3. Không dùng missing-evidence score.
4. Không dùng remaining risk budget.
5. Không có `observe_more`.
6. Không có `defer`.
7. Thay belief state bằng anomaly score.

## 15. Expected results

Paper kỳ vọng chứng minh:

1. Policy dùng belief state tốt hơn policy dùng score-only.
2. Observe_more giúp giảm false action trong vùng uncertainty trung bình.
3. Risk-sensitive gating tốt hơn fixed threshold trong nhiều cost regimes.

## 16. Cấu trúc paper đề xuất

### Abstract

- gap của threshold-based automation
- 4-action policy
- risk-sensitive evaluation

### 1. Introduction

- predictive AIOps không đủ cho operational action
- cần gating under uncertainty

### 2. Related Work

- anomaly-based AIOps
- abstention/deferral learning
- selective classification
- active information gathering

### 3. Problem Formulation

- action space
- cost model
- budgeted decision problem

### 4. Method

- belief-state-to-action mapping
- risk-sensitive policy

### 5. Experiments

- datasets/episodes
- baselines
- metrics

### 6. Results

- main comparison
- cost sensitivity
- ablation

## 17. Reviewer risk và cách phòng thủ

### Risk 1: “Đây chỉ là thresholding tinh vi hơn”

Phòng thủ:

- action space 4 chiều
- belief-state conditioning
- explicit observe_more

### Risk 2: “Cost model là chủ quan”

Phòng thủ:

- minh bạch cost assumptions
- sensitivity analysis nhiều regime

## 18. Minimum Viable Paper

1. Input từ belief state của Paper 1.
2. 4 actions: act, defer, observe_more, escalate.
3. GAIA-derived incident episodes.
4. Baselines:
   - act-now
   - threshold gating
   - escalate-always
   - score-only gating
5. Metrics:
   - safe success
   - false automation
   - escalation cost
   - average observations

## 19. One-sentence pitch

`This paper studies how an AIOps agent should choose between acting, waiting, gathering more evidence, and escalating when observability is incomplete and action costs are asymmetric.`
