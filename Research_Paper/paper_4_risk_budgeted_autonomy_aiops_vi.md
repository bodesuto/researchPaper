# Paper 4 Chi Tiết

## Tên paper đề xuất

### Tên chính

`Risk-Budgeted Autonomy for Reliable AIOps Agents`

### Tên thay thế

`How Much Autonomy is Safe? Risk-Budgeted Control for Agentic AIOps`

## 1. Vai trò của Paper 4 trong toàn bộ luận án

Paper 4 là paper tích hợp có đóng góp khoa học riêng rõ nhất. Nếu:

- Paper 1 hỏi `agent biết gì`
- Paper 2 hỏi `agent nên làm gì`
- Paper 3 hỏi `khi nào nên cập nhật workflow`

thì Paper 4 hỏi:

`Agent nên được phép tự động đến đâu khi rủi ro tích lũy tăng lên?`

Đây là paper quan trọng nhất để làm cho luận án không bị nhìn như chuỗi bài kỹ thuật rời rạc.

## 2. Abstract dự thảo

As AI agents become more capable of acting within operational workflows, the key challenge is no longer only whether they can act, but how much autonomy they should be granted under uncertainty and risk. In AIOps, repeated low-confidence actions, delayed escalation, unnecessary tool calls, and accumulated decision errors can produce substantial operational harm even if individual predictions appear acceptable. Existing systems often rely on static permissions, fixed thresholds, or ad hoc guardrails, which fail to account for cumulative risk over an incident episode.

This paper proposes a risk-budgeted autonomy framework for reliable AIOps agents. The framework treats agent autonomy as a dynamic control variable governed by a remaining risk budget. As the episode evolves, the agent’s allowed action set, escalation rules, and evidence-gathering privileges are adapted according to cumulative risk, belief uncertainty, and incident severity. We formulate autonomy control as a bounded-risk decision problem and evaluate it on AIOps incident episodes using public datasets and simulated cost regimes. Compared with static-autonomy and threshold-based baselines, the proposed framework is expected to achieve better safe success under bounded cumulative risk. The paper contributes a system-level view of autonomy governance for operational AI agents.

## 3. Vấn đề nghiên cứu

### 3.1. Vấn đề thực tế

Trong nhiều hệ AI hiện nay, quyền tự động hóa được cấu hình khá tĩnh:

- agent được quyền làm gì
- khi nào phải escalate
- khi nào được gọi tool

Nhưng trong thực tế, mức tự động hóa nên phụ thuộc vào diễn biến của incident:

- nếu evidence rõ, risk thấp, có thể cho agent tự xử lý nhiều hơn
- nếu evidence mâu thuẫn, risk tăng, phải giảm quyền
- nếu agent đã nhiều lần observe_more mà vẫn chưa rõ, cần chuyển sang escalate

Khoảng trống lớn là:

`quyền tự động hóa hiện chưa được quản trị như một tài nguyên hữu hạn theo ngân sách rủi ro tích lũy.`

### 3.2. Vấn đề khoa học

Paper 4 giải tension:

`automation benefit vs cumulative operational risk`

## 4. Câu hỏi nghiên cứu của Paper 4

### RQ4.1

`Làm thế nào để formal hóa autonomy như một biến điều khiển phụ thuộc risk budget còn lại?`

### RQ4.2

`Làm thế nào để dùng risk budget để giới hạn allowed actions, escalation policy và evidence-gathering behavior của agent?`

### RQ4.3

`Risk-budgeted autonomy có tốt hơn static autonomy và threshold-based autonomy trong tối đa hóa safe success dưới bounded cumulative risk không?`

## 5. Core hypothesis

`Autonomy should be governed dynamically as a function of remaining risk budget, and such governance improves safe operational outcomes compared with static autonomy rules.`

## 6. Định nghĩa autonomy trong paper

Autonomy không nên hiểu là nhị phân `autonomous / not autonomous`.
Paper nên định nghĩa autonomy là:

```text
A_t = set of currently permitted actions and privileges
```

Ví dụ:

- được query tối đa bao nhiêu loại evidence
- có được recommend action hay không
- có được execute simulated remediation hay không
- có được auto-open critical ticket hay không
- có bắt buộc human approval hay không

Autonomy level có thể là:

- Level 0: recommend-only, no autonomous action
- Level 1: evidence gathering only
- Level 2: recommend + limited ticketing
- Level 3: simulated remediation allowed

## 7. Risk budget formalization

Tại thời điểm `t`, còn lại:

```text
B_t = B_0 - Σ_{i=1..t} risk_i
```

Trong đó `risk_i` có thể gồm:

- risk của false action
- risk của delay
- risk của repeated tool use
- risk của conflict unresolved
- risk của late escalation

Autonomy controller:

```text
g(b_t, B_t, s_t) -> A_t
```

Trong đó:

- `b_t`: belief state
- `B_t`: remaining budget
- `s_t`: severity / policy context

## 8. Novelty của Paper 4

1. Quản trị autonomy ở cấp episode thay vì từng threshold cục bộ.
2. Xem autonomy là biến điều khiển động, không phải cấu hình tĩnh.
3. Kết nối uncertainty, severity và cumulative risk vào autonomy control.
4. Đưa ra objective rõ: `safe success under bounded cumulative risk`.

## 9. Phương pháp đề xuất

### 9.1. Policy decomposition

#### Decision policy

Chọn hành động trong action set hiện tại:

```text
π(a_t | b_t, A_t)
```

#### Autonomy controller

Chọn action set cho bước hiện tại:

```text
g(A_t | b_t, B_t, severity_t)
```

### 9.2. Controller options

#### Option A: Rule-based dynamic controller

Ví dụ:

- nếu `B_t > 0.7B_0` và uncertainty thấp -> level 3
- nếu `0.4B_0 < B_t <= 0.7B_0` -> level 2
- nếu `B_t <= 0.4B_0` hoặc severity cao -> level 1 hoặc 0

#### Option B: Learned controller

Học mapping từ state sang autonomy level.

Khuyến nghị:

Để paper khả thi, bắt đầu bằng rule-based dynamic controller + learned controller comparison.

## 10. Autonomy adaptation mechanisms

Khi budget giảm, controller có thể:

- cắt quyền `execute`
- cắt quyền `observe_more` quá nhiều lần
- tăng xác suất `escalate`
- hạ ngưỡng human approval

Khi budget còn dồi dào và uncertainty thấp, controller có thể:

- cho phép observe_more
- cho phép autonomous recommendation
- cho phép limited auto-remediation

## 11. Experimental setup

### 11.1. Incident episodes

Dùng environment của Paper 2/3, nhưng thêm autonomy levels.

Mỗi episode theo dõi:

- hành động nào agent muốn làm
- controller có cho phép không
- risk tích lũy cập nhật ra sao
- episode kết thúc với success/failure/escalation

### 11.2. Baseline autonomy regimes

- Static high autonomy
- Static low autonomy
- Confidence-threshold autonomy
- Severity-only autonomy
- Proposed risk-budgeted dynamic autonomy

## 12. Metrics

### Primary

- `safe success under bounded cumulative risk`
- `budget violation rate`
- `expected operational utility`

### Secondary

- autonomy utilization
- escalation rate
- false automation rate
- average remaining budget at termination
- delayed escalation cost

## 13. Ablations

1. Không dùng cumulative budget, chỉ dùng instantaneous confidence.
2. Không dùng severity.
3. Không dùng uncertainty.
4. Không dùng conflict signal.
5. Không adaptive, chỉ static autonomy.
6. Autonomy 2-level vs 4-level.

## 14. Expected results

Paper kỳ vọng chứng minh:

1. Static high autonomy gây false automation cao.
2. Static low autonomy an toàn nhưng mất hiệu quả.
3. Confidence-only autonomy chưa đủ.
4. Risk-budgeted autonomy đạt trade-off tốt hơn giữa hiệu quả và an toàn.

## 15. Cấu trúc paper đề xuất

### Abstract

- problem of cumulative risk
- propose risk-budgeted autonomy
- bounded-risk gains

### 1. Introduction

- why capability is not enough
- why static permissions fail

### 2. Related Work

- AI autonomy governance
- selective automation
- constrained decision-making

### 3. Problem Formulation

- autonomy levels
- risk budget
- objective

### 4. Method

- autonomy controller
- interaction with action policy
- budget update

### 5. Experiments

- environments
- baselines
- metrics

### 6. Results

- safe success under budget
- autonomy-performance frontier
- ablations

## 16. Reviewer risk và cách phòng thủ

### Risk 1: “Cost/budget model là chủ quan”

Phòng thủ:

- sensitivity analysis
- multiple budget regimes
- Pareto analysis

### Risk 2: “Paper quá giống Paper 2”

Phòng thủ:

- Paper 2 chọn action
- Paper 4 chọn mức autonomy/allowed actions

## 17. Minimum Viable Paper

1. 3 autonomy levels.
2. Rule-based dynamic budget controller.
3. Compare with:
   - static high autonomy
   - static low autonomy
   - confidence-threshold autonomy
4. Metrics:
   - safe success
   - budget violation
   - false automation

## 18. One-sentence pitch

`This paper studies how an AIOps agent’s degree of autonomy should be dynamically adjusted as cumulative operational risk evolves over an incident episode.`

## 19. Kết luận

Paper 4 là paper chiến lược nhất của toàn luận án vì nó đưa ra câu trả lời ở cấp hệ thống:

`AI không chỉ cần quyết định đúng; AI còn phải biết mình đang được phép tự động đến đâu trong một ngân sách rủi ro hữu hạn.`
