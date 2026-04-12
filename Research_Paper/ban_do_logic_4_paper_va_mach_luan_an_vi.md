# Bản Đồ Logic 4 Paper Và Mạch Luận Án

## 1. Mục tiêu của tài liệu

Tài liệu này trả lời bốn câu hỏi thực dụng:

1. bốn paper liên kết với nhau như thế nào
2. paper nào là lõi học thuật mạnh nhất
3. paper nào có rủi ro cao hơn
4. nếu cần thu hẹp để tăng xác suất `pass PhD`, nên gộp hoặc ưu tiên paper nào

Mục tiêu không phải mô tả lại từng paper, mà là làm rõ:

`toàn bộ luận án có thực sự là một trục khoa học thống nhất hay chỉ là 4 bài ghép lại`

## 2. Câu hỏi lớn xuyên suốt của luận án

Toàn bộ luận án nên được kể bằng một câu hỏi lớn duy nhất:

`Làm thế nào để Agentic AI có thể ra quyết định vận hành IT một cách đáng tin cậy khi trạng thái hệ thống chỉ được quan sát một phần, bằng chứng thường nhiễu và mâu thuẫn, và mức tự động hóa phải luôn nằm trong giới hạn rủi ro chấp nhận được?`

Từ câu hỏi lớn đó, 4 paper xuất hiện như 4 tầng logic kế tiếp nhau:

1. nếu không biết trạng thái đủ đáng tin, không thể quyết định đúng
2. nếu trạng thái chưa chắc chắn, phải biết khi nào nên hành động hay chưa
3. nếu evidence thay đổi theo thời gian, phải biết khi nào cần cập nhật workflow
4. nếu agent ngày càng có quyền hơn, phải biết giới hạn quyền đó bằng ngân sách rủi ro

## 3. Bản đồ logic 4 paper

```text
Paper 1: Belief-State Grounding
    ↓
Paper 2: Action Gating under Uncertainty
    ↓
Paper 3: Event-Triggered Workflow Coordination
    ↓
Paper 4: Risk-Budgeted Autonomy
```

Đây là mạch logic mạnh nhất vì:

- Paper 1 tạo ra `state object`
- Paper 2 dùng state object để chọn hành động
- Paper 3 dùng state và action policy để quyết định khi nào phải replanning
- Paper 4 quản trị toàn bộ autonomy của agent trong suốt episode

Nếu viết đúng, đây không phải 4 bài độc lập.
Đây là:

`4 câu trả lời cho 4 lớp của cùng một bài toán closed-loop decision-making`

## 4. Vai trò riêng của từng paper

## 4.1. Paper 1 là paper nền

### Chức năng

Paper 1 tạo ra đối tượng trung tâm của toàn luận án:

`belief state`

### Nó trả lời

- agent đang tin điều gì?
- agent chắc đến mức nào?
- bằng chứng nào ủng hộ?
- bằng chứng nào mâu thuẫn?

### Vì sao nó quan trọng

Nếu không có Paper 1:

- Paper 2 sẽ chỉ là thresholding trên score
- Paper 3 sẽ thiếu state để trigger replanning
- Paper 4 sẽ thiếu signal để quản trị autonomy

### Kết luận

`Paper 1 là nền bắt buộc.`

## 4.2. Paper 2 là paper bản lề

### Chức năng

Paper 2 chuyển từ `nhận thức trạng thái` sang `quyết định hành động`.

### Nó trả lời

- khi nào nên act?
- khi nào nên defer?
- khi nào nên observe_more?
- khi nào nên escalate?

### Vì sao nó quan trọng

Đây là chỗ toàn luận án bắt đầu thật sự trở thành `agentic`.
Trước đó mới là state inference. Từ Paper 2 trở đi mới là decision-making.

### Kết luận

`Paper 2 là cầu nối giữa perception và autonomy.`

## 4.3. Paper 3 là paper về dynamics

### Chức năng

Paper 3 thêm yếu tố thời gian và biến động workflow.

### Nó trả lời

- khi nào evidence mới đủ mạnh để đổi kế hoạch?
- khi nào nên giữ workflow hiện tại?
- làm sao tránh replanning quá nhiều?

### Vì sao nó có giá trị

Paper này làm cho luận án thực sự trở thành `closed-loop`.
Nếu chỉ có Paper 1 và 2, hệ vẫn gần với one-shot decision.
Paper 3 đưa vào:

- dynamic evidence
- replanning
- workflow adaptation

### Điểm yếu

Đây là paper có novelty dễ bị nghi ngờ nhất nếu viết không chặt.
Reviewer rất dễ nói:

- đây chỉ là orchestration
- đây chỉ là engineering workflow

### Kết luận

`Paper 3 có giá trị đẹp về mặt mạch luận án, nhưng là paper rủi ro cao nhất.`

## 4.4. Paper 4 là paper identity của luận án

### Chức năng

Paper 4 đưa ra đóng góp cấp hệ thống:

`risk-budgeted autonomy`

### Nó trả lời

- agent nên được phép tự động đến đâu?
- khi nào phải giảm quyền?
- khi nào phải buộc human approval?

### Vì sao nó quan trọng

Paper 4 làm cho luận án có bản sắc rõ:

`đề tài này không chỉ nói về agent, mà nói về governance of agent autonomy under risk`

### Kết luận

`Paper 4 là paper chiến lược mạnh nhất về mặt định vị học thuật.`

## 5. Phụ thuộc giữa các paper

### 5.1. Phụ thuộc logic

- Paper 2 phụ thuộc logic vào Paper 1
- Paper 3 phụ thuộc logic vào Paper 1 và một phần Paper 2
- Paper 4 phụ thuộc logic vào Paper 1 và Paper 2, nhưng không nhất thiết phụ thuộc chặt vào Paper 3

### 5.2. Phụ thuộc thực nghiệm

Thực tế triển khai nên như sau:

- Paper 1 tạo state
- Paper 2 dùng state để ra action
- Paper 4 dùng state + action traces để quản trị autonomy
- Paper 3 có thể dùng lại environment của Paper 2 nhưng thêm dynamic replanning

### Kết luận quan trọng

`Paper 4 không nhất thiết phải chờ Paper 3 hoàn chỉnh mới làm được.`

Điều này rất quan trọng để giảm rủi ro tiến độ.

## 6. Xếp hạng mức độ quan trọng

Nếu xếp theo độ quan trọng đối với toàn luận án:

1. `Paper 1`
2. `Paper 4`
3. `Paper 2`
4. `Paper 3`

Giải thích:

- Paper 1 tạo nền representation
- Paper 4 tạo identity học thuật
- Paper 2 tạo bước chuyển sang agentic decisions
- Paper 3 đẹp nhưng không phải điểm sống còn nếu buộc phải thu hẹp

## 7. Xếp hạng mức độ rủi ro

Nếu xếp theo rủi ro nghiên cứu:

1. `Paper 3` là rủi ro cao nhất
2. `Paper 4`
3. `Paper 2`
4. `Paper 1` là an toàn nhất

Giải thích:

### Paper 1

- có dataset rõ
- có benchmark rõ
- có novelty tương đối sạch

### Paper 2

- có thể xây từ output của Paper 1
- decision problem rõ
- baseline tương đối dễ

### Paper 4

- mạnh nhưng phụ thuộc vào cost model và formalization
- dễ bị hỏi “risk budget có chủ quan không?”

### Paper 3

- dễ bị xem là orchestration
- khó làm novelty mạnh nếu không formalize tốt

## 8. Nếu cần gộp để tăng xác suất pass

### Phương án an toàn nhất

Giữ nguyên:

- Paper 1
- Paper 2
- Paper 4

Và xử lý Paper 3 theo một trong hai cách:

1. giữ nguyên nếu nó có kết quả tốt
2. gộp một phần vào Paper 2 hoặc Paper 4 nếu novelty không đủ mạnh

### Cách gộp khả thi

#### Gộp Paper 3 vào Paper 2

Khi đó Paper 2 trở thành:

`Uncertainty-Aware Action Gating and Dynamic Replanning for AIOps Agents`

Hợp nếu muốn nhấn mạnh decision-making theo chuỗi.

#### Gộp Paper 3 vào Paper 4

Khi đó Paper 4 trở thành:

`Risk-Budgeted Closed-Loop Autonomy for Dynamic AIOps Workflows`

Hợp nếu muốn coi replanning là một phần của autonomy governance.

### Kết luận

`Paper 3 là paper linh hoạt nhất, có thể tách hoặc gộp.`

## 9. Lộ trình triển khai an toàn nhất

Nếu mục tiêu là:

- có kết quả sớm
- giảm rủi ro
- tăng khả năng pass

thì nên đi theo thứ tự:

### Giai đoạn 1

Làm thật chắc:

- Paper 1

### Giai đoạn 2

Dựa trên Paper 1, làm:

- Paper 2

### Giai đoạn 3

Song song hoặc ngay sau đó:

- Paper 4

### Giai đoạn 4

Cuối cùng mới quyết định:

- Paper 3 sẽ giữ độc lập hay gộp

## 10. Câu chuyện trình bày với giáo sư và hội đồng

Bạn nên kể luận án bằng đúng logic này:

### Câu hỏi lớn

`AI agent trong AIOps nên được tin đến mức nào để ra quyết định vận hành trong môi trường quan sát không đầy đủ và rủi ro cao?`

### 4 lớp câu trả lời

1. trước hết agent phải có `belief state` đáng tin
2. từ belief state đó, agent phải biết khi nào nên act/defer/observe/escalate
3. nếu evidence thay đổi, workflow phải biết khi nào cần cập nhật
4. trên toàn bộ quá trình, quyền tự động hóa phải bị giới hạn bởi ngân sách rủi ro

Đây là logic rất mạnh vì nó không phải:

- 4 bài về 4 thuật toán khác nhau
- 4 bài về 4 use case khác nhau

Mà là:

`4 lớp của một hệ decision-making đáng tin cậy`

## 11. Điểm cần giữ để luận án không bị loãng

Có 5 nguyên tắc cần giữ:

1. `AIOps là domain duy nhất`
Không mở rộng sang manufacturing hay cybersecurity trong phần thực nghiệm chính.

2. `Belief state là object trung tâm`
Không để mỗi paper dùng representation khác nhau.

3. `Safe success under bounded risk là metric triết lý chung`
Mỗi paper đo metric riêng, nhưng triết lý chung phải thống nhất.

4. `Paper 4 là nơi chốt identity`
Đừng để Paper 4 thành một bài integration mơ hồ.

5. `Paper 3 là optional-strong, không phải mandatory-weak`
Nếu không đủ mạnh thì gộp, không cố giữ chỉ để đủ 4 bài.

## 12. Kịch bản tốt nhất

Kịch bản tốt nhất cho toàn luận án là:

- Paper 1 publish được như một bài nền về state grounding
- Paper 2 publish được như một bài decision policy dưới bất định
- Paper 4 publish được như một bài autonomy governance dưới risk budget
- Paper 3 nếu mạnh thì giữ độc lập, nếu không thì gộp

Trong kịch bản này, luận án vẫn rất mạnh vì trục chính là:

`state -> action -> autonomy`

Paper 3 chỉ làm cho trục đó động hơn và đẹp hơn.

## 13. Kết luận cuối

Nếu phải nói ngắn gọn nhất:

- `Paper 1` là nền
- `Paper 2` là cầu nối
- `Paper 3` là phần động
- `Paper 4` là bản sắc

Và nếu phải ưu tiên để bảo đảm pass:

`hãy làm thật chắc Paper 1, Paper 2, Paper 4 trước; xem Paper 3 là paper có thể linh hoạt tách hoặc gộp.`
