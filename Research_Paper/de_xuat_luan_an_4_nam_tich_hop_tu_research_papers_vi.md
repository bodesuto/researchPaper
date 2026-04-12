# Đề Xuất Luận Văn Tiến Sĩ 4 Năm Tích Hợp Từ Các Research Paper

## 1. Mục đích

Tài liệu này được đặt ngay trong thư mục `Research_Paper` để dùng cùng lúc với các PDF nguồn. Mục tiêu là:

- ánh xạ từng paper nền vào cấu trúc luận án
- xây một lộ trình 4 năm mạch lạc
- tách thành 4 paper công bố không chồng novelty
- giữ định hướng đủ thực dụng để có thể làm thật

## 2. Các paper trong thư mục này nên được dùng như thế nào

## 2.1. Nhóm nền cho Paper 1

- `Addressing hallucinations in generative AI agents using observability and dual memory knowledge graphs`
- `hgfjhgfjg.pdf` với metadata cho thấy đây là paper về intelligent maintenance

Vai trò:

- cung cấp nền cho `observability grounding`
- cung cấp nền cho `maintenance knowledge`
- khóa domain neo cho bài đầu tiên là `industrial maintenance`

## 2.2. Nhóm nền cho Paper 2

- `MAMHSAN.pdf`
- `Dynamic cognitive cycle-driven multimodal agent for knowledge graph completion`

Vai trò:

- `MAMHSAN` là baseline mạnh cho `graph-based MARL` trong FJSP
- paper MMKGC cung cấp ý tưởng `context-adaptive representation` như LRMP

## 2.3. Nhóm nền cho Paper 3

- `Graph reinforcement learning with auxiliary temporal-graph convolutional ... for unit commitment`

Vai trò:

- cung cấp nền gần domain cho `smart grid / unit commitment`
- phù hợp hơn các paper alignment kiểu LLM nếu mục tiêu là hệ cyber-physical có hard constraints

## 2.4. Paper phụ trợ

- `State recommender system for actuator devices in smart homes: Integration of deep reinforcement learning and implicit feedback`

Vai trò:

- gợi ý cho protocol đánh giá trong môi trường động
- hữu ích cho tư duy phản hồi ngầm và multi-agent adaptation
- không nên là xương sống novelty

## 3. Thesis statement nên dùng

`Các tác nhân AI trong hệ kỹ thuật phức tạp thường thất bại vì nhận thức không được neo vào dữ liệu vận hành, điều phối thiếu cấu trúc thích ứng, và tối ưu policy chưa gắn chặt với hard constraints. Luận án này đề xuất một kiến trúc closed-loop liên kết grounded perception, adaptive coordination và safe alignment để tạo lợi ích hệ thống đo được trong các domain công nghiệp.`

Đây phải là câu chuyện xuyên suốt toàn bộ luận án. Không nên trình bày luận án như một tập hợp kỹ thuật ghép từ nhiều paper nền.

## 4. Cấu trúc 4 paper công bố

## 4.1. Paper 1: Grounded Perception

### Tên hướng

`Observability-Grounded Dual-Memory Knowledge Graph for Hallucination-Aware Industrial Maintenance Agents`

### Novelty trung tâm

`observability-grounded dual-memory reasoning with temporal conflict validation`

### Phải giữ

- semantic memory
- observability memory
- temporal evidence retrieval
- semantic-observability conflict validation
- grounded state scoring

### Không được claim lại

- hierarchical coordination
- safe alignment
- closed-loop gain toàn hệ

### Vai trò

- tạo `grounded_state`
- là bài mạnh nhất để làm trước

## 4.2. Paper 2: Adaptive Coordination

### Tên hướng

`Hierarchical Graph-Based Multi-Agent Coordination for Dynamic Flexible Job Shop Scheduling`

### Novelty trung tâm

`hierarchical graph-based coordination with context-adaptive representation`

### Phải giữ

- heterogeneous graph state
- hierarchical policy
- master-worker decomposition
- context-adaptive embedding
- robustness protocol cho perturbation

### Chỉ giữ nếu ablation chứng minh được

- LRMP trong title hoặc abstract
- MD-MDP như điểm mới

### Không được claim lại

- hallucination reduction
- preference alignment
- integrated architecture

### Vai trò

- tạo `action_candidates`, `context_embedding`, `coordination_confidence`

## 4.3. Paper 3: Safe Alignment Under Hard Constraints

### Tên hướng

`Constraint-Aware Preference-Guided Optimization for Safe Multi-Agent Decision Making in Smart Grid`

### Novelty trung tâm

`tách utility preference và safety feasibility trong constrained policy optimization`

### Phải giữ

- utility head
- safety head
- constrained optimization
- protocol đánh giá dưới hard constraints

### Tránh

- framing như RLHF cho LLM
- phụ thuộc quá mạnh vào human labeling thật

### Vai trò

- tạo `constraint_model` và `policy_update_signal`

## 4.4. Paper 4: Closed-Loop Integration

### Tên hướng

`Closed-Loop Cognitive Multi-Agent Architecture for Operationally Grounded, Adaptive and Safe Industrial Decision Systems`

### Novelty trung tâm

`feedback semantics và closed-loop gain`

### Phải giữ

- interface chuẩn hóa giữa 3 module
- mandatory feedback
- event-triggered re-grounding
- pairwise vs full-loop comparison
- closed-loop gain metric

### Không được claim lại

- novelty sâu của dual-memory
- novelty sâu của graph MARL
- novelty sâu của constrained optimization

### Vai trò

- khóa luận điểm tiến sĩ ở cấp kiến trúc

## 5. Logic tích lũy giữa 4 paper

Luận án chỉ mạch lạc nếu được viết theo chuỗi phụ thuộc sau:

1. `Paper 1` tạo `grounded_state`.
2. `Paper 2` dùng grounded/contextual state để điều phối tốt hơn.
3. `Paper 3` bảo đảm policy tối ưu nhưng vẫn an toàn dưới hard constraints.
4. `Paper 4` chứng minh khi ba lớp đóng vòng thì toàn hệ tốt hơn open-loop.

Chuỗi này nên xuất hiện nhất quán trong proposal, slide, outline bài báo và luận án cuối cùng.

## 6. Lộ trình 4 năm

## 6.1. Năm 1

Mục tiêu:

- khóa proposal
- khóa RQ1-RQ4
- xây dữ liệu và baseline cho Paper 1
- tạo draft mạnh cho Paper 1

Việc chính:

1. Chốt publication mapping.
2. Chốt schema cho semantic memory và observability memory.
3. Làm sạch dữ liệu maintenance.
4. Chạy baseline semantic-only, retrieval-only, dual-memory đơn giản.
5. Phát triển temporal retrieval và conflict validation.
6. Viết draft Paper 1.

Đầu ra bắt buộc:

- proposal ổn định
- literature matrix
- baseline report Paper 1
- draft Paper 1

## 6.2. Năm 2

Mục tiêu:

- nộp Paper 1
- xây lõi Paper 2

Việc chính:

1. Sửa và nộp Paper 1.
2. Chốt benchmark FJSP.
3. Chạy heuristic, flat RL/MARL, MAMHSAN-like baseline.
4. Thiết kế hierarchical controller và graph state.
5. Làm ablation cho context-adaptive representation.
6. Viết draft Paper 2.

Đầu ra bắt buộc:

- bản nộp Paper 1
- baseline table Paper 2
- core model Paper 2
- draft Paper 2

## 6.3. Năm 3

Mục tiêu:

- nộp Paper 2
- xây hướng an toàn cho Paper 3
- chốt interface tích hợp

Việc chính:

1. Nộp Paper 2.
2. Chốt domain smart grid/unit commitment cho Paper 3.
3. Thiết kế preference strategy khả thi:
   - simulated expert preference
   - rule-based preference
   - human validation subset
4. Xây utility head, safety head, constrained update.
5. Chốt interface giữa Perception, Coordination, Alignment.
6. Viết draft Paper 3.
7. Chuẩn bị protocol cho Paper 4.

Đầu ra bắt buộc:

- bản nộp Paper 2
- design note interface CAMAS
- draft Paper 3
- integration protocol draft

## 6.4. Năm 4

Mục tiêu:

- nộp Paper 3
- hoàn thiện Paper 4
- viết và bảo vệ luận án

Việc chính:

1. Nộp Paper 3.
2. Tích hợp 3 module theo interface chuẩn hóa.
3. So sánh:
   - open-loop
   - pairwise integration
   - full CAMAS without feedback
   - full CAMAS with feedback
4. Đo closed-loop gain, robustness, safety, overhead.
5. Viết và nộp Paper 4.
6. Viết bản thảo luận án hoàn chỉnh.

Đầu ra bắt buộc:

- bản nộp Paper 3
- bản nộp Paper 4
- bản thảo luận án

## 7. Thứ tự ưu tiên thực dụng

Nếu mục tiêu là `làm được thật và publish được 4 paper`, nên đi theo thứ tự:

1. `Paper 1`
2. `Paper 2`
3. chuẩn bị `Paper 3`
4. chỉ làm mạnh `Paper 4` khi interface đã rõ

Nếu xét theo rủi ro:

- thấp nhất: `Paper 1`
- trung bình: `Paper 2`
- cao: `Paper 4`
- cao nhất: `Paper 3`

## 8. Các rủi ro cần tránh

1. Để một paper ôm nhiều novelty ngang nhau.
2. Dùng paper nền như danh sách kỹ thuật để ghép cơ học.
3. Viết Paper 3 theo buzzword alignment thay vì bài toán an toàn gần domain.
4. Bắt đầu Paper 4 quá sớm.
5. Không ghi rõ `paper này không claim lại gì`.

## 9. Kết luận

Từ các paper trong thư mục này, cấu hình luận án hợp lý nhất là:

- `Paper 1`: dual-memory observability cho maintenance
- `Paper 2`: hierarchical graph-based coordination cho dynamic FJSP
- `Paper 3`: constraint-aware preference-guided optimization cho smart grid
- `Paper 4`: closed-loop protocol và closed-loop gain

Cấu trúc này vừa mạch lạc về học thuật, vừa có logic tích lũy giữa các năm, và thực tế hơn nhiều so với việc cố gắng mở rộng tất cả paper nền cùng lúc.
