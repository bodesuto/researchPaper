# Bản Đồ Codebase Cho 4 Paper CAMAS

## 1. Mục tiêu của file này

File này trả lời trực tiếp câu hỏi: phương pháp đề xuất của từng paper nên bám vào codebase nào, phần nào có thể tái sử dụng, phần nào bắt buộc phải tự viết mới, và hướng đi nào là khả thi nhất để tránh biến luận án thành một tập hợp ý tưởng khó triển khai.

Điểm cần nói rất rõ ngay từ đầu:

- Trong workspace hiện tại của bạn chưa có repo code nào được kéo về làm nền.
- Các file hiện có mới là PDF bài báo và các file thiết kế nghiên cứu.
- Vì vậy, bản đồ dưới đây là `chiến lược khóa codebase`, chưa phải `xác nhận repo đã tải`.

## 2. Nguyên tắc chọn codebase nền

Mỗi paper chỉ nên có:

- `1 codebase chính`
- tối đa `1 codebase phụ`

Không nên chọn 3-4 codebase cho cùng một paper vì sẽ gây:

- lệch kiến trúc
- tốn thời gian debug
- khó chứng minh novelty của chính bạn
- tăng rủi ro implementation không xong

Nguyên tắc chọn codebase:

1. Chọn codebase gần bài toán nhất, không phải codebase nghe “xịn” nhất.
2. Chọn codebase có baseline rõ và dễ tái lập trước.
3. Chỉ thêm codebase phụ nếu nó giải quyết một khối thật sự thiếu.
4. Mọi phần tạo novelty cho paper phải nằm ở phần code bạn tự kiểm soát.

## 3. Kết luận ngắn cho toàn roadmap

Nếu đi theo hướng khả thi nhất, bạn nên khóa như sau:

- `Paper 1`: không phụ thuộc một codebase học sâu quá lớn; nên tự dựng pipeline trên nền retrieval/KG đơn giản
- `Paper 2`: lấy một codebase `graph RL hoặc scheduling RL` làm xương sống chính
- `Paper 3`: lấy một codebase `constrained RL` hoặc `safe RL` làm xương sống chính, không lấy RLHF-LLM codebase làm nền chính
- `Paper 4`: không có codebase gốc duy nhất; phải tích hợp từ các module bạn đã làm

Đây là điểm rất quan trọng: `Paper 3 không nên lấy codebase CoRLHF cho LLM làm nền triển khai chính`, vì như vậy sẽ làm bài quá xa bối cảnh smart grid và tăng rủi ro implementation.

## 4. Mapping chi tiết cho từng paper

## 4.1. Paper 1: Perception

### 4.1.1. Phương pháp đề xuất đã khóa

- dual-memory knowledge graph
- observability memory
- temporal retrieval
- conflict checking
- grounded output

### 4.1.2. Nên dựa trên bài nào về mặt tư tưởng

Về mặt ý tưởng nghiên cứu, Paper 1 đang neo gần nhất vào nhóm paper về:

- hallucination reduction bằng observability grounding
- agent reasoning có bằng chứng vận hành
- KG/RAG cho industrial reasoning

Trong bộ tài liệu hiện có của bạn, paper gần nhất là:

- `Addressing hallucinations in generative AI agents using observability and ...`

### 4.1.3. Có nên lấy codebase từ paper đó làm nền không

Không nên phụ thuộc hoàn toàn.

Lý do:

- novelty của bạn nằm ở `dual-memory graph structure`, không chỉ ở observability
- paper nền có thể không công khai code hoặc code không khớp data pipeline của bạn
- nếu bám quá chặt codebase agent đầy đủ, bạn sẽ mất thời gian ở phần orchestration thay vì phần phương pháp lõi

### 4.1.4. Cách làm khả thi nhất

Paper 1 nên được làm theo hướng:

- tự dựng codebase chính
- chỉ mượn ý tưởng và giao thức đánh giá từ paper nền

Codebase chính nên gồm các khối:

- module ingest semantic knowledge
- module ingest observability logs
- module temporal retrieval
- module conflict checking
- module scoring và evaluation

### 4.1.5. Phần có thể tái sử dụng

- cách định nghĩa task
- protocol đánh giá grounding/hallucination
- một số retrieval baseline

### 4.1.6. Phần bắt buộc phải tự viết mới

- dual-memory graph schema
- observability memory builder
- conflict checking engine
- inconsistency scoring
- grounded state formatter

### 4.1.7. Kết luận codebase cho Paper 1

- `Codebase chính`: tự xây
- `Codebase phụ`: nếu có, chỉ dùng repo retrieval/KG đơn giản để tiết kiệm thời gian baseline
- `Mức khả thi`: cao nhất trong 4 paper

## 4.2. Paper 2: Coordination

### 4.2.1. Phương pháp đề xuất đã khóa

- hierarchical MARL
- graph encoder
- context adaptation
- LRMP
- MD-MDP là thành phần tăng cường có điều kiện

### 4.2.2. Nên dựa trên bài nào về mặt tư tưởng

Trong bộ tài liệu hiện có, Paper 2 đang gần nhóm bài:

- `Graph reinforcement learning with auxiliary temporal-graph convolutional ...`
- `Hierarchical optimization of virtual power plants via sequential Game-Based Multi-Agent reinforcement learning`
- `MAMHSAN.pdf`

Ba paper này gợi ra ba lớp ý tưởng:

- graph representation
- hierarchical decision making
- attention/context modeling

### 4.2.3. Nên chọn codebase nào làm xương sống

Về mặt chiến lược, chỉ nên chọn `một codebase có graph RL hoặc scheduling RL` làm xương sống chính.

Không nên lấy đồng thời:

- một repo hierarchy
- một repo graph
- một repo attention

rồi ghép lại từ đầu.

### 4.2.4. Cách khóa codebase khả thi nhất

Hướng khả thi nhất là:

- lấy một codebase scheduling RL hoặc graph RL gần FJSP nhất làm `codebase chính`
- tự thêm `hierarchical controller`
- sau đó mới tự thêm `LRMP`

Nếu bạn không tìm được codebase FJSP đủ gần, thứ tự fallback là:

1. codebase graph RL có môi trường scheduling
2. codebase MARL có action/state đủ linh hoạt
3. tự dựng môi trường FJSP tối giản rồi gắn graph encoder

### 4.2.5. Phần có thể tái sử dụng

- environment FJSP
- training loop PPO/DQN/MARL
- graph encoder khởi đầu
- evaluation metrics của scheduling

### 4.2.6. Phần bắt buộc phải tự viết mới

- hierarchical master-worker policy
- context-adaptive representation logic
- LRMP block
- module gắn graph state với scheduling policy của riêng bạn
- ablation framework để chứng minh hierarchy/graph/LRMP

### 4.2.7. Cảnh báo rất quan trọng

`MD-MDP` không nên là lý do để chọn codebase.

Bạn không cần một repo riêng cho MD-MDP. Phần này nên được cài như:

- cách tổ chức state/action/reward
- hoặc một wrapper trên training objective

Nếu chọn codebase chỉ vì nó có vẻ hỗ trợ multi-dimensional reward, bạn rất dễ lạc khỏi bài toán chính.

### 4.2.8. Kết luận codebase cho Paper 2

- `Codebase chính`: graph RL hoặc scheduling RL gần FJSP nhất
- `Codebase phụ`: không bắt buộc; chỉ dùng nếu cần module attention/graph phụ
- `Phần tự viết mới`: hierarchy + LRMP + context adaptation
- `Mức khả thi`: khá tốt nếu khóa scope đúng

## 4.3. Paper 3: Alignment

### 4.3.1. Phương pháp đề xuất đã khóa

- dual-head reward model
- simulated expert preference
- human validation subset
- Lagrangian constrained policy optimization

### 4.3.2. Nên dựa trên bài nào về mặt tư tưởng

Trong bộ tài liệu hiện có, neo tư tưởng gần nhất là:

- `CoRLHF Reinforcement learning from human feedback with cooperative policy-reward optimization for LLMs`

Tuy nhiên cần phân biệt rất rõ:

- paper đó phù hợp để lấy `framing về preference-policy co-optimization`
- paper đó không phù hợp để làm `codebase triển khai chính` cho smart grid

### 4.3.3. Sai lầm phải tránh

Sai lầm lớn nhất là lấy codebase RLHF cho LLM làm nền chính, rồi cố ép sang smart grid.

Lý do:

- khác môi trường
- khác không gian trạng thái/hành động
- khác loại reward
- khác cách đánh giá
- tốn thời gian chuyển đổi mà không tạo ra novelty thật

### 4.3.4. Cách khóa codebase khả thi nhất

Paper 3 nên chọn:

- `Codebase chính`: một repo constrained RL hoặc safe RL cho control/multi-agent environment
- `Codebase phụ`: nếu cần, một implementation reward model đơn giản để học preference ranking

Nói ngắn gọn:

- xương sống phải là `safe/constrained control`
- phần preference/RLHF chỉ là lớp mở rộng phía trên

### 4.3.5. Phần có thể tái sử dụng

- môi trường smart grid hoặc power system simulation
- training loop constrained policy optimization
- baseline safe RL/constrained RL
- evaluation safety metrics

### 4.3.6. Phần bắt buộc phải tự viết mới

- preference data generation pipeline
- dual-head reward model
- utility-safety joint training logic
- bridge giữa reward model và constrained optimizer
- validation protocol giữa simulated preference và human subset

### 4.3.7. Cách triển khai khả thi nhất

Thứ tự đúng nên là:

1. chạy constrained RL baseline trong smart grid
2. thêm safety evaluation sạch
3. thêm utility head
4. thêm safety head
5. thêm preference-guided update

Không được làm ngược lại.

### 4.3.8. Kết luận codebase cho Paper 3

- `Codebase chính`: constrained RL hoặc safe RL cho smart grid/control
- `Codebase phụ`: reward model/preference learner đơn giản
- `Không nên dùng làm codebase chính`: CoRLHF-LLM style implementation
- `Mức khả thi`: trung bình, chỉ ổn nếu giữ framing thực dụng

## 4.4. Paper 4: Integration

### 4.4.1. Phương pháp đề xuất đã khóa

- standardized interfaces
- mandatory feedback
- event-triggered re-grounding
- closed-loop gain

### 4.4.2. Có bài báo/codebase gốc nào để bám không

Không có một codebase duy nhất phù hợp.

Paper 4 bản chất là:

- bài tích hợp kiến trúc
- bài giao thức
- bài chứng minh lợi ích ở mức hệ thống

Vì vậy codebase của Paper 4 phải được xây từ các module bạn đã làm ở Paper 1, 2, 3.

### 4.4.3. Cách làm khả thi nhất

Bạn phải tự xây:

- interface spec
- message/data exchange
- feedback trigger logic
- evaluation harness cho open-loop và closed-loop

### 4.4.4. Phần có thể tái sử dụng

- output modules từ Paper 1
- policy/action modules từ Paper 2
- constraint/reward update từ Paper 3
- các script benchmark và evaluation đã có

### 4.4.5. Phần bắt buộc phải tự viết mới

- integration layer
- protocol orchestration
- feedback controller
- event-triggered re-grounding scheduler
- overhead analysis tools

### 4.4.6. Kết luận codebase cho Paper 4

- `Codebase chính`: tự xây từ 3 module trước
- `Codebase phụ`: không cần nếu interface đã rõ
- `Mức khả thi`: tốt nếu 1 và 2 đã ổn; rủi ro cao nếu làm quá sớm

## 5. Bản đồ thực dụng: bắt đầu từ đâu

Nếu mục tiêu của bạn là làm được thật thay vì tiếp tục mở rộng ý tưởng, hãy khóa thứ tự implementation như sau:

1. `Paper 1`: tự xây codebase perception vì đây là phần khả thi nhất và ít phụ thuộc ngoài.
2. `Paper 2`: chọn một repo graph RL/scheduling RL làm nền, rồi chỉ thêm hierarchy và LRMP.
3. `Paper 3`: chọn một repo constrained RL làm nền, rồi thêm dual-head reward model.
4. `Paper 4`: chỉ bắt đầu khi output interface của 1-2 đã rõ, và tốt nhất là 3 đã có optimizer sạch.

## 6. File nào bạn nên tạo tiếp theo

Để chuyển từ “bản đồ chiến lược” sang “làm thật”, bạn nên tạo tiếp ba file:

- `repo_selection_checklist_vi.md`
- `implementation_bootstrap_plan_vi.md`
- `paper1_data_schema_vi.md`

Vai trò của chúng:

- `repo_selection_checklist_vi.md`: tiêu chí chọn repo nào làm nền, repo nào bỏ
- `implementation_bootstrap_plan_vi.md`: tuần đầu tiên dựng code và baseline cho Paper 1
- `paper1_data_schema_vi.md`: khóa dữ liệu và schema để bắt đầu Paper 1 ngay

## 7. Kết luận cuối

Tóm lại, hiện tại phương pháp đề xuất của bạn đã khá rõ về mặt học thuật, nhưng `chưa khóa codebase thực thi`.

Khóa đúng nhất ở thời điểm này là:

- `Paper 1`: tự xây
- `Paper 2`: bám codebase graph RL/scheduling RL
- `Paper 3`: bám codebase constrained RL/safe RL, không bám RLHF-LLM codebase
- `Paper 4`: tự tích hợp từ các module trước

Đây là phương án khả thi nhất để vừa giữ được novelty của luận án, vừa tránh rơi vào bẫy ghép quá nhiều repo khác nhau.
