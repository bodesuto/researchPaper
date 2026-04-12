# Đề Xuất Nghiên Cứu Tiến Sĩ

## Tên đề tài

### Tiếng Việt

`Agentic AI có ngân sách rủi ro cho AIOps: Ra quyết định vận hành IT đáng tin cậy dưới bất định`

### Tiếng Anh

`Risk-Budgeted Agentic AI for Reliable AIOps under Uncertainty`

## 1. Tóm tắt đề xuất

Sự phát triển của Agentic AI đang mở ra khả năng tự động hóa nhiều bước trong vận hành IT, nơi hệ thống AI không chỉ phân tích dữ liệu mà còn có thể lập kế hoạch, gọi công cụ, đề xuất hoặc thực hiện hành động, và phối hợp với con người trong quy trình xử lý sự cố. Tuy nhiên, điểm nghẽn lớn nhất hiện nay không còn là làm cho agent có năng lực ngôn ngữ tốt hơn, mà là làm cho agent đủ đáng tin cậy để hành động trong môi trường vận hành thực, nơi dữ liệu thường thiếu, nhiễu, trễ và mâu thuẫn; các quyết định phải được đưa ra nhanh; và hành động sai có thể gây ra gián đoạn dịch vụ nghiêm trọng.

Đề xuất này tập trung vào domain `AIOps / IT Operations`, thay vì giữ phạm vi rộng trên toàn bộ enterprise operations. Mục tiêu của luận án là phát triển một khung Agentic AI có khả năng ra quyết định closed-loop đáng tin cậy trong AIOps, dựa trên bốn thành phần liên kết chặt chẽ: `state grounding`, `uncertainty-aware action gating`, `event-triggered incident workflow coordination`, và `risk-budgeted autonomy`. Về mặt khoa học, luận án hướng tới việc chuyển trọng tâm từ nghiên cứu `agent capability` sang nghiên cứu `bounded autonomy under uncertainty`, trong đó agent không chỉ cần biết phải làm gì, mà còn phải biết khi nào chưa biết đủ, khi nào nên trì hoãn, khi nào nên quan sát thêm, khi nào phải chuyển người, và khi nào quyền tự động hóa cần bị giới hạn bởi ngân sách rủi ro.

Về thực nghiệm, luận án sử dụng các dataset công khai phù hợp với AIOps như `GAIA`, `KPI-Anomaly-Detection`, `Multi-Source Distributed System Data`, và nhóm `public log anomaly datasets` để xây dựng các episode xử lý sự cố IT. Các episode này cho phép đánh giá agent trong bối cảnh có bất định, có nhiều nguồn quan sát, có lựa chọn hành động, và có ràng buộc rủi ro. Kết quả kỳ vọng là một luận án có chiều sâu khoa học, có dữ liệu thực nghiệm cụ thể, có khả năng công bố thành bốn bài báo quốc tế liên kết chặt chẽ, và có tính thực tiễn cao đối với triển khai Agentic AI trong vận hành IT doanh nghiệp.

## 2. Bối cảnh và động cơ nghiên cứu

Trong các hệ thống CNTT hiện đại, vận hành dịch vụ ngày càng phụ thuộc vào hạ tầng phân tán, microservices, cloud-native platforms, pipelines CI/CD, và hệ thống giám sát đa nguồn. Khi xảy ra sự cố, tín hiệu vận hành thường đến từ nhiều nguồn khác nhau:

- logs
- metrics
- traces
- alerts
- incident tickets
- topology hoặc dependency graph
- runbooks và lịch sử can thiệp

Trong thực tế, không có một tín hiệu đơn lẻ nào đủ để kết luận chắc chắn trạng thái của hệ thống. Một alert có thể là false alarm. Một metric spike có thể là hậu quả chứ không phải nguyên nhân. Một trace có thể chưa đầy đủ. Một log anomaly có thể chỉ phản ánh nhiễu tạm thời. Vì vậy, việc phát hiện bất thường đơn thuần không đủ để đưa ra hành động vận hành.

Song song với đó, Agentic AI đang được xem là hướng đi mới để tự động hóa các workflow phức tạp hơn so với chatbot truyền thống. Trong AIOps, một agent có thể:

- truy vấn thêm logs, metrics hoặc traces
- tổng hợp bằng chứng từ nhiều nguồn
- định vị root cause sơ bộ
- gợi ý hoặc áp dụng runbook
- mở hoặc cập nhật incident ticket
- quyết định khi nào cần escalate cho on-call engineer

Tuy nhiên, agent trong môi trường này phải đối mặt với hai loại ràng buộc cốt lõi. Thứ nhất là `epistemic uncertainty`: agent không bao giờ quan sát đầy đủ trạng thái thật của hệ thống. Thứ hai là `operational risk`: một hành động sai, quá sớm, hoặc quá tự tin có thể gây downtime, tăng chi phí xử lý, tạo thêm cảnh báo giả, hoặc làm chậm thời gian khôi phục dịch vụ.

Khoảng trống của nghiên cứu hiện nay là phần lớn công trình AIOps vẫn tách rời các bài toán như anomaly detection, root-cause analysis, log mining, alert suppression hoặc incident prediction. Trong khi đó, bài toán thực tế của Agentic AI cho AIOps là bài toán ra quyết định closed-loop, trong đó hệ phải liên tục:

1. xây dựng nhận thức về trạng thái vận hành từ quan sát không hoàn hảo
2. quyết định có nên hành động hay không dưới bất định
3. cập nhật kế hoạch khi có bằng chứng mới
4. kiểm soát mức tự động hóa theo rủi ro chấp nhận được

Đây là khoảng trống vừa có giá trị khoa học, vừa có tính thực tiễn cao.

## 3. Khoảng trống nghiên cứu

Đề xuất này dựa trên bốn khoảng trống chính.

### 3.1. Thiếu cơ chế state grounding đáng tin cậy cho agent AIOps

Nhiều hệ AIOps hiện nay chỉ tối ưu một đầu ra như anomaly score, root-cause label hoặc alert priority. Chúng chưa cung cấp một `belief state` có cấu trúc, phản ánh:

- trạng thái hệ thống được ước lượng
- mức độ chắc chắn
- bằng chứng ủng hộ
- bằng chứng mâu thuẫn
- mức độ thiếu thông tin

Điều này làm cho các quyết định downstream khó được biện minh và khó được kiểm soát.

### 3.2. Thiếu cơ chế hành động dưới bất định

Phần lớn pipeline hiện tại mặc định rằng hệ phải đưa ra một kết luận hoặc một hành động ngay. Trong thực tế, một agent vận hành tốt đôi khi cần:

- trì hoãn
- hỏi thêm dữ liệu
- xác minh chéo
- hoặc chuyển người

Khoảng trống là chưa có đủ nghiên cứu về `act / defer / observe more / escalate` như một policy ra quyết định trong AIOps.

### 3.3. Thiếu cơ chế phối hợp workflow theo sự kiện

Trong xử lý sự cố IT, anomaly detection, root-cause analysis, runbook recommendation, remediation proposal và human escalation không vận hành độc lập. Chúng ảnh hưởng lẫn nhau theo thời gian. Tuy nhiên, nghiên cứu hiện nay còn thiếu một cơ chế `event-triggered coordination` cho agent, trong đó workflow được cập nhật khi có evidence mới hoặc khi mức rủi ro thay đổi.

### 3.4. Thiếu cơ chế quản trị quyền tự động hóa theo ngân sách rủi ro

Prompt guardrails hoặc rule-based fallback là chưa đủ. Một agent có thể đúng ở nhiều bước nhỏ nhưng vẫn gây rủi ro tích lũy lớn nếu liên tục gọi tool, đưa ra quyết định quá sớm, hoặc trì hoãn escalate quá lâu. Hiện nay còn thiếu một khung `risk-budgeted autonomy` có thể quản trị mức tự động hóa của agent theo chi phí và rủi ro tích lũy trong suốt episode xử lý sự cố.

## 4. Mục tiêu nghiên cứu

Luận án theo đuổi mục tiêu tổng quát sau:

`Phát triển một khung Agentic AI có khả năng ra quyết định vận hành IT đáng tin cậy trong AIOps dưới điều kiện quan sát không đầy đủ, bất định cao và ngân sách rủi ro hữu hạn.`

Các mục tiêu cụ thể gồm:

1. Xây dựng cơ chế `belief-state grounding` cho agent AIOps từ logs, metrics, traces, alerts và lịch sử sự cố.
2. Thiết kế cơ chế `uncertainty-aware action gating` cho phép agent chọn giữa `act`, `defer`, `observe more`, và `escalate`.
3. Phát triển cơ chế `event-triggered incident workflow coordination` để cập nhật kế hoạch xử lý sự cố khi trạng thái hoặc rủi ro thay đổi.
4. Đề xuất bộ điều khiển `risk-budgeted autonomy` để điều tiết mức tự động hóa của agent theo rủi ro tích lũy.
5. Xây dựng giao thức đánh giá nhấn mạnh `safe success under bounded risk`, thay vì chỉ đo `task success`.

## 5. Câu hỏi nghiên cứu

### RQ1

`Làm thế nào để agent suy ra belief state đáng tin cậy của hệ thống IT từ logs, metrics, traces, alerts và lịch sử sự cố trong điều kiện dữ liệu thiếu, nhiễu, trễ và mâu thuẫn?`

### RQ2

`Khi belief state chưa đủ chắc chắn, agent nên chọn act, defer, observe more hay escalate như thế nào để tối ưu cân bằng giữa hiệu quả xử lý và an toàn vận hành?`

### RQ3

`Khi xuất hiện evidence mới hoặc mức rủi ro thay đổi, agent nên tái phối hợp workflow xử lý sự cố như thế nào để cập nhật quyết định một cách có hệ thống?`

### RQ4

`Làm thế nào để kiểm soát mức tự động hóa của agent bằng ngân sách rủi ro tích lũy, sao cho safe success được tối đa hóa trong khi cumulative risk được khống chế?`

## 6. Giả thuyết nghiên cứu

Luận án đặt ra giả thuyết trung tâm:

`Độ tin cậy của Agentic AI trong AIOps không phải là thuộc tính của một predictor đơn lẻ, mà là thuộc tính nổi lên từ sự kết hợp có cấu trúc giữa state grounding, uncertainty-aware action gating, event-triggered coordination và risk-budgeted autonomy.`

Các giả thuyết cụ thể gồm:

- Một belief state giàu bằng chứng và có uncertainty calibration sẽ cải thiện chất lượng quyết định downstream so với pipeline chỉ dựa vào một score hoặc một label.
- Việc cho phép agent trì hoãn, quan sát thêm hoặc chuyển người sẽ làm giảm lỗi nghiêm trọng so với agent luôn hành động theo dự đoán tốt nhất.
- Việc tái phối hợp workflow khi có evidence mới sẽ cải thiện hiệu quả xử lý sự cố so với workflow tĩnh.
- Việc quản trị mức tự động hóa bằng risk budget sẽ tạo ra cân bằng tốt hơn giữa tốc độ xử lý và an toàn vận hành so với threshold-based autonomy đơn giản.

## 7. Phạm vi nghiên cứu

### 7.1. Phạm vi bao gồm

- Domain chính: `AIOps / IT Operations`
- Bối cảnh: xử lý sự cố trong hệ thống phân tán hoặc microservices
- Nguồn dữ liệu: logs, metrics, traces, alerts, incident records, runbooks
- Thiết lập thực nghiệm: offline evaluation trên dataset công khai và incident episodes mô phỏng

### 7.2. Phạm vi không bao gồm

- Không claim áp dụng đầy đủ cho mọi enterprise operations
- Không triển khai trực tiếp trên production system
- Không giải quyết toàn bộ bài toán MLOps, observability platform hoặc enterprise automation stack
- Không tập trung vào tối ưu model nền hoặc huấn luyện foundation model mới

## 8. Phương pháp nghiên cứu đề xuất

Luận án đề xuất một khung bốn lớp.

### 8.1. Lớp 1: Belief-State Grounding

Lớp này hợp nhất nhiều nguồn quan sát để suy ra trạng thái vận hành hiện tại của hệ thống. Đầu ra không chỉ là một nhãn bất thường, mà là một cấu trúc belief state gồm:

- giả thuyết trạng thái hiện tại
- mức độ chắc chắn
- bằng chứng ủng hộ
- bằng chứng mâu thuẫn
- thành phần hoặc service có khả năng là root cause

Mục tiêu của lớp này là trả lời câu hỏi: agent đang biết gì, biết chắc đến đâu, và đang thiếu gì.

### 8.2. Lớp 2: Uncertainty-Aware Action Gating

Thay vì buộc agent phải hành động ngay, lớp này cho phép chọn một trong bốn hành động:

- `act`
- `defer`
- `observe_more`
- `escalate`

Quyết định sẽ dựa trên:

- belief confidence
- chi phí của false action
- chi phí của delayed action
- mức nghiêm trọng của incident
- mức rủi ro còn lại trong budget

### 8.3. Lớp 3: Event-Triggered Incident Workflow Coordination

Lớp này điều phối workflow xử lý sự cố khi xuất hiện evidence mới, khi có kết quả từ tool khác, hoặc khi risk state thay đổi. Trong AIOps, coordination được hiểu là phối hợp giữa:

- anomaly detector
- RCA module
- runbook recommender
- remediation proposer
- incident ticketing
- human escalation

Mục tiêu là tránh workflow cứng và cho phép quyết định được cập nhật động.

### 8.4. Lớp 4: Risk-Budgeted Autonomy

Lớp này theo dõi rủi ro tích lũy của episode và điều tiết quyền tự động hóa của agent:

- vùng rủi ro thấp: được phép tự xử lý nhiều hơn
- vùng rủi ro trung bình: phải xác minh thêm hoặc giảm quyền công cụ
- vùng rủi ro cao: bắt buộc escalate hoặc yêu cầu human approval

Điểm mới của lớp này là đưa autonomy từ một cấu hình tĩnh thành một biến điều khiển phụ thuộc trạng thái và rủi ro.

## 9. Dữ liệu và tài nguyên thực nghiệm

### 9.1. Dataset chính: GAIA

Nguồn: `https://github.com/CloudWise-OpenSource/GAIA-DataSet`

Vai trò:

- nguồn dữ liệu chính cho state grounding
- xây dựng incident episodes có anomaly injection
- đánh giá root-cause reasoning và action gating

Lý do chọn:

- có metrics, logs, traces và nhiều nguồn dữ liệu khác
- phù hợp với microservice scenarios
- có điều kiện gần với AIOps hơn các dataset log đơn lẻ

### 9.2. Dataset phụ: KPI-Anomaly-Detection

Nguồn: `https://github.com/NetManAIOps/KPI-Anomaly-Detection`

Vai trò:

- benchmark phụ cho KPI anomaly detection
- stress test cho uncertainty và false alarm

### 9.3. Dataset phụ: Multi-Source Distributed System Data

Nguồn: `https://zenodo.org/records/3484801`

Vai trò:

- đánh giá hợp nhất nhiều nguồn quan sát
- kiểm tra robustness dưới điều kiện thiếu hoặc mâu thuẫn dữ liệu

### 9.4. Dataset phụ: Public Log Anomaly Datasets

Nguồn: `https://github.com/ait-aecid/anomaly-detection-log-datasets`

Vai trò:

- benchmark phụ cho log anomaly detection
- kiểm tra khả năng tổng quát hóa của state grounding trên log-only settings

## 10. Thiết kế thực nghiệm

### 10.1. Đơn vị đánh giá

Mỗi `episode` mô phỏng một sự cố vận hành IT:

1. anomaly hoặc fault xuất hiện
2. agent nhận observability evidence ban đầu
3. agent tạo belief state
4. agent chọn `act`, `defer`, `observe_more`, hoặc `escalate`
5. môi trường trả về evidence mới, chi phí hoặc outcome
6. risk budget được cập nhật

### 10.2. Hành động có thể mô phỏng

- query logs
- query metrics
- query traces
- inspect dependency graph
- classify severity
- localize root cause
- recommend runbook
- open incident ticket
- propose rollback / restart / scale
- escalate to human
- execute simulated remediation

### 10.3. Mô hình rủi ro

Rủi ro của một episode được mô hình hóa bởi một hàm chi phí, ví dụ:

```text
risk = cost(false_action)
     + cost(delayed_action)
     + cost(unnecessary_escalation)
     + cost(policy_violation)
     + cost(repeated_tool_calls)
     + cost(missed_root_cause)
```

Risk budget cho phép quyết định mức tự động hóa khả dụng ở từng bước.

### 10.4. Baselines

- Reactive agent
- Confidence-threshold agent
- Anomaly-only pipeline
- RCA-only pipeline
- Human-escalate-always policy
- Proposed risk-budgeted agent

### 10.5. Chỉ số đánh giá

- `task success rate`
- `safe success rate`
- `root-cause localization accuracy`
- `mean time to resolution`
- `false automation rate`
- `unnecessary escalation rate`
- `delayed escalation cost`
- `policy violation rate`
- `cumulative risk`
- `tool-call cost`
- `human intervention efficiency`

Chỉ số chính của luận án là:

`safe success rate under bounded cumulative risk`

## 11. Đóng góp khoa học dự kiến

Luận án dự kiến đóng góp:

1. Một mô hình `belief-state grounding` cho Agentic AIOps.
2. Một cơ chế `uncertainty-aware action gating` trong môi trường vận hành IT.
3. Một cơ chế `event-triggered coordination` cho workflow xử lý sự cố.
4. Một bộ điều khiển `risk-budgeted autonomy` cho Agentic AI.
5. Một giao thức đánh giá nhấn mạnh `safe success under bounded risk`.

## 12. Đóng góp thực tiễn dự kiến

Nếu thành công, luận án có thể mang lại giá trị thực tiễn sau:

- giúp doanh nghiệp triển khai agent AIOps với mức tự động hóa có kiểm soát hơn
- giảm nguy cơ tự động hóa quá mức trong incident handling
- chuẩn hóa cơ chế defer, observe more và escalate
- hỗ trợ thiết kế workflow human-in-the-loop cho AIOps
- cung cấp benchmark đánh giá gần với bài toán vận hành thực hơn so với chỉ đo anomaly detection

## 13. Kế hoạch công bố theo 4 bài báo

### Paper 1

`Belief-State Grounding for AIOps Agents under Partial Observability`

### Paper 2

`Uncertainty-Aware Action Gating for AIOps Agents`

### Paper 3

`Event-Triggered Incident Workflow Coordination for Agentic AIOps`

### Paper 4

`Risk-Budgeted Autonomy for Reliable AIOps Agents`

Lưu ý chiến lược: nếu Paper 3 không chứng minh được novelty đủ mạnh, có thể gộp phần coordination vào Paper 2 hoặc Paper 4 để giảm rủi ro luận án.

## 14. Kế hoạch thực hiện dự kiến trong 4 năm

### Năm 1

- hoàn thiện tổng quan tài liệu
- chốt formal problem statement
- chuẩn hóa dữ liệu và giao thức thực nghiệm
- thực hiện Paper 1

### Năm 2

- phát triển action gating
- xây baselines và ablation
- hoàn thiện Paper 2

### Năm 3

- phát triển coordination hoặc risk controller
- xây dựng incident episodes nâng cao
- hoàn thiện Paper 3

### Năm 4

- hoàn thiện risk-budgeted autonomy
- tích hợp giao thức đánh giá tổng thể
- hoàn thiện Paper 4 và luận án

## 15. Rủi ro nghiên cứu và phương án giảm thiểu

### Rủi ro 1: Dataset công khai chưa đủ sát production

Giảm thiểu:

- dùng nhiều dataset bổ sung
- thiết kế incident episodes có stress scenarios
- giới hạn claim ở mức offline AIOps evaluation

### Rủi ro 2: Risk model mang tính giả định

Giảm thiểu:

- định nghĩa cost function minh bạch
- phân tích sensitivity theo nhiều cost settings
- tham khảo expert priors hoặc runbooks nếu có

### Rủi ro 3: Scope quá rộng

Giảm thiểu:

- giữ AIOps là domain duy nhất
- xem multi-agent hoặc coordination là phần mở rộng, không phải trung tâm bắt buộc
- ưu tiên bounded autonomy under uncertainty là trục khoa học lõi

## 16. Kết luận

Đề tài `Risk-Budgeted Agentic AI for Reliable AIOps under Uncertainty` là một hướng nghiên cứu có tính thực tiễn cao, có dữ liệu công khai để thực nghiệm, và có khả năng phát triển thành một luận án Tiến sĩ mạch lạc. Điểm mạnh của đề tài là không dừng ở mức xây một agent có thể làm việc, mà tập trung vào câu hỏi khoa học khó hơn và giá trị hơn: làm thế nào để một agent vận hành IT biết khi nào mình chưa biết đủ, biết khi nào không nên hành động, và biết duy trì mức tự động hóa trong giới hạn rủi ro chấp nhận được.

Phiên bản đề xuất này phù hợp hơn để trình giáo sư hướng dẫn hoặc nộp nội bộ vì đã:

- chốt domain rõ ràng
- có câu hỏi nghiên cứu xuyên suốt
- có dữ liệu thực nghiệm cụ thể
- có thiết kế đánh giá khả thi
- có lộ trình công bố tương đối rõ

## 17. Tài liệu tham khảo chính

1. GAIA Dataset. `https://github.com/CloudWise-OpenSource/GAIA-DataSet`
2. KPI-Anomaly-Detection. `https://github.com/NetManAIOps/KPI-Anomaly-Detection`
3. Multi-Source Distributed System Data. `https://zenodo.org/records/3484801`
4. Log Anomaly Detection Datasets. `https://github.com/ait-aecid/anomaly-detection-log-datasets`
5. A survey on AIOps datasets, tools and benchmarks for log analytics. `https://www.sciencedirect.com/science/article/pii/S2666389923001915`
6. GAIA: A Benchmark for AIOps. `https://dl.acm.org/doi/10.1145/3578245.3584730`
