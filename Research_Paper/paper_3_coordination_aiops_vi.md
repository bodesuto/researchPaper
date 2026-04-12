# Paper 3 Chi Tiết

## Tên paper đề xuất

### Tên chính

`Event-Triggered Incident Workflow Coordination for Agentic AIOps`

### Tên thay thế

`When Should an AIOps Agent Replan? Event-Triggered Coordination under Dynamic Evidence`

## 1. Vai trò của Paper 3 trong toàn bộ luận án

Nếu:

- Paper 1 trả lời `agent biết gì`
- Paper 2 trả lời `agent nên làm gì`

thì Paper 3 trả lời:

`Khi bối cảnh thay đổi hoặc evidence mới xuất hiện, agent có nên cập nhật lại toàn bộ workflow xử lý không?`

Đây là paper về coordination và replanning ở cấp workflow.

## 2. Abstract dự thảo

Incident handling in AIOps is inherently dynamic: new logs arrive, traces expose hidden bottlenecks, deployment events alter fault hypotheses, and risk levels shift as time passes. Yet many existing AIOps pipelines assume a fixed processing order or a one-shot decision flow. This creates a mismatch between real incident evolution and the workflow used by agentic systems. Replanning too often wastes computation and increases instability, while replanning too late locks the system into outdated decisions.

This paper proposes an event-triggered coordination framework for agentic AIOps workflows. Instead of executing a static incident pipeline, the framework monitors belief-state changes, evidence conflicts, severity shifts, and risk-budget updates, and triggers workflow re-coordination only when justified. The proposed method decides when to recompute root-cause hypotheses, when to request additional evidence, when to revise remediation suggestions, and when to escalate. We evaluate the framework on dynamic incident episodes derived from public AIOps datasets, comparing it with static pipelines and periodic replanning baselines. The expected contribution is a principled coordination mechanism that improves workflow adaptability while controlling unnecessary replanning overhead.

## 3. Vấn đề nghiên cứu

### 3.1. Vấn đề thực tế

Một workflow incident thực tế có thể bắt đầu như sau:

1. alert về service A
2. metrics gợi ý CPU spike
3. trace mới xuất hiện và chỉ ra bottleneck ở database
4. deployment log cho biết vừa có rollout ở service B

Nếu workflow không cập nhật, hệ có thể bám vào giả thuyết cũ quá lâu.
Ngược lại, nếu cứ mỗi tín hiệu mới lại replan toàn bộ, hệ sẽ bất ổn và tốn chi phí.

Khoảng trống:

`AIOps thiếu một cơ chế quyết định khi nào nên tái phối hợp workflow và khi nào không cần.`

### 3.2. Vấn đề khoa học

Paper 3 giải tension:

`adaptivity vs stability`

## 4. Câu hỏi nghiên cứu của Paper 3

### RQ3.1

`Sự thay đổi nào trong evidence hoặc belief state đủ mạnh để kích hoạt replanning?`

### RQ3.2

`Làm thế nào để điều phối lại các bước anomaly analysis, RCA, remediation và escalation mà không gây oscillation?`

### RQ3.3

`Event-triggered coordination có tốt hơn static workflow và periodic replanning không?`

## 5. Core hypothesis

`Workflow replanning should be triggered by meaningful state or risk changes rather than by fixed schedules or every incoming signal, and such event-triggered coordination improves adaptability without excessive replanning overhead.`

## 6. Coordination problem definition

Workflow state tại thời điểm `t`:

```text
w_t = {current_hypothesis, planned_next_steps, open_queries, candidate_actions, escalation_status}
```

Trigger function:

```text
τ(b_t, b_t-1, r_t, e_t) -> {replan, continue}
```

## 7. Các loại event trigger

### Trigger 1: Belief shift

Khi root-cause hypotheses thay đổi mạnh.

### Trigger 2: Conflict surge

Khi conflict evidence tăng mạnh.

### Trigger 3: Severity jump

Khi severity estimate tăng đột ngột.

### Trigger 4: Risk budget transition

Khi remaining risk budget giảm qua ngưỡng quan trọng.

## 8. Novelty của Paper 3

1. Event-triggered replanning cho AIOps workflows.
2. Trigger dựa trên belief shift, conflict surge, severity jump và risk-budget transition.
3. Cơ chế cân bằng giữa workflow adaptability và replanning overhead.
4. Evaluation trong dynamic incident episodes thay vì static one-shot tasks.

## 9. Phương pháp đề xuất

### 9.1. Workflow graph

Workflow biểu diễn bằng DAG hoặc state machine:

- ingest evidence
- update belief
- request more evidence
- run RCA refinement
- propose action
- escalate

### 9.2. Trigger scoring

```text
S_trigger = αΔbelief + βconflict + γΔseverity + δrisk_transition
```

Nếu `S_trigger > threshold` thì replan.

### 9.3. Anti-oscillation mechanism

Có thể dùng:

- hysteresis threshold
- minimum dwell time
- cooldown window

## 10. Experimental setup

### 10.1. Dynamic incident episodes

1. initial anomaly appears
2. partial evidence arrives
3. new evidence arrives sequentially
4. belief state evolves
5. risk state changes
6. workflow may or may not replan

### 10.2. Sources of dynamic updates

- delayed traces
- delayed deployment logs
- conflicting evidence injection
- severity escalation events

## 11. Baselines

- Static workflow
- Periodic replanning
- Replan-on-every-update
- Severity-only trigger
- Proposed event-triggered coordination

## 12. Metrics

### Primary metrics

- safe success rate
- workflow adaptation gain
- replanning overhead

### Secondary metrics

- number of replans per episode
- unnecessary replans
- missed replans
- mean time to stable decision

## 13. Ablations

1. Chỉ dùng belief shift trigger.
2. Chỉ dùng severity trigger.
3. Không dùng conflict trigger.
4. Không dùng risk-budget trigger.
5. Không có anti-oscillation.

## 14. Expected results

Paper kỳ vọng chứng minh:

1. Static workflow là quá cứng.
2. Replan-on-every-update là quá tốn và bất ổn.
3. Event-triggered coordination đạt trade-off tốt hơn.

## 15. Cấu trúc paper đề xuất

### Abstract

- workflow dynamics in AIOps
- static or periodic replanning is suboptimal
- propose event-triggered coordination

### 1. Introduction

- workflow dynamics in AIOps
- gap of fixed pipelines

### 2. Related Work

- workflow automation in AIOps
- replanning in dynamic systems
- event-triggered control

### 3. Problem Formulation

- dynamic incident workflow
- event triggers
- replanning objective

### 4. Method

- trigger score / trigger policy
- workflow coordinator
- anti-oscillation

### 5. Experiments

- dynamic episodes
- baselines
- metrics

### 6. Results

- adaptation vs stability
- overhead vs benefit

## 16. Reviewer risk và cách phòng thủ

### Risk 1: “Đây chỉ là orchestration engineering”

Phòng thủ:

- formalize trigger problem
- define adaptation-stability trade-off

### Risk 2: “Paper này không cần thiết”

Phòng thủ:

- chứng minh static policy thất bại khi evidence đến trễ/mâu thuẫn

## 17. Minimum Viable Paper

1. Dynamic GAIA-derived incident episodes.
2. Compare:
   - static workflow
   - periodic replanning
   - replan-on-every-update
   - proposed event-triggered coordination
3. Metrics:
   - safe success
   - replanning overhead
   - trigger precision/recall

## 18. One-sentence pitch

`This paper studies when an AIOps agent should replan its incident workflow as new evidence arrives, balancing adaptability against replanning overhead and instability.`
