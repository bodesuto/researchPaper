# Executive Summary Gửi 4 Giáo Sư

## 1. Mục tiêu của đề xuất

Đề xuất này trình bày một hướng luận án PhD về AI cho các hệ kỹ thuật phức tạp, với mục tiêu xây dựng một chương trình nghiên cứu đủ mạnh để tạo ra `4 công bố Q1` có logic tích lũy, thay vì 4 bài rời rạc thiếu trục học thuật chung.

Luận án được xây dựng quanh một câu hỏi trung tâm:

`Làm thế nào để các hệ đa tác nhân nhận thức ra quyết định đáng tin cậy trong các miền kỹ thuật phức tạp khi quan sát không chắc chắn, môi trường biến đổi động và policy phải thỏa mãn các ràng buộc vận hành cứng?`

## 2. Luận điểm trung tâm

Luận điểm cốt lõi của luận án là:

`Độ tin cậy trong hệ đa tác nhân công nghiệp không phải là kết quả của từng module mạnh riêng lẻ, mà là kết quả của một kiến trúc closed-loop trong đó nhận thức được neo vào bằng chứng vận hành, điều phối thích ứng với nhiễu động động, và tối ưu policy luôn bị kiểm soát bởi feasibility và safety constraints.`

Từ luận điểm này, luận án đề xuất CAMAS:

- `Grounded Perception`
- `Adaptive Coordination`
- `Safe Alignment`
- `Closed-Loop Integration`

## 3. Vì sao đề tài này quan trọng

Trong nhiều hệ AI công nghiệp hiện nay, failure không đến từ việc mô hình quá yếu, mà đến từ kiến trúc ra quyết định thiếu reliability ở 4 điểm:

1. Hệ suy luận hợp lý về mặt ngữ nghĩa nhưng không đúng với trạng thái vận hành thật.
2. Hệ điều phối tốt trong benchmark tĩnh nhưng phản ứng yếu khi môi trường thay đổi.
3. Hệ tối ưu utility nhưng không thể triển khai vì vi phạm constraints vật lý hoặc an toàn.
4. Các module mạnh riêng lẻ nhưng không phản hồi cho nhau, khiến toàn hệ vẫn hoạt động như pipeline một chiều.

Đây là khoảng trống thực tế lớn trong industrial AI, smart manufacturing và smart grid AI.

## 4. Đóng góp dự kiến của luận án

## 4.1. Paper 1: Grounded Perception

Đóng góp trung tâm:

- phát triển `conflict-validated temporal grounding` cho industrial maintenance agents

Ý tưởng chính:

- dùng observability memory như một nguồn xác thực bắt buộc
- mô hình hóa temporal validity
- phát hiện mâu thuẫn giữa semantic memory và observability evidence

Giá trị khoa học:

- tái định nghĩa hallucination thành `operationally unsupported reasoning`

## 4.2. Paper 2: Adaptive Coordination

Đóng góp trung tâm:

- phát triển `strategy-dispatch decomposed hierarchical coordination` cho dynamic FJSP

Ý tưởng chính:

- tách quyết định chiến lược điều độ khỏi dispatch cục bộ
- dùng graph-based state representation để hỗ trợ phối hợp đa tác nhân

Giá trị khoa học:

- chỉ ra rằng strategic decomposition là nguồn tạo robustness chính dưới perturbation động

## 4.3. Paper 3: Safe Alignment

Đóng góp trung tâm:

- phát triển `constraint-aware preference-guided optimization` cho smart grid control

Ý tưởng chính:

- tách `utility preference` khỏi `safety feasibility`
- dùng dual-head reward modeling
- cập nhật policy bằng constrained optimization

Giá trị khoa học:

- reformulate alignment trong cyber-physical systems thành bài toán utility-feasibility separation, thay vì dùng framing RLHF chung chung

## 4.4. Paper 4: Closed-Loop Integration

Đóng góp trung tâm:

- phát triển `event-triggered closed-loop integration protocol`

Ý tưởng chính:

- chuẩn hóa interface giữa perception, coordination và alignment
- thiết kế feedback semantics
- định nghĩa và đo `closed-loop gain`

Giá trị khoa học:

- chuyển integration từ engineering composition thành một đối tượng nghiên cứu đo lường được

## 5. Tính mạch lạc của 4 paper

Điểm mạnh nhất của đề xuất không nằm ở việc có 4 bài, mà nằm ở việc 4 bài giải cùng một lớp vấn đề từ 4 góc nhìn bổ sung:

- `Paper 1` trả lời: trạng thái nào là đủ đáng tin để ra quyết định?
- `Paper 2` trả lời: khi trạng thái thay đổi, hệ phải điều phối thế nào?
- `Paper 3` trả lời: khi tối ưu policy, làm sao bảo đảm triển khai được?
- `Paper 4` trả lời: phản hồi giữa ba lớp trên có tạo ra lợi ích hệ thống thực sự không?

Vì vậy, luận án không phải là tuyển tập 4 domain papers. Nó là một chương trình nghiên cứu về:

`closed-loop reliability for cognitive multi-agent systems in complex engineering domains`

## 6. Tính mới học thuật

Tính mới của luận án không đến từ việc ghép nhiều kỹ thuật quen thuộc như graph, memory, RL hay multi-agent learning. Tính mới nằm ở 4 reformulation:

1. Hallucination được reformulate thành `operational unsupportedness`.
2. Scheduling adaptation được reformulate thành `strategy-dispatch decomposition`.
3. Alignment được reformulate thành `utility-feasibility separation`.
4. Integration được reformulate thành `measurable feedback semantics`.

Mỗi paper chỉ giữ `một novelty trung tâm`, nhằm tránh loãng đóng góp và tăng sức thuyết phục với reviewer Q1.

## 7. Tính khả thi

Đề xuất này có tính khả thi vì:

- mỗi paper gắn với một problem cụ thể và một benchmark/simulator khả thi
- các đóng góp được triển khai theo thứ tự rủi ro tăng dần
- hai bài đầu có khả năng tạo kết quả sớm hơn, giúp mở đường cho các bài sau
- Paper 4 chỉ được thực hiện khi output interfaces của 3 bài trước đã rõ

Thứ tự triển khai đề xuất:

1. Paper 1
2. Paper 2
3. Paper 3
4. Paper 4

Đây là thứ tự tối ưu để giảm rủi ro cho toàn luận án.

## 8. Rủi ro chính và cách kiểm soát

### Rủi ro 1

Paper 3 có thể bị xem là thiếu dữ liệu preference đủ mạnh.

Giải pháp:

- dùng simulated expert preferences
- dùng human/expert validation subset
- giữ utility-safety frontier là trọng tâm thay vì claim RLHF lớn

### Rủi ro 2

Paper 4 có thể bị xem là integration demo.

Giải pháp:

- định nghĩa closed-loop gain trước thực nghiệm
- dùng feedback ablation rõ
- báo cáo overhead trung thực

### Rủi ro 3

Luận án có thể bị nhìn là quá rộng.

Giải pháp:

- nhấn mạnh đây là một thesis về `mechanisms of reliability`
- ba domain chỉ là các domain slices kiểm chứng cho ba failure modes khác nhau

## 9. Vì sao luận án này xứng đáng ở mức PhD

Luận án này đủ tầm PhD vì nó:

- giải một lớp vấn đề tổng quát, không phải một benchmark hẹp
- có 4 câu hỏi nghiên cứu liên kết logic
- có đóng góp phương pháp luận và đóng góp hệ thống
- có chiều sâu lý thuyết vừa đủ và thực nghiệm đủ mạnh
- có giá trị ứng dụng rõ cho industrial AI, manufacturing AI và smart grid AI

Nói ngắn gọn, đây không phải là đề tài “làm tốt hơn một mô hình”, mà là đề tài:

`xây nguyên lý cho reliable AI-driven decision-making in complex engineering systems`

## 10. Kết luận

Đề xuất CAMAS hướng tới một luận án PhD mạch lạc, có chiều sâu và có khả năng công bố quốc tế cao. Điểm then chốt là luận án không xem perception, coordination, alignment và integration như bốn nhánh độc lập, mà xem chúng là bốn lớp của cùng một câu hỏi khoa học về reliability.

Nếu triển khai đúng kỷ luật:

- mỗi paper giữ một novelty trung tâm
- mỗi paper có baseline mạnh, ablation rõ, stress test rõ
- synthesis cuối luận án được viết ở mức nguyên lý

thì đây là một hướng nghiên cứu đủ mạnh để thuyết phục hội đồng học thuật và có tiềm năng tạo ra một bộ công bố Q1 có chất lượng cao.
