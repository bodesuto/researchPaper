# Paper 2: Adaptive Coordination Cho Scheduling Động

## 1. Problem statement

Trong các bài toán scheduling động nhiều thực thể như FJSP, quyết định tối ưu không chỉ phụ thuộc vào trạng thái cục bộ của từng máy hay từng job, mà còn phụ thuộc vào cấu trúc phụ thuộc đang thay đổi giữa operation, machine, deadline và tình trạng nhiễu động của hệ thống. Các policy phẳng hoặc biểu diễn tĩnh thường không theo kịp độ phức tạp này, dẫn đến điều phối kém linh hoạt và giảm chất lượng vận hành.

## 2. Gap nghiên cứu

Literature hiện có hai xu hướng chính. Một là các phương pháp MARL hoặc RL mạnh về tối ưu hành động nhưng yếu ở biểu diễn cấu trúc phụ thuộc động. Hai là các phương pháp graph-based scheduling mạnh về biểu diễn cấu trúc nhưng chưa khai thác đủ tốt phân cấp quyết định và thích ứng theo ngữ cảnh. Khoảng trống nghiên cứu nằm ở việc chưa có nhiều framework đồng thời kết hợp:

- quyết định phân cấp
- biểu diễn đồ thị dị thể theo thời gian
- action/reward đa chiều
- cơ chế thích ứng biểu diễn theo ngữ cảnh

## 3. Câu hỏi nghiên cứu và giả thuyết

### RQ

Liệu một framework `hierarchical context-adaptive multi-agent coordination` kết hợp graph encoder, MD-MDP và LRMP có thể cải thiện chất lượng điều độ và độ bền trước nhiễu động tốt hơn flat MARL, graph-only coordination và rule-based scheduling hay không?

### Giả thuyết

Việc kết hợp `Hierarchical MARL + graph-based state modeling + MD-MDP + LRMP` sẽ giúp cải thiện makespan, tardiness, machine utilization và robustness trong FJSP động so với các baseline không có phân cấp hoặc không có biểu diễn thích ứng theo ngữ cảnh.

## 4. Đóng góp và novelty claim

### Novelty claim một câu

Bài báo đề xuất một framework điều phối đa tác nhân phân cấp thích ứng theo ngữ cảnh, trong đó biểu diễn đồ thị dị thể theo thời gian và LRMP được dùng để hỗ trợ ra quyết định scheduling động dưới ràng buộc đa chiều.

### Đóng góp chính

- Đề xuất khung `Hierarchical MARL` cho tách quyết định chiến lược và tác nghiệp.
- Dùng `heterogeneous/temporal graph encoder` để nắm phụ thuộc động giữa job, operation, machine và trạng thái hệ thống.
- Dùng `MD-MDP` để mô hình hóa action/reward đa chiều.
- Dùng `LRMP` như tầng biểu diễn thích ứng theo ngữ cảnh.

### Phiên bản khả thi nhất của phương pháp

Để tăng xác suất làm thật và publish được, bài này nên được triển khai theo hai tầng ưu tiên:

- `Tầng cốt lõi bắt buộc`: Hierarchical MARL + graph encoder
- `Tầng tăng cường có điều kiện`: LRMP và MD-MDP

Nếu nguồn lực thực nghiệm hoặc thời gian huấn luyện bị hạn chế, bài vẫn có thể đứng được với novelty chính là `hierarchical graph-based coordination`. LRMP và MD-MDP chỉ nên được giữ khi chúng tạo ra chênh lệch đủ rõ trong ablation.

### Cải tiến gì và cải tiến ở đâu

- So với flat MARL: tách được chiến lược và tác nghiệp.
- So với graph-based scheduling thuần túy: thêm policy phân cấp và biểu diễn thích ứng.
- So với MDP chuẩn: action/reward được mô hình hóa phù hợp hơn với bản chất scheduling đa chiều.
- So với attention/graph encoder riêng lẻ: bổ sung một logic điều phối hoàn chỉnh chứ không chỉ nâng encoder.

## 5. Phương pháp đề xuất

### 5.1. Domain neo

- FJSP/Scheduling

### 5.2. Mô hình hóa bài toán

Trạng thái hệ thống được biểu diễn bằng một heterogeneous graph gồm:

- nodes cho jobs
- nodes cho operations
- nodes cho machines
- temporal state features cho trạng thái hệ thống đang thay đổi

Quan hệ giữa các node thể hiện:

- thứ tự công đoạn
- tính tương thích giữa operation và machine
- phụ thuộc tài nguyên
- trạng thái bận/rỗi và nhiễu động của máy

### 5.3. Kiến trúc

#### Graph encoder

Graph encoder trích xuất biểu diễn ngữ cảnh từ cấu trúc scheduling hiện tại.

#### LRMP

LRMP được đặt sau graph encoder để làm cho biểu diễn thay đổi theo ngữ cảnh thay vì giữ embedding cố định. Đây là điểm cần nhấn mạnh để tránh bài bị hiểu là chỉ “graph + attention”.

#### Hierarchical policy

- `Master policy`: chọn chiến lược, subgoal hoặc dạng ưu tiên điều độ
- `Worker policies`: chọn hành động gán việc cụ thể

#### MD-MDP

MD-MDP dùng để mô hình hóa:

- nhiều chiều action
- nhiều chiều reward
- trade-off giữa tiến độ, tài nguyên và độ ổn định

## 6. So sánh với literature

### Baseline families

- heuristic dispatch rules
- PPO hoặc DQN
- flat MARL
- hierarchical MARL không graph
- graph RL không LRMP
- graph coordination không MD-MDP

### Điểm literature dễ bị phản biện

- Nếu chỉ ghép graph encoder với MARL, novelty sẽ yếu.
- Nếu không chứng minh được vai trò riêng của hierarchy và LRMP, bài sẽ dễ bị xem là incremental.
- Nếu dùng metric mơ hồ, bài sẽ mất tính thuyết phục.

## 7. Thiết kế thực nghiệm

### Dữ liệu

- Barnes FJSP
- dynamic FJSP instances nếu có
- có thể tự tạo perturbation scenarios nếu benchmark công khai chưa đủ

### Metrics

- makespan
- total tardiness
- machine utilization
- robustness under perturbation
- convergence stability

Không dùng các metric mơ hồ như HHS làm headline metric.

### Baselines

- heuristic dispatch rules
- PPO/DQN
- flat MARL
- hierarchical MARL không graph
- graph RL không LRMP

### Ablations

- bỏ hierarchy
- bỏ graph encoder
- bỏ MD-MDP
- bỏ LRMP
- bỏ temporal modeling

### Stress tests

- machine breakdown
- urgent order insertion
- processing delay
- dynamic deadline shift

## 8. Điều kiện để đủ sức Q1

### Đánh giá thực dụng hiện tại

- Khả thi triển khai: `7/10`
- Độ mới học thuật: `7.5/10`
- Tiềm năng Q1: `7.5/10`

### Khuyến nghị chiến lược

Đây là bài có tiềm năng tốt nhưng dễ bị quá tải thành phần. Hướng đi an toàn là chốt novelty quanh `hierarchical graph-based coordination`, sau đó xem LRMP và MD-MDP là thành phần tăng cường. Nếu ôm đủ cả bốn khối như nhau, bài sẽ khó làm sâu và dễ bị reviewer xem là tổ hợp kỹ thuật.

### Venue family phù hợp

- Expert Systems with Applications
- Information Sciences
- Knowledge-Based Systems nếu phần methodological framing đủ mạnh

### Điều kiện đủ tối thiểu

- phải chứng minh được novelty không chỉ là tổ hợp graph + MARL
- phải có ablation tách vai trò của từng thành phần
- phải có perturbation scenarios đủ nặng để chứng minh adaptation
- phải có baseline mạnh và công bằng
- nên ưu tiên chứng minh rõ lợi ích của hierarchy trước, rồi mới đến lợi ích của LRMP/MD-MDP

### Điều gì sẽ kéo bài xuống Q2/Q3

- chỉ hơn heuristic nhẹ nhưng không hơn flat MARL mạnh
- không có perturbation test
- LRMP không tạo ra chênh lệch thực sự
- bài chỉ giống một engineering assembly

### Cách làm thực tế nhất

- Giai đoạn đầu chỉ nên khóa một tập benchmark FJSP chuẩn và một tập perturbation scenarios.
- Nếu chi phí huấn luyện quá lớn, ưu tiên giảm số biến thể mô hình hơn là giữ quá nhiều thành phần nhưng thí nghiệm nông.
- Không dùng quá nhiều metric phụ; headline nên xoay quanh makespan, tardiness và robustness.

## 9. Rủi ro phản biện và cách phòng thủ

### Phản biện 1

“Bài này chỉ ghép graph encoder với hierarchical MARL.”

### Phòng thủ

Chỉ ra cấu trúc mới nằm ở chỗ:

- graph encoder phục vụ hierarchy
- MD-MDP mô hình hóa bản chất action/reward đa chiều
- LRMP làm biểu diễn thích ứng theo ngữ cảnh

### Phản biện 2

“Không rõ phần nào tạo ra cải thiện chính.”

### Phòng thủ

Dùng ablation tách riêng:

- hierarchy
- graph encoder
- MD-MDP
- LRMP

### Phản biện 3

“Kết quả không đủ giá trị thực tế.”

### Phòng thủ

Đưa perturbation scenarios gần với sản xuất động thực hơn và nhấn mạnh lợi ích vận hành như giảm tardiness, tăng utilization.

## 10. Vai trò trong luận án tiến sĩ

Paper 2 cung cấp `context-adaptive action generation`, tức khả năng ra quyết định phối hợp hiệu quả từ grounded state. Đây là lớp trung gian quan trọng nối từ nhận thức có grounding sang điều phối có chất lượng trong môi trường động.

### Mapping vào luận án

- một chương hoặc cụm nội dung về adaptive coordination
- một chứng minh rằng grounded state có thể được biến thành action chất lượng cao
- một thành phần lõi trước khi đưa constraint-aware alignment vào hệ
