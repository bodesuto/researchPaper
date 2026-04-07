# Final Novelty Và Q1 Positioning Cho 4 Paper CAMAS

## 1. Mục tiêu của file này

File này chốt lại cách định vị cuối cùng cho 4 paper CAMAS ở mức có thể đưa trực tiếp vào proposal, bài báo hoặc slide trao đổi với giáo viên hướng dẫn. Nội dung tập trung vào:

- bài toán chính xác
- gap chính xác
- novelty statement chính xác
- kỹ thuật cải tiến nên claim
- baseline mạnh nhất
- metric headline
- điều kiện tối thiểu để đủ sức Q1

Nguyên tắc của file này: mỗi paper chỉ được phép có một trục novelty trung tâm. Các kỹ thuật khác chỉ là thành phần hỗ trợ.

## 2. Positioning tổng thể

Roadmap CAMAS không nên được viết là “một hệ thống ghép 8 kỹ thuật từ 8 paper”. Cách định vị đúng là:

- Paper 1 tạo `grounded state` đáng tin cậy.
- Paper 2 dùng `grounded/contextual state` để ra quyết định điều phối thích ứng.
- Paper 3 kiểm soát policy dưới hard constraints.
- Paper 4 chứng minh feedback loop giữa ba lớp tạo lợi ích hệ thống.

Câu chuyện xuyên suốt của luận án:

`Industrial agents fail because they perceive without operational grounding, coordinate without adaptive structure, and align policies without hard-constraint awareness. CAMAS addresses these failures through a closed-loop architecture that links grounded perception, adaptive coordination, and safe alignment.`

Viết tiếng Việt:

`Các tác nhân công nghiệp thất bại vì nhận thức không được neo vào dữ liệu vận hành, điều phối thiếu cấu trúc thích ứng, và căn chỉnh policy chưa xét hard constraints. CAMAS giải quyết ba điểm yếu này bằng một kiến trúc closed-loop liên kết grounded perception, adaptive coordination và safe alignment.`

## 3. Paper 1: Perception

## 3.1. Tên bài nên dùng

`Observability-Grounded Dual-Memory Knowledge Graph for Hallucination-Aware Industrial Maintenance Agents`

Tên tiếng Việt:

`Dual-Memory Knowledge Graph Có Neo Observability Cho Tác Nhân Bảo Trì Công Nghiệp Nhận Biết Hallucination`

## 3.2. Problem statement

Industrial maintenance agents often generate diagnoses or action recommendations that are semantically plausible but operationally unsupported because their reasoning is grounded in static knowledge rather than current logs, traces, and execution histories.

Tiếng Việt:

`Tác nhân bảo trì công nghiệp thường tạo ra chẩn đoán hoặc khuyến nghị hành động có vẻ đúng về mặt ngữ nghĩa nhưng không được hỗ trợ bởi trạng thái vận hành hiện tại, vì quá trình suy luận chủ yếu dựa trên tri thức tĩnh thay vì log, trace và lịch sử thực thi.`

## 3.3. Gap statement

Existing RAG/KG-RAG and dual-memory agent methods improve factual grounding, but they do not sufficiently model temporal validity and semantic-observability conflicts in industrial maintenance environments.

Tiếng Việt:

`Các phương pháp RAG, KG-RAG và dual-memory agent hiện tại cải thiện grounding, nhưng chưa mô hình hóa đủ rõ tính hiệu lực theo thời gian và mâu thuẫn giữa tri thức nền với dữ liệu observability trong môi trường bảo trì công nghiệp.`

## 3.4. Novelty statement cuối cùng

`We propose an observability-grounded dual-memory knowledge graph that combines temporal evidence retrieval with semantic-observability conflict validation to produce traceable grounded states and reduce hallucinated maintenance reasoning.`

Tiếng Việt:

`Bài báo đề xuất một dual-memory knowledge graph có neo observability, kết hợp temporal evidence retrieval với semantic-observability conflict validation để tạo grounded state có thể truy vết và giảm hallucination trong suy luận bảo trì.`

## 3.5. Technical contribution nên claim

Chỉ claim 4 đóng góp:

- `Observability memory`: lưu log, trace, sensor/event history và execution history như evidence có timestamp.
- `Temporal evidence retrieval`: truy xuất evidence theo semantic relevance, temporal validity và source reliability.
- `Semantic-observability conflict validation`: phát hiện mâu thuẫn giữa tri thức nền và bằng chứng vận hành.
- `Grounded state scoring`: sinh `inconsistency_score` và `uncertainty_score`.

Không claim:

- LRMP
- Barlow Twins
- full closed-loop CAMAS
- multi-agent collaboration nếu không thực sự cần

## 3.6. Baseline mạnh nhất

Baseline mạnh nhất phải vượt:

- `KG-RAG/MAKG-like maintenance reasoning baseline`

Các baseline khác:

- semantic-only KG
- vector RAG
- dual-memory without temporal retrieval
- dual-memory without conflict validation

## 3.7. Metric headline

Metric headline:

- `hallucination rate`

Metric phụ:

- evidence grounding score
- factual consistency
- maintenance task success
- inconsistency detection accuracy

## 3.8. Experiment design tối thiểu để Q1

Bạn cần tối thiểu 4 nhóm thực nghiệm:

1. Main comparison với RAG/KG-RAG/MAKG-like baseline.
2. Ablation theo observability memory, temporal retrieval, conflict validation.
3. Stress test theo missing logs, noisy logs, temporal drift, conflicting evidence.
4. Error analysis theo retrieval error, stale evidence, wrong entity mapping, unsupported recommendation.

## 3.9. Điều kiện đủ để Paper 1 có profile Q1

Paper 1 đủ mạnh nếu:

- conflict validation tạo chênh lệch rõ so với dual-memory retrieval thông thường
- hallucination rate được định nghĩa bằng evidence trace rõ
- stress test cho thấy hệ robust khi log thiếu hoặc evidence mâu thuẫn
- baseline gần-domain như MAKG/KG-RAG được so sánh công bằng

## 3.10. Câu cần tránh trong bài

Không viết:

- “We propose a new dual-memory agent.”

Vì dual-memory đã có.

Nên viết:

- “We extend dual-memory agent grounding to industrial maintenance by making temporal observability conflicts first-class validation signals.”

## 4. Paper 2: Coordination

## 4.1. Tên bài nên dùng

`Hierarchical Graph-Based Multi-Agent Coordination for Dynamic Flexible Job Shop Scheduling`

Tên tiếng Việt:

`Điều Phối Đa Tác Nhân Phân Cấp Dựa Trên Graph Cho Dynamic Flexible Job Shop Scheduling`

## 4.2. Problem statement

Dynamic FJSP requires agents to coordinate under changing dependencies among jobs, operations, machines, and disruptions, while flat MARL and graph-only schedulers often lack explicit strategic decomposition.

Tiếng Việt:

`Dynamic FJSP đòi hỏi các tác nhân điều phối dưới các phụ thuộc thay đổi giữa job, operation, machine và nhiễu động, trong khi flat MARL và graph-only scheduling thường thiếu cơ chế phân rã chiến lược rõ ràng.`

## 4.3. Gap statement

Existing graph-attention MARL methods for FJSP, such as MAMHSAN-like frameworks, improve representation and scheduling quality but do not sufficiently separate high-level scheduling strategy from low-level dispatch execution under dynamic perturbations.

Tiếng Việt:

`Các phương pháp graph-attention MARL cho FJSP, điển hình như MAMHSAN, cải thiện biểu diễn và chất lượng scheduling nhưng chưa tách đủ rõ chiến lược điều độ tầng cao khỏi hành động dispatch tầng thấp trong điều kiện nhiễu động động.`

## 4.4. Novelty statement cuối cùng

`We propose a hierarchical graph-based multi-agent coordination framework that separates strategy-level scheduling decisions from dispatch-level actions and uses context-adaptive graph representations to improve robustness in dynamic FJSP.`

Tiếng Việt:

`Bài báo đề xuất một framework điều phối đa tác nhân phân cấp dựa trên graph, tách quyết định chiến lược điều độ khỏi hành động dispatch và dùng biểu diễn graph thích ứng theo ngữ cảnh để tăng robustness trong dynamic FJSP.`

## 4.5. Technical contribution nên claim

Chỉ claim 4 đóng góp:

- `Hierarchical policy`: master policy chọn strategy/subgoal, worker agents chọn dispatch actions.
- `Heterogeneous graph state`: biểu diễn job-operation-machine và resource constraints.
- `Context-adaptive representation`: cập nhật embedding theo machine load, due-date pressure, breakdown state.
- `Dynamic FJSP robustness protocol`: đánh giá dưới machine breakdown, urgent jobs, due-date shift.

Không claim MD-MDP là mới nếu dựa trên MAMHSAN, vì MD-MDP đã được paper nền dùng rất rõ.

LRMP chỉ claim nếu kết quả ablation chứng minh nó tạo chênh lệch có ý nghĩa.

## 4.6. Baseline mạnh nhất

Baseline mạnh nhất phải vượt:

- `MAMHSAN-like graph-attention MARL baseline`

Các baseline khác:

- dispatch rules
- single-agent PPO/DQN
- flat MARL
- graph RL without hierarchy
- hierarchy without graph
- graph + attention without context adaptation

## 4.7. Metric headline

Metric headline:

- `makespan`
- `total tardiness`

Metric phụ:

- machine utilization
- rescheduling cost
- robustness under perturbation
- convergence stability

## 4.8. Experiment design tối thiểu để Q1

Bạn cần:

1. Benchmark FJSP chuẩn.
2. Dynamic FJSP perturbation scenarios.
3. Main comparison với MAMHSAN-like baseline.
4. Ablation:
   - no hierarchy
   - no graph encoder
   - no context adaptation/LRMP
   - flat policy instead of master-worker.
5. Stress test:
   - machine breakdown
   - urgent job arrival
   - due-date shift
   - processing-time uncertainty.

## 4.9. Điều kiện đủ để Paper 2 có profile Q1

Paper 2 đủ mạnh nếu:

- hierarchy chứng minh lợi ích riêng
- dynamic perturbation evaluation tốt
- không bị viết như một mô hình ghép thêm vào MAMHSAN
- MAMHSAN-like baseline được so sánh công bằng

## 4.10. Câu cần tránh trong bài

Không viết:

- “We combine MHSAN, MD-MDP, LRMP and hierarchical MARL.”

Nên viết:

- “We introduce strategic hierarchy into graph-based FJSP coordination and show that explicit strategy-dispatch decomposition improves robustness under dynamic perturbations.”

## 5. Paper 3: Alignment

## 5.1. Tên bài nên dùng

`Constraint-Aware Preference-Guided Multi-Agent Optimization for Safe Smart Grid Control`

Tên tiếng Việt:

`Tối Ưu Đa Tác Nhân Có Hướng Dẫn Preference Và Xét Ràng Buộc Cho Điều Khiển Smart Grid An Toàn`

## 5.2. Problem statement

In smart grid control, a policy that optimizes economic utility but violates physical or safety constraints is unacceptable, while standard RLHF and preference-based methods do not directly enforce feasibility under hard constraints.

Tiếng Việt:

`Trong điều khiển smart grid, một policy tối ưu utility kinh tế nhưng vi phạm ràng buộc vật lý hoặc an toàn là không thể chấp nhận, trong khi RLHF và các phương pháp preference-based chuẩn không trực tiếp bảo đảm feasibility dưới hard constraints.`

## 5.3. Gap statement

Existing CoRLHF-style methods address policy-reward mismatch in LLM alignment, while safe/constrained RL methods address feasibility but lack preference-guided utility modeling. The gap lies in unifying preference learning and hard-constraint control for multi-agent smart grid decision making.

Tiếng Việt:

`Các phương pháp kiểu CoRLHF xử lý mismatch giữa policy và reward model trong LLM alignment, trong khi safe/constrained RL xử lý feasibility nhưng thiếu preference-guided utility modeling. Khoảng trống nằm ở việc kết hợp preference learning với hard-constraint control cho ra quyết định đa tác nhân trong smart grid.`

## 5.4. Novelty statement cuối cùng

`We propose a constraint-aware preference-guided optimization framework that separates utility preference and safety feasibility through a dual-head reward model and performs policy updates using Lagrangian constrained optimization.`

Tiếng Việt:

`Bài báo đề xuất một framework tối ưu có hướng dẫn preference và xét ràng buộc, trong đó utility preference và safety feasibility được tách bằng dual-head reward model, còn policy được cập nhật bằng Lagrangian constrained optimization.`

## 5.5. Technical contribution nên claim

Chỉ claim 4 đóng góp:

- `Dual-head reward model`: utility head và safety/feasibility head.
- `Simulated expert preference protocol`: sinh preference từ expert rules và utility-safety tradeoff.
- `Human validation subset`: dùng một tập nhỏ để kiểm tra preference simulated.
- `Lagrangian constrained policy update`: tối ưu utility dưới safety budget.

Không claim:

- full RLHF với dữ liệu human lớn
- CoRLHF y nguyên
- general LLM alignment

## 5.6. Baseline mạnh nhất

Baseline mạnh nhất phải vượt:

- `constrained RL/safe RL baseline`

Các baseline khác:

- RLHF-like preference optimization without safety head
- handcrafted penalty reward
- dual-head without Lagrangian
- preference-only without safety
- safety-only without preference

## 5.7. Metric headline

Metric headline:

- `safety violation rate`

Metric phụ:

- constraint satisfaction rate
- return/profit
- operating cost
- load shedding
- utility-safety frontier
- robustness under disturbances

## 5.8. Experiment design tối thiểu để Q1

Bạn cần:

1. IEEE 30/118 bus test.
2. Constrained RL baseline.
3. Preference-guided model.
4. Utility-safety tradeoff curve.
5. Ablation:
   - no safety head
   - no utility head
   - no Lagrangian
   - no preference.
6. Stress test:
   - load surge
   - line outage
   - renewable fluctuation
   - demand uncertainty.

## 5.9. Điều kiện đủ để Paper 3 có profile Q1

Paper 3 đủ mạnh nếu:

- không phụ thuộc vào claim RLHF lớn
- vượt constrained RL ở utility-safety tradeoff
- safety violation giảm mà profit không sụp đổ
- simulated preference được kiểm tra bằng human validation subset hoặc expert validation rõ

## 5.10. Câu cần tránh trong bài

Không viết:

- “We apply CoRLHF to smart grid.”

Nên viết:

- “We adapt preference-guided optimization to safety-critical grid control by separating preference utility from feasibility constraints.”

## 6. Paper 4: Integration

## 6.1. Tên bài nên dùng

`CAMAS: A Closed-Loop Cognitive Multi-Agent Architecture with Grounded Perception, Adaptive Coordination, and Safe Alignment`

Tên tiếng Việt:

`CAMAS: Kiến Trúc Đa Tác Nhân Nhận Thức Closed-Loop Với Grounded Perception, Adaptive Coordination Và Safe Alignment`

## 6.2. Problem statement

Perception, coordination, and alignment methods are often developed as independent modules or one-way pipelines, leaving unclear whether feedback among these layers produces measurable system-level benefits.

Tiếng Việt:

`Các phương pháp perception, coordination và alignment thường được phát triển như các module độc lập hoặc pipeline một chiều, khiến chưa rõ việc phản hồi giữa các lớp này có tạo ra lợi ích đo được ở cấp hệ thống hay không.`

## 6.3. Gap statement

Existing agent architectures often lack standardized interfaces, feedback semantics, and controlled open-loop versus closed-loop evaluation protocols for measuring the architectural gain of integrating perception, coordination, and alignment.

Tiếng Việt:

`Các kiến trúc agent hiện tại thường thiếu interface chuẩn hóa, feedback semantics và protocol đánh giá có kiểm soát giữa open-loop và closed-loop để đo lợi ích kiến trúc khi tích hợp perception, coordination và alignment.`

## 6.4. Novelty statement cuối cùng

`We propose a closed-loop cognitive multi-agent integration protocol that standardizes module interfaces and feedback semantics, and demonstrates measurable closed-loop gain over open-loop and pairwise integrations.`

Tiếng Việt:

`Bài báo đề xuất một giao thức tích hợp closed-loop cho hệ đa tác nhân nhận thức, chuẩn hóa interface và feedback semantics giữa các module, đồng thời chứng minh closed-loop gain đo được so với open-loop và tích hợp từng cặp.`

## 6.5. Technical contribution nên claim

Chỉ claim:

- `interface specification`: grounded state, context embedding, constraint model, policy update signal.
- `mandatory feedback`: alignment trả risk-aware prior/policy signal.
- `event-triggered re-grounding`: trigger theo uncertainty, conflict, near-violation.
- `closed-loop gain metric`: đo lợi ích của feedback loop.

Không claim lại:

- dual-memory novelty của Paper 1
- hierarchy novelty của Paper 2
- dual-head reward novelty của Paper 3

## 6.6. Baseline mạnh nhất

Baseline mạnh nhất phải vượt:

- `full pipeline without feedback`

Các baseline khác:

- perception only
- perception + coordination
- coordination + alignment
- pairwise integration
- fixed-interval feedback

## 6.7. Metric headline

Metric headline:

- `closed-loop gain`

Metric phụ:

- end-to-end task success
- safety violation
- robustness
- efficiency/profit
- latency overhead
- compute overhead

## 6.8. Experiment design tối thiểu để Q1

Bạn cần:

1. Open-loop vs closed-loop comparison.
2. Pairwise vs full integration comparison.
3. Feedback ablation:
   - no mandatory feedback
   - no event trigger
   - no uncertainty propagation
   - fixed interval feedback.
4. Domain slice evaluation:
   - maintenance đo grounding
   - FJSP đo coordination adaptation
   - smart grid đo safety-utility tradeoff.
5. Overhead analysis.

## 6.9. Điều kiện đủ để Paper 4 có profile Q1

Paper 4 đủ mạnh nếu:

- full closed-loop vượt full no-feedback
- feedback ablation chứng minh feedback semantics tạo lợi ích riêng
- closed-loop gain có công thức rõ
- overhead chấp nhận được
- bài không overclaim cross-domain generalization

## 6.10. Câu cần tránh trong bài

Không viết:

- “We integrate all modules and achieve a general architecture.”

Nên viết:

- “We show that explicit feedback semantics among grounded perception, adaptive coordination, and safe alignment produce measurable closed-loop gain.”

## 7. Bảng chốt cuối cùng

| Paper | Core novelty | Supporting technique | Must-beat baseline | Headline metric | Q1 condition |
|---|---|---|---|---|---|
| Paper 1 | Conflict-validated observability-grounded dual-memory | Temporal retrieval | KG-RAG/MAKG-like | Hallucination rate | Conflict validation phải tạo gain rõ |
| Paper 2 | Hierarchical graph-based coordination | LRMP/context adaptation | MAMHSAN-like | Makespan/tardiness | Hierarchy phải tạo gain dưới dynamic perturbation |
| Paper 3 | Constraint-aware preference-guided optimization | Dual-head RM + Lagrangian | Constrained RL/safe RL | Safety violation rate | Utility-safety frontier phải tốt hơn baseline |
| Paper 4 | Closed-loop feedback protocol | Event-triggered re-grounding | Full pipeline without feedback | Closed-loop gain | Feedback phải tạo gain riêng và overhead chấp nhận được |

## 8. Đề xuất chiến lược nộp bài

### Nên làm trước

Paper 1.

Lý do:

- dễ khóa dữ liệu hơn
- novelty rõ nhất
- ít phụ thuộc vào module khác
- dễ tạo kết quả sớm

### Nên làm thứ hai

Paper 2.

Lý do:

- có nền MAMHSAN mạnh
- nếu hierarchy tốt sẽ thành contribution rõ
- nối logic tốt từ perception sang decision

### Nên làm sau khi có module

Paper 4.

Lý do:

- cần output từ Paper 1 và 2
- không nên làm khi module chưa ổn

### Nên làm song song nhưng kiểm soát rủi ro

Paper 3.

Lý do:

- rủi ro preference data cao
- cần smart grid/control implementation
- nên chuẩn bị label protocol sớm nhưng không nên đẩy làm paper đầu tiên

## 9. Kết luận cuối cùng

Nếu bạn viết theo hướng này, roadmap CAMAS sẽ có logic Q1 hơn vì mỗi bài có:

- một gap rõ
- một novelty rõ
- một baseline mạnh
- một metric headline
- một điều kiện đủ để thành bài mạnh

Điều quan trọng nhất là không viết CAMAS như một hệ thống có nhiều kỹ thuật. Hãy viết CAMAS như một chuỗi nghiên cứu có logic tích lũy:

- state phải grounded
- decision phải adaptive
- policy phải safe
- loop phải tạo gain đo được

Đó là câu chuyện học thuật mạnh nhất cho luận án của bạn.
