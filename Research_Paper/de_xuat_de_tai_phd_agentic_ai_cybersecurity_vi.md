# Đề Xuất Nghiên Cứu Tiến Sĩ

## Tên đề tài

### Tiếng Việt

`Agentic AI có ngân sách rủi ro cho vận hành an ninh mạng: Ra quyết định điều tra và ứng phó đáng tin cậy dưới bất định`

### Tiếng Anh

`Risk-Budgeted Agentic AI for Reliable Cybersecurity Operations under Uncertainty`

## 1. Tóm tắt đề xuất

Trong các trung tâm vận hành an ninh mạng hiện đại, khối lượng cảnh báo, logs, indicators of compromise, threat intelligence và sự kiện bất thường tăng nhanh vượt quá khả năng xử lý hoàn toàn thủ công. Agentic AI mở ra khả năng tự động hóa một phần quy trình SOC bằng cách cho phép hệ AI quan sát nhiều nguồn dữ liệu, gọi công cụ, điều tra cảnh báo, tổng hợp bằng chứng, đề xuất hành động và phối hợp với chuyên gia an ninh.

Tuy nhiên, bài toán cốt lõi không phải là làm cho agent trả lời giống chuyên gia hơn, mà là làm cho agent đủ đáng tin cậy để hỗ trợ hoặc tự động ra quyết định trong một môi trường có rủi ro cao, dữ liệu nhiễu, tín hiệu mâu thuẫn và hậu quả lớn nếu hành động sai. Một agent an ninh mạng không chỉ cần biết “có vẻ nguy hiểm”, mà còn phải biết:

- nhận thức được trạng thái điều tra hiện tại đáng tin đến đâu
- khi nào chưa đủ bằng chứng để cô lập hoặc chặn
- khi nào cần yêu cầu thêm bằng chứng
- khi nào phải chuyển cho analyst
- khi nào mức tự động hóa đang vượt quá ngân sách rủi ro chấp nhận được

Đề xuất này áp dụng khung luận án sang domain `cybersecurity operations / SOC`, tập trung vào bốn thành phần: `security state grounding`, `uncertainty-aware action gating`, `event-triggered incident investigation coordination`, và `risk-budgeted autonomy`. Về mặt khoa học, luận án hướng tới một khung Agentic AI có khả năng ra quyết định điều tra và ứng phó đáng tin cậy trong an ninh mạng dưới bất định. Về mặt thực nghiệm, luận án dự kiến dùng các nguồn dữ liệu công khai hoặc bán công khai như `SAIBERSOC`, các benchmark alert triage/incident response, bộ dữ liệu telemetry và logs, kết hợp với incident episodes mô phỏng để đánh giá.

## 2. Bối cảnh và động cơ nghiên cứu

Trong SOC, các quyết định thường dựa trên nhiều loại bằng chứng:

- SIEM alerts
- endpoint telemetry
- network flows
- authentication logs
- threat intelligence
- ticket history
- triage notes
- playbooks và response policies

Một alert đơn lẻ thường không đủ để kết luận đây là:

- false positive
- low-risk anomaly
- active compromise
- lateral movement
- data exfiltration attempt

Hơn nữa, các hành động tiếp theo có chi phí và rủi ro rất khác nhau:

- bỏ qua cảnh báo
- hỏi thêm dữ liệu
- enrich IOC
- mở điều tra sâu hơn
- cô lập endpoint
- khóa tài khoản
- chặn domain/IP
- escalte cho analyst hoặc incident commander

Nếu agent hành động quá sớm, nó có thể gây gián đoạn nghiệp vụ, khóa nhầm tài khoản hoặc làm nhiễu workflow SOC. Nếu agent trì hoãn quá lâu, nó có thể bỏ lỡ thời gian vàng để containment. Vì vậy, cybersecurity operations là một domain rất phù hợp để nghiên cứu Agentic AI dưới bounded autonomy.

## 3. Khoảng trống nghiên cứu

### 3.1. Thiếu cơ chế security state grounding

Nhiều mô hình hiện nay chỉ gán nhãn alert hoặc ưu tiên cảnh báo. Chúng chưa xây dựng một `security belief state` phản ánh:

- mức độ khả nghi hiện tại
- loại tấn công khả dĩ
- độ chắc chắn
- bằng chứng ủng hộ và mâu thuẫn
- phạm vi ảnh hưởng có thể có

### 3.2. Thiếu cơ chế hành động dưới bất định

Trong thực tế SOC, không phải lúc nào cũng nên chặn ngay. Hệ có thể cần:

- quan sát thêm
- query thêm logs
- làm enrichment
- chờ tín hiệu xác nhận
- hoặc chuyển analyst

Khoảng trống là chưa có nhiều nghiên cứu formal hóa `act / defer / observe more / escalate` trong incident response agent.

### 3.3. Thiếu cơ chế phối hợp điều tra theo sự kiện

Điều tra an ninh là một quy trình động. Khi có IOC mới, kết quả sandbox mới, hoặc kết quả từ EDR mới, toàn bộ hướng điều tra có thể phải cập nhật. Cần một cơ chế `event-triggered incident investigation coordination` thay vì workflow cứng.

### 3.4. Thiếu cơ chế quản trị autonomy theo rủi ro

Trong an ninh mạng, rủi ro của false action và false inaction đều cao. Nhưng phần lớn hệ hiện tại vẫn dùng threshold hoặc rule static. Cần một khung `risk-budgeted autonomy` để quyết định agent được phép tự động đến đâu trong từng tình huống.

## 4. Mục tiêu nghiên cứu

Mục tiêu tổng quát:

`Phát triển một khung Agentic AI có khả năng ra quyết định điều tra và ứng phó an ninh mạng đáng tin cậy dưới điều kiện quan sát không đầy đủ, tín hiệu mâu thuẫn và ngân sách rủi ro hữu hạn.`

Các mục tiêu cụ thể:

1. Xây dựng `security state grounding` từ alerts, logs, telemetry và threat evidence.
2. Thiết kế `uncertainty-aware action gating` cho các lựa chọn act, defer, observe more và escalate.
3. Phát triển `event-triggered coordination` cho workflow điều tra và ứng phó sự cố.
4. Đề xuất `risk-budgeted autonomy` để giới hạn quyền tự động hóa của agent trong SOC.
5. Xây dựng giao thức đánh giá nhấn mạnh `safe response under bounded risk`.

## 5. Câu hỏi nghiên cứu

### RQ1

`Làm thế nào để agent suy ra một security belief state đáng tin cậy từ nhiều nguồn telemetry và alerts vốn thiếu, nhiễu và mâu thuẫn?`

### RQ2

`Khi chưa đủ bằng chứng, agent nên quyết định như thế nào giữa hành động ngay, trì hoãn, quan sát thêm hay chuyển analyst?`

### RQ3

`Khi có bằng chứng mới hoặc mức độ nghiêm trọng thay đổi, hệ nên tái phối hợp workflow điều tra và ứng phó như thế nào?`

### RQ4

`Làm thế nào để kiểm soát mức tự động hóa của agent trong SOC bằng ngân sách rủi ro, sao cho tối đa hóa hiệu quả điều tra mà vẫn hạn chế false action và missed response?`

## 6. Giả thuyết nghiên cứu

Giả thuyết trung tâm:

`Độ tin cậy của Agentic AI trong cybersecurity operations là thuộc tính nổi lên từ security state grounding, action gating dưới bất định, coordination theo sự kiện và quản trị autonomy theo ngân sách rủi ro.`

Các giả thuyết cụ thể:

- belief state giàu bằng chứng sẽ tốt hơn alert score đơn lẻ cho triage và response
- cho phép defer hoặc observe more sẽ giảm false containment và false blocking
- coordination động sẽ nâng hiệu quả điều tra so với pipeline tĩnh
- risk-budgeted autonomy sẽ tốt hơn static threshold trong cân bằng giữa phản ứng nhanh và an toàn tác nghiệp

## 7. Phạm vi nghiên cứu

### 7.1. Bao gồm

- domain chính: SOC / cybersecurity operations
- bài toán trung tâm: alert triage, investigation support và bounded response
- dữ liệu: alerts, logs, telemetry, investigation traces, policies/playbooks
- đánh giá offline và semi-simulated incident episodes

### 7.2. Không bao gồm

- không claim full autonomous cyber defense trên production
- không tập trung vào malware reverse engineering sâu
- không tối ưu foundation model mới
- không giải quyết toàn bộ attack detection stack

## 8. Phương pháp nghiên cứu đề xuất

### 8.1. Lớp 1: Security State Grounding

Đầu vào:

- alerts
- endpoint/network telemetry
- log evidence
- IOC enrichment
- prior incident notes

Đầu ra:

- belief state về bản chất của sự cố
- uncertainty score
- bằng chứng ủng hộ/mâu thuẫn
- mức độ ảnh hưởng khả dĩ

### 8.2. Lớp 2: Uncertainty-Aware Action Gating

Agent chọn giữa:

- `act`
- `defer`
- `observe_more`
- `escalate`

Trong SOC, `act` có thể là:

- enrich thêm IOC
- tạo incident
- đề xuất containment
- đề xuất account suspension
- đề xuất block IOC

### 8.3. Lớp 3: Event-Triggered Investigation Coordination

Phối hợp giữa:

- alert triage
- IOC enrichment
- correlation
- investigation update
- containment recommendation
- analyst escalation

### 8.4. Lớp 4: Risk-Budgeted Autonomy

Điều tiết mức tự động hóa:

- rủi ro thấp: agent được triage và recommend tự động
- rủi ro trung bình: agent phải quan sát thêm hoặc yêu cầu xác minh
- rủi ro cao: chỉ recommend, không tự containment
- rủi ro rất cao: bắt buộc human approval

## 9. Dữ liệu và tài nguyên thực nghiệm

### 9.1. SAIBERSOC

Nguồn:

`https://arxiv.org/abs/2010.08453`

Vai trò:

- mô phỏng realistic SOC setting với synthetic attack injection
- hỗ trợ xây incident episodes cho evaluation

### 9.2. Các benchmark alert triage / SOC workflow công khai

Ví dụ:

- AACT: Alert Analysis and Classification/Containment oriented studies
- các dataset từ nghiên cứu alert triage dùng telemetry và alert context

Vai trò:

- triage benchmark
- severity/risk reasoning benchmark

### 9.3. Bộ dữ liệu logs/telemetry an ninh công khai

Có thể dùng thêm tùy phạm vi:

- Windows event logs
- authentication logs
- network intrusion datasets
- enterprise telemetry datasets công khai

Vai trò:

- stress test cho state grounding
- test generalization trên loại evidence khác nhau

### 9.4. Incident episodes mô phỏng

Do dữ liệu SOC công khai thường không đủ đầy, luận án cần xây semi-simulated episodes bằng cách:

- kết hợp alerts với telemetry bổ sung
- định nghĩa playbooks
- gán cost/risk cho action
- tạo luồng evidence xuất hiện theo thời gian

## 10. Thiết kế thực nghiệm

### 10.1. Đơn vị đánh giá

Mỗi `episode` mô phỏng một security incident:

1. cảnh báo ban đầu xuất hiện
2. agent nhận alert + context ban đầu
3. agent xây security belief state
4. agent chọn hành động
5. môi trường trả về evidence mới hoặc cost
6. risk budget được cập nhật

### 10.2. Action Space

- inspect related alerts
- query user/device history
- query IOC enrichment
- correlate events
- classify severity
- open investigation ticket
- recommend containment
- recommend block/suspend
- escalate to analyst

### 10.3. Mô hình rủi ro

```text
risk = cost(false_containment)
     + cost(delayed_response)
     + cost(unnecessary_escalation)
     + cost(missed_incident)
     + cost(policy_violation)
     + cost(excessive_tool_use)
```

### 10.4. Baselines

- alert-score threshold baseline
- triage-only model
- investigate-always baseline
- escalate-always baseline
- proposed risk-budgeted agent

### 10.5. Metrics

- triage accuracy
- safe response rate
- false containment rate
- missed incident rate
- mean time to containment recommendation
- unnecessary escalation rate
- cumulative risk
- tool cost
- human intervention efficiency

Metric chính:

`safe response rate under bounded cumulative risk`

## 11. Đóng góp khoa học dự kiến

1. Một mô hình `security belief-state grounding`
2. Một cơ chế `uncertainty-aware action gating` cho SOC agents
3. Một cơ chế `event-triggered coordination` cho investigation workflow
4. Một bộ điều khiển `risk-budgeted autonomy` cho cybersecurity agents
5. Một giao thức đánh giá nhấn mạnh bounded-risk response

## 12. Đóng góp thực tiễn dự kiến

- hỗ trợ thiết kế AI analyst assistant an toàn hơn
- giảm false containment và false blocking
- tăng tính kiểm soát khi triển khai AI trong SOC
- cung cấp benchmark gần với incident workflow thật hơn

## 13. Kế hoạch công bố theo 4 bài báo

### Paper 1

`Security Belief-State Grounding for SOC Agents`

### Paper 2

`Uncertainty-Aware Action Gating for Cybersecurity Operations`

### Paper 3

`Event-Triggered Incident Investigation Coordination for Agentic SOC`

### Paper 4

`Risk-Budgeted Autonomy for Reliable Cybersecurity Agents`

## 14. Kế hoạch thực hiện dự kiến trong 4 năm

### Năm 1

- tổng quan tài liệu
- chuẩn hóa dữ liệu và incident episodes
- Paper 1

### Năm 2

- action gating và baselines
- Paper 2

### Năm 3

- coordination workflow
- Paper 3

### Năm 4

- risk-budgeted autonomy
- đánh giá tích hợp
- Paper 4 và luận án

## 15. Rủi ro nghiên cứu và phương án giảm thiểu

### Rủi ro 1: dữ liệu SOC công khai hạn chế

Giảm thiểu:

- dùng semi-simulated episodes
- kết hợp nhiều nguồn công khai
- giới hạn claim ở mức benchmarked SOC workflows

### Rủi ro 2: chi phí/rủi ro hành động khó định lượng

Giảm thiểu:

- định nghĩa cost model minh bạch
- đánh giá sensitivity trên nhiều risk setting

### Rủi ro 3: domain quá nhạy cho full automation

Giảm thiểu:

- tập trung vào recommend/approve workflow
- bounded autonomy thay vì full autonomous response

## 16. Kết luận

Đề tài `Risk-Budgeted Agentic AI for Reliable Cybersecurity Operations under Uncertainty` là một hướng mở rộng mạnh về mặt thực tiễn và học thuật. Nó phù hợp nếu mục tiêu là nghiên cứu Agentic AI trong môi trường rủi ro cao, nơi bounded autonomy, uncertainty-aware decisions và human-in-the-loop là trung tâm.
