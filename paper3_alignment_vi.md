# Paper 3: Safe Alignment Dưới Hard Constraints

## 1. Problem statement

Trong các hệ cyber-physical như smart grid, một policy có utility cao nhưng vi phạm hard constraints vẫn là policy không chấp nhận được. Các phương pháp RLHF chuẩn có thể học preference tốt, nhưng không đủ để bảo đảm tính khả thi vật lý và an toàn vận hành khi ra quyết định trong môi trường nhiều ràng buộc.

## 2. Gap nghiên cứu

Khoảng trống nghiên cứu của literature hiện nay nằm ở giao điểm giữa `RLHF`, `safe RL` và `constrained optimization`. Cụ thể:

- RLHF mạnh ở preference alignment nhưng yếu ở constraint satisfaction
- safe RL mạnh ở constraint control nhưng thiếu cơ chế học preference
- constrained RL mạnh ở tối ưu dưới ràng buộc nhưng không xử lý được tín hiệu human preference hoặc preference surrogate

Trong smart grid đa tác nhân, vẫn thiếu một framework đủ chặt để đồng thời:

- học utility từ preference hoặc đánh giá chuyên gia
- học feasibility/safety từ constraint signals
- cập nhật policy dưới cơ chế tối ưu có ràng buộc rõ ràng

## 3. Câu hỏi nghiên cứu và giả thuyết

### RQ

Liệu một framework `constraint-aware cooperative RLHF` với `dual-head reward model` và `Lagrangian constrained policy optimization` có thể giảm safety violation mà vẫn giữ hiệu quả utility tốt hơn RLHF chuẩn, safe RL và constrained RL baseline hay không?

### Giả thuyết

Việc tách utility learning và safety learning trong reward model, kết hợp với Lagrangian constrained optimization, sẽ làm giảm rõ constraint violations trong khi utility không bị sụp đổ.

## 4. Đóng góp và novelty claim

### Novelty claim một câu

Bài báo đề xuất một framework `constraint-aware cooperative RLHF` cho môi trường đa tác nhân có ràng buộc, trong đó utility và safety được học tách biệt nhưng được tối ưu đồng thời trong một vòng cập nhật policy có kiểm soát an toàn.

### Đóng góp chính

- Thiết kế `dual-head reward model` gồm utility head và safety/feasibility head.
- Thiết kế chiến lược `simulated expert preference + human validation subset`.
- Chọn `Lagrangian constrained policy optimization` làm cơ chế tối ưu chính.
- Đánh giá trade-off utility-safety trong smart grid dưới nhiều nhiễu động hệ thống.

### Phiên bản khả thi nhất của phương pháp

Đây là bài có rủi ro cao nhất trong cả lộ trình. Vì vậy, phiên bản khả thi nhất không nên đặt tham vọng vào RLHF theo nghĩa có lượng lớn human preference thật. Thay vào đó, bài nên được đóng khung thực dụng hơn là:

- `preference-guided constrained policy optimization`
- preference chủ yếu đến từ `simulated expert preference`
- human feedback thật chỉ dùng ở `validation subset`

Cách framing này vẫn giữ được linh hồn của alignment, nhưng giảm mạnh rủi ro dữ liệu và chi phí gán nhãn.

### Cải tiến gì và cải tiến ở đâu

- So với RLHF chuẩn: thêm hard-constraint awareness.
- So với safe RL: thêm preference learning.
- So với constrained RL: thêm reward modeling theo preference và cooperative update logic.
- So với CoRLHF nguyên bản: thêm explicit safety head và constrained optimization logic.

## 5. Phương pháp đề xuất

### 5.1. Domain neo

- Smart Grid

### 5.2. Dữ liệu và tín hiệu học

#### Dữ liệu môi trường

- IEEE 30 bus
- IEEE 118 bus
- IEEE 300 bus
- dữ liệu EVN nếu đủ sạch và công bố được

#### Preference labels

Preference labels được xây theo chiến lược hai tầng:

- `simulated expert preference`: sinh từ expert rules, utility objective và ranking trajectory trong simulator
- `human validation subset`: tập con trajectory được chuyên gia hoặc người vận hành đánh giá để kiểm tra chất lượng preference mô phỏng

#### Safety labels

Safety labels lấy trực tiếp từ hard constraints:

- line overload
- power balance violation
- safety margin violation
- infeasible dispatch/action

### 5.3. Kiến trúc

#### Dual-head reward model

- `utility head`: học giá trị hành vi theo preference
- `safety head`: học xác suất hoặc mức độ vi phạm feasibility/safety

#### Cooperative update

Policy và reward model được cập nhật theo vòng lặp phối hợp, nhưng policy update bị ràng buộc bởi Lagrangian constraint term.

#### Tối ưu chính

Proposal khóa lựa chọn chính là `Lagrangian constrained policy optimization`. Đây là điểm cần giữ cố định để bài đủ chặt và tránh cảm giác “liệt kê nhiều khả năng”.

## 6. So sánh với literature

### Baseline families

- RLHF chuẩn
- constrained RL
- safe RL
- CoRLHF không safety head
- handcrafted penalty reward optimization

### Điểm literature dễ bị phản biện

- Nếu preference labels không đủ rõ, bài sẽ bị hỏi về tính hợp lệ của RLHF.
- Nếu utility sụp đổ quá mạnh khi giảm violations, bài sẽ mất giá trị thực tế.
- Nếu không tách được utility head và safety head bằng ablation, novelty sẽ yếu.

## 7. Thiết kế thực nghiệm

### Metrics

- safety violation rate
- constraint satisfaction rate
- profit/return
- robustness under disturbances
- stability under load shifts

### Baselines

- RLHF chuẩn
- constrained RL
- safe RL
- CoRLHF không safety head

### Ablations

- bỏ safety head
- bỏ cooperative reward refinement
- bỏ Lagrangian constrained optimization
- chỉ dùng preference feedback

### Stress tests

- demand spike
- renewable fluctuation
- line congestion
- noisy preference annotations

## 8. Điều kiện để đủ sức Q1

### Đánh giá thực dụng hiện tại

- Khả thi triển khai: `5.5/10`
- Độ mới học thuật: `8/10`
- Tiềm năng Q1: `6.5/10`

### Khuyến nghị chiến lược

Đây là bài có novelty hấp dẫn nhưng rủi ro cao nhất. Nếu muốn làm thật và vẫn giữ cửa Q1, cần hạ tham vọng ở phần human feedback, tăng độ chặt ở preference surrogate và tập trung vào utility-safety trade-off. Nếu không khóa chiến lược dữ liệu rõ, bài này rất dễ bị sa vào tranh luận về tính hợp lệ hơn là được đánh giá trên contribution thật.

### Venue family phù hợp

- Expert Systems with Applications
- Information Sciences
- venue AI for cyber-physical decision making nếu framing đủ mạnh

### Điều kiện đủ tối thiểu

- preference data strategy phải rõ và defendable
- phải chứng minh utility không sụp đổ khi tăng kiểm soát an toàn
- phải có baseline mạnh từ cả RLHF lẫn safe RL
- phải có một câu chuyện rõ về utility-safety trade-off
- nên xem `human validation subset` là thành phần bắt buộc tối thiểu để giữ tính thuyết phục học thuật

### Điều gì sẽ kéo bài xuống Q2/Q3

- preference labels mơ hồ
- chỉ giảm violations bằng cách làm policy quá bảo thủ
- không hơn được constrained RL mạnh
- thiếu robustness test dưới disturbances

### Cách làm thực tế nhất

- Không khởi đầu bằng EVN thật nếu dữ liệu chưa sạch.
- Dùng IEEE bus làm xương sống thực nghiệm.
- Chỉ khi preference surrogate đã ổn mới mở rộng sang dữ liệu thực hoặc chuyên gia thật.
- Nếu cần đổi framing khi nộp bài, nên nhấn vào `safe preference-guided optimization` hơn là quảng bá RLHF quá mạnh.

## 9. Rủi ro phản biện và cách phòng thủ

### Phản biện 1

“Đây không còn là RLHF thực sự nếu preference phần lớn là mô phỏng.”

### Phòng thủ

Nhấn mạnh:

- đây là preference surrogate có kiểm chứng
- có human validation subset
- mục tiêu là adaptation phù hợp với bối cảnh cyber-physical, nơi chi phí lấy large-scale human preference rất cao

### Phản biện 2

“Bài này chỉ là safe RL gắn thêm reward model.”

### Phòng thủ

Chỉ ra novelty nằm ở:

- tách utility head và safety head
- cooperative update giữa reward model và policy
- preference-aware constrained optimization

### Phản biện 3

“Safety tăng nhưng utility giảm mạnh.”

### Phòng thủ

Thiết kế rõ utility-safety frontier, báo cáo trade-off thay vì chỉ report một điểm.

## 10. Vai trò trong luận án tiến sĩ

Paper 3 cung cấp `safe policy update`, tức lớp đảm bảo rằng quyết định tối ưu không vi phạm hard constraints. Đây là thành phần bắt buộc để CAMAS có ý nghĩa trong các môi trường công nghiệp rủi ro cao.

### Mapping vào luận án

- một chương hoặc cụm nội dung về safe alignment
- lớp kiểm soát an toàn của CAMAS
- điều kiện cần trước khi chứng minh kiến trúc closed-loop tổng thể
