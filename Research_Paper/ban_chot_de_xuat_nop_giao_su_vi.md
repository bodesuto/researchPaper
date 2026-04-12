# Bản Chốt Đề Xuất Nghiên Cứu Sinh Tiến Sĩ

## Tên đề tài đề xuất

### Tiếng Việt

`Agentic AI có ngân sách rủi ro cho AIOps: Ra quyết định vận hành IT đáng tin cậy dưới bất định`

### Tiếng Anh

`Risk-Budgeted Agentic AI for Reliable AIOps under Uncertainty`

## 1. Lý do chọn đề tài

Agentic AI đang mở ra khả năng chuyển các hệ AI từ vai trò phân tích thụ động sang vai trò có thể lập kế hoạch, gọi công cụ, tổng hợp bằng chứng, đề xuất hành động và phối hợp với con người trong các quy trình vận hành phức tạp. Trong số các domain ứng dụng, `AIOps / IT Operations` là môi trường phù hợp nhất để nghiên cứu vì:

- đây là bài toán thực tế trong doanh nghiệp
- có dữ liệu công khai đủ để thực nghiệm
- có bài toán quyết định dưới bất định rõ ràng
- phù hợp để đánh giá bounded autonomy và human-in-the-loop

Trong vận hành IT, sự cố thường không xuất hiện dưới dạng một nhãn rõ ràng mà đến từ nhiều tín hiệu không hoàn hảo như logs, alerts, metrics, traces và incident tickets. Do đó, một agent không chỉ cần phát hiện bất thường mà còn phải biết:

- trạng thái hệ thống hiện tại đáng tin đến đâu
- khi nào nên hành động
- khi nào nên trì hoãn hoặc quan sát thêm
- khi nào cần chuyển cho người vận hành
- khi nào quyền tự động hóa phải bị giới hạn bởi rủi ro

Đây chính là khoảng trống mà đề tài này hướng tới.

## 2. Vấn đề nghiên cứu

Phần lớn nghiên cứu hiện tại trong AIOps tập trung vào từng bài toán riêng lẻ như anomaly detection, log analysis, fault localization hoặc root-cause analysis. Tuy nhiên, khi đưa Agentic AI vào vận hành thực, vấn đề không còn là một mô hình dự báo đơn lẻ, mà là cách để agent ra quyết định closed-loop đáng tin cậy dưới điều kiện:

- quan sát không đầy đủ
- dữ liệu nhiễu hoặc mâu thuẫn
- môi trường thay đổi liên tục
- chi phí của hành động sai cao
- yêu cầu kiểm soát mức tự động hóa

Vì vậy, câu hỏi trung tâm của đề tài là:

`Làm thế nào để một Agentic AI ra quyết định vận hành IT đáng tin cậy trong AIOps khi quan sát không đầy đủ, độ bất định cao và hành động tự động phải nằm trong ngân sách rủi ro cho phép?`

## 3. Mục tiêu nghiên cứu

Đề tài hướng tới năm mục tiêu chính:

1. Xây dựng cơ chế `belief-state grounding` từ logs, metrics, traces, alerts và lịch sử sự cố.
2. Thiết kế cơ chế `uncertainty-aware action gating` cho phép agent chọn giữa `act`, `defer`, `observe_more` và `escalate`.
3. Phát triển cơ chế `event-triggered incident workflow coordination` để cập nhật workflow xử lý sự cố khi có bằng chứng mới.
4. Đề xuất bộ điều khiển `risk-budgeted autonomy` để giới hạn mức tự động hóa theo rủi ro tích lũy.
5. Xây dựng giao thức đánh giá nhấn mạnh `safe success under bounded cumulative risk`.

## 4. Câu hỏi nghiên cứu

### RQ1

`Làm thế nào để agent suy ra belief state đáng tin cậy của hệ thống IT từ logs, metrics, traces, alerts và lịch sử sự cố trong điều kiện dữ liệu thiếu, nhiễu, trễ hoặc mâu thuẫn?`

### RQ2

`Khi belief state chưa đủ chắc chắn, agent nên chọn act, defer, observe_more hay escalate như thế nào để cân bằng giữa hiệu quả xử lý và an toàn vận hành?`

### RQ3

`Khi xuất hiện evidence mới hoặc mức rủi ro thay đổi, agent nên tái phối hợp workflow xử lý sự cố như thế nào?`

### RQ4

`Làm thế nào để kiểm soát mức tự động hóa của agent bằng ngân sách rủi ro tích lũy, sao cho tối đa hóa safe success trong khi cumulative risk vẫn được khống chế?`

## 5. Điểm mới dự kiến

Đề tài có tính mới ở bốn điểm:

1. Chuyển trọng tâm từ `agent capability` sang `bounded autonomy under uncertainty`.
2. Đưa ra một khung thống nhất cho Agentic AI trong AIOps thay vì xử lý từng bài toán rời rạc.
3. Kết nối bốn lớp quyết định thường bị tách rời:
   - state grounding
   - action gating dưới bất định
   - coordination theo sự kiện
   - quản trị quyền tự động hóa theo rủi ro
4. Đề xuất tiêu chí đánh giá `safe success under bounded risk`, thay vì chỉ đo accuracy hoặc task success đơn thuần.

## 6. Phương pháp nghiên cứu

Đề tài dự kiến xây dựng một khung bốn lớp:

### 6.1. Belief-State Grounding

Hợp nhất:

- logs
- alerts
- metrics
- traces
- incident history
- runbooks

để tạo ra một `belief state` gồm:

- trạng thái vận hành ước lượng
- uncertainty score
- bằng chứng ủng hộ
- bằng chứng mâu thuẫn
- root cause hypothesis sơ bộ

### 6.2. Uncertainty-Aware Action Gating

Agent chọn giữa:

- `act`
- `defer`
- `observe_more`
- `escalate`

Quyết định này dựa trên uncertainty, severity, chi phí hành động sai, chi phí trì hoãn và phần ngân sách rủi ro còn lại.

### 6.3. Event-Triggered Incident Workflow Coordination

Điều phối và cập nhật workflow giữa:

- anomaly detection
- root-cause analysis
- runbook recommendation
- remediation proposal
- incident ticketing
- human escalation

### 6.4. Risk-Budgeted Autonomy

Bộ điều khiển này theo dõi rủi ro tích lũy trong toàn bộ episode xử lý sự cố và điều tiết mức tự động hóa của agent:

- rủi ro thấp: cho phép tự động xử lý nhiều hơn
- rủi ro trung bình: yêu cầu xác minh hoặc quan sát thêm
- rủi ro cao: bắt buộc escalate hoặc human approval

## 7. Dữ liệu và thực nghiệm

Đề tài có lợi thế là có thể thực nghiệm trên các dữ liệu công khai phù hợp với AIOps:

### Dataset chính

- `GAIA Dataset`
  Nguồn: `https://github.com/CloudWise-OpenSource/GAIA-DataSet`

### Dataset phụ

- `KPI-Anomaly-Detection`
  Nguồn: `https://github.com/NetManAIOps/KPI-Anomaly-Detection`
- `Multi-Source Distributed System Data`
  Nguồn: `https://zenodo.org/records/3484801`
- `Log Anomaly Detection Datasets`
  Nguồn: `https://github.com/ait-aecid/anomaly-detection-log-datasets`

### Thiết lập đánh giá

Mỗi `episode` mô phỏng một tình huống sự cố IT:

1. anomaly hoặc fault xuất hiện
2. agent nhận observability evidence ban đầu
3. agent xây belief state
4. agent chọn hành động
5. môi trường trả về evidence mới, cost và outcome
6. risk budget được cập nhật

### Các baseline so sánh

- reactive agent
- confidence-threshold agent
- anomaly-only pipeline
- RCA-only pipeline
- human-escalate-always policy
- proposed risk-budgeted agent

### Các chỉ số đánh giá chính

- `task success rate`
- `safe success rate`
- `root-cause localization accuracy`
- `mean time to resolution`
- `false automation rate`
- `unnecessary escalation rate`
- `delayed escalation cost`
- `policy violation rate`
- `cumulative risk`

Chỉ số trung tâm là:

`safe success rate under bounded cumulative risk`

## 8. Đóng góp dự kiến

### Đóng góp khoa học

1. Một mô hình `belief-state grounding` cho Agentic AIOps.
2. Một cơ chế `uncertainty-aware action gating` cho quyết định dưới bất định.
3. Một cơ chế `event-triggered coordination` cho workflow xử lý sự cố IT.
4. Một bộ điều khiển `risk-budgeted autonomy` cho Agentic AI trong AIOps.
5. Một giao thức đánh giá mới nhấn mạnh bounded-risk operational success.

### Đóng góp thực tiễn

1. Hỗ trợ thiết kế agent AIOps đáng tin cậy hơn cho doanh nghiệp.
2. Giảm nguy cơ tự động hóa quá mức trong incident handling.
3. Chuẩn hóa cơ chế observe more, defer và escalate trong workflow AI.
4. Tăng khả năng triển khai Agentic AI với human-in-the-loop trong vận hành IT.

## 9. Kế hoạch công bố

Luận án dự kiến phát triển thành bốn bài báo:

### Paper 1

`Belief-State Grounding for AIOps Agents under Partial Observability`

### Paper 2

`Uncertainty-Aware Action Gating for AIOps Agents`

### Paper 3

`Event-Triggered Incident Workflow Coordination for Agentic AIOps`

### Paper 4

`Risk-Budgeted Autonomy for Reliable AIOps Agents`

## 10. Kế hoạch thực hiện dự kiến

### Năm 1

- tổng quan tài liệu
- chuẩn hóa dữ liệu và problem setup
- hoàn thiện Paper 1

### Năm 2

- phát triển action gating
- thực hiện ablation và baseline comparison
- hoàn thiện Paper 2

### Năm 3

- phát triển coordination layer
- xây dựng incident episodes nâng cao
- hoàn thiện Paper 3

### Năm 4

- formal hóa risk-budgeted autonomy
- đánh giá tích hợp
- hoàn thiện Paper 4 và luận án

## 11. Rủi ro và phương án giảm thiểu

### Rủi ro 1

Dataset công khai chưa phản ánh hoàn toàn production AIOps.

Phương án:

- sử dụng nhiều dataset bổ sung
- thiết kế incident episodes có stress scenarios
- giới hạn claim ở mức offline evaluated AIOps

### Rủi ro 2

Risk model có thể phụ thuộc giả định cost.

Phương án:

- công khai cost model
- phân tích sensitivity dưới nhiều cấu hình
- dùng expert priors khi có thể

### Rủi ro 3

Scope có thể quá rộng nếu mở rộng sang quá nhiều domain hoặc quá nhiều chức năng agent.

Phương án:

- giữ AIOps là domain duy nhất
- xem coordination là phần mở rộng có kiểm soát
- tập trung vào bounded autonomy under uncertainty là trục lõi

## 12. Kết luận

Đề tài `Risk-Budgeted Agentic AI for Reliable AIOps under Uncertainty` là một hướng nghiên cứu phù hợp để phát triển thành luận án Tiến sĩ vì có:

- bài toán thực tiễn rõ trong industry
- dữ liệu công khai để thực nghiệm
- câu hỏi khoa học xuyên suốt
- khả năng chia thành nhiều bài báo liên kết
- không gian đóng góp ở mức cơ chế, không chỉ ở mức ứng dụng

Điểm cốt lõi của đề tài là chuyển từ câu hỏi “agent có làm được việc không” sang câu hỏi có giá trị học thuật và thực tế hơn: “agent nên được phép tự động đến đâu khi nó chưa chắc chắn và khi rủi ro phải được kiểm soát”.

## 13. Tài liệu tham khảo chính

1. GAIA Dataset. `https://github.com/CloudWise-OpenSource/GAIA-DataSet`
2. KPI-Anomaly-Detection. `https://github.com/NetManAIOps/KPI-Anomaly-Detection`
3. Multi-Source Distributed System Data. `https://zenodo.org/records/3484801`
4. Log Anomaly Detection Datasets. `https://github.com/ait-aecid/anomaly-detection-log-datasets`
5. GAIA: A Benchmark for AIOps. `https://dl.acm.org/doi/10.1145/3578245.3584730`
6. A survey on AIOps datasets, tools and benchmarks for log analytics. `https://www.sciencedirect.com/science/article/pii/S2666389923001915`
