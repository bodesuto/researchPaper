# Đề Xuất Nghiên Cứu Tiến Sĩ

## Tên đề tài

### Tiếng Việt

`Agentic AI có ngân sách rủi ro cho sản xuất thông minh: Ra quyết định vận hành và bảo trì đáng tin cậy dưới bất định`

### Tiếng Anh

`Risk-Budgeted Agentic AI for Reliable Smart Manufacturing Operations under Uncertainty`

## 1. Tóm tắt đề xuất

Sản xuất thông minh đang chuyển dần từ các hệ thống giám sát thụ động sang các hệ thống có khả năng hỗ trợ hoặc tự động ra quyết định trong bảo trì, điều độ, phân bổ tài nguyên và ứng phó gián đoạn. Trong bối cảnh đó, Agentic AI hứa hẹn đưa AI tiến xa hơn khỏi vai trò dự báo đơn lẻ, để trở thành một tác nhân có thể tổng hợp dữ liệu cảm biến, logs vận hành, cảnh báo, lịch bảo trì và ràng buộc sản xuất; sau đó đề xuất hoặc thực hiện hành động phù hợp.

Tuy nhiên, thách thức trọng tâm không phải là làm cho agent dự báo chính xác hơn một chút, mà là làm cho agent **đủ đáng tin cậy để tham gia vòng lặp ra quyết định vận hành thực**. Trong nhà máy, các quyết định sai có thể gây ra downtime, giảm chất lượng sản phẩm, tăng tiêu hao năng lượng, phá vỡ lịch sản xuất, hoặc tạo rủi ro an toàn. Vì vậy, một agent không chỉ cần biết “nên làm gì”, mà còn phải biết:

- trạng thái vận hành hiện tại đáng tin đến đâu
- khi nào chưa nên hành động
- khi nào cần quan sát thêm hoặc gọi con người
- khi nào phải phối hợp lại kế hoạch trên toàn hệ
- mức tự động hóa nào là chấp nhận được dưới ngân sách rủi ro

Đề xuất này áp dụng cùng trục khoa học của khung luận án sang domain `smart manufacturing / predictive maintenance`, với bốn thành phần: `state grounding`, `uncertainty-aware action gating`, `event-triggered joint coordination`, và `risk-budgeted closed-loop autonomy`. Về mặt khoa học, luận án hướng đến việc phát triển một khung ra quyết định closed-loop đáng tin cậy cho môi trường sản xuất dưới điều kiện quan sát không đầy đủ, gián đoạn động và ràng buộc an toàn. Về mặt thực nghiệm, luận án tận dụng các dataset công khai như `NASA C-MAPSS`, `AI4I 2020 Predictive Maintenance`, `MetroPT 3`, và một số bộ dữ liệu industrial anomaly/fault khác để xây dựng benchmark và kịch bản đánh giá.

## 2. Bối cảnh và động cơ nghiên cứu

Các hệ sản xuất hiện đại ngày càng được instrument hóa mạnh bởi:

- cảm biến rung, nhiệt độ, áp suất, tốc độ, dòng điện
- PLC/SCADA logs
- alarms và event streams
- lịch vận hành, lịch bảo trì, lịch sản xuất
- thông tin về chất lượng sản phẩm
- cấu trúc phụ thuộc giữa thiết bị và dây chuyền

Mặc dù dữ liệu ngày càng nhiều, quyết định vận hành vẫn khó vì trạng thái thật của hệ thống không được quan sát trực tiếp. Một cụm rung bất thường có thể là dấu hiệu hỏng ổ trục, nhưng cũng có thể do thay đổi chế độ tải. Một nhiệt độ tăng có thể là triệu chứng sớm của lỗi, nhưng cũng có thể phản ánh điều kiện môi trường. Một cảnh báo đơn lẻ không đủ để quyết định dừng máy, nhưng bỏ qua nó có thể dẫn đến hỏng nghiêm trọng hơn.

Phần lớn nghiên cứu hiện nay trong sản xuất thông minh vẫn tách rời các lớp quyết định:

- predictive maintenance
- anomaly detection
- fault diagnosis
- scheduling
- resource allocation

Trong thực tế, các quyết định này liên kết chặt chẽ với nhau. Nếu một thiết bị có nguy cơ hỏng tăng, hệ thống không chỉ cần gán nhãn “fault likely”, mà còn cần quyết định:

- tiếp tục chạy hay dừng kiểm tra?
- giảm tải hay đổi lịch?
- gọi kỹ sư hay yêu cầu quan sát thêm?
- tái phối hợp kế hoạch sản xuất với bảo trì và phân bổ tài nguyên như thế nào?

Đây là lý do cần một khung Agentic AI cho sản xuất thông minh, trong đó AI không chỉ dự báo mà còn tham gia ra quyết định closed-loop dưới bất định.

## 3. Khoảng trống nghiên cứu

### 3.1. Thiếu cơ chế state grounding ở mức vận hành

Nhiều nghiên cứu chỉ dự đoán RUL, fault class hoặc anomaly score. Nhưng nhà máy cần một `operational belief state` giàu ngữ cảnh hơn, thể hiện:

- tình trạng thiết bị hiện tại
- mức độ chắc chắn
- nguồn bằng chứng hỗ trợ và mâu thuẫn
- mức độ ảnh hưởng tới dây chuyền
- nguy cơ lan truyền sang các công đoạn khác

### 3.2. Thiếu cơ chế hành động dưới bất định

Trong thực tế, khi chưa chắc chắn, hệ có thể cần:

- trì hoãn quyết định
- yêu cầu cảm biến hoặc kiểm tra bổ sung
- giảm tải
- chuyển kỹ sư xác minh

Khoảng trống là chưa có nhiều nghiên cứu formal hóa lựa chọn `act / defer / observe more / escalate` trong ngữ cảnh bảo trì và vận hành công nghiệp.

### 3.3. Thiếu cơ chế phối hợp giữa bảo trì, điều độ và tài nguyên

Một rủi ro thiết bị mới xuất hiện có thể làm thay đổi kế hoạch sản xuất, lịch bảo trì, phân bổ nhân lực và vật tư. Tuy nhiên, phần lớn các mô hình vẫn giải các bài toán này rời rạc. Cần một cơ chế `event-triggered joint coordination` cho phép tái phối hợp khi có gián đoạn động.

### 3.4. Thiếu cơ chế quản trị mức tự động hóa theo rủi ro

Trong nhà máy, không thể giao quyền hành động cố định cho AI trong mọi bối cảnh. Cần một bộ điều khiển biết:

- khi nào AI chỉ được cảnh báo
- khi nào AI được đề xuất hành động
- khi nào AI được tự động điều chỉnh nhẹ
- khi nào phải dừng ở mức recommend-only hoặc human approval

Hiện vẫn thiếu một khung `risk-budgeted autonomy` cho Agentic AI trong sản xuất thông minh.

## 4. Mục tiêu nghiên cứu

Mục tiêu tổng quát của luận án là:

`Phát triển một khung Agentic AI có khả năng ra quyết định vận hành và bảo trì đáng tin cậy trong sản xuất thông minh, dưới điều kiện quan sát không đầy đủ, gián đoạn động và ngân sách rủi ro hữu hạn.`

Các mục tiêu cụ thể gồm:

1. Xây dựng `belief-state grounding` từ sensor streams, logs, alarms và lịch sử vận hành.
2. Thiết kế `uncertainty-aware action gating` cho quyết định act, defer, observe more, escalate.
3. Phát triển `event-triggered joint coordination` giữa bảo trì, điều độ và phân bổ tài nguyên.
4. Đề xuất `risk-budgeted autonomy` để giới hạn mức tự động hóa theo rủi ro tích lũy.
5. Xây dựng giao thức đánh giá nhấn mạnh `safe operational success under bounded risk`.

## 5. Câu hỏi nghiên cứu

### RQ1

`Làm thế nào để agent suy ra trạng thái vận hành đáng tin cậy của thiết bị và dây chuyền khi dữ liệu cảm biến, logs và alarms bị thiếu, nhiễu, trễ hoặc mâu thuẫn?`

### RQ2

`Khi trạng thái vận hành chưa đủ chắc chắn, agent nên quyết định như thế nào giữa hành động ngay, trì hoãn, quan sát thêm, giảm tải hoặc chuyển kỹ sư xác minh?`

### RQ3

`Khi rủi ro thiết bị hoặc hiệu năng dây chuyền thay đổi, hệ nên tái phối hợp bảo trì, điều độ và phân bổ tài nguyên như thế nào?`

### RQ4

`Làm thế nào để kiểm soát mức tự động hóa của Agentic AI trong nhà máy bằng ngân sách rủi ro, sao cho tối đa hóa hiệu quả vận hành mà vẫn giữ an toàn và độ tin cậy?`

## 6. Giả thuyết nghiên cứu

Giả thuyết trung tâm của luận án là:

`Độ tin cậy của Agentic AI trong sản xuất thông minh là thuộc tính nổi lên từ sự tương tác có cấu trúc giữa state grounding, action gating dưới bất định, phối hợp theo sự kiện và quản trị quyền tự động hóa theo ngân sách rủi ro.`

Các giả thuyết cụ thể gồm:

- belief state giàu ngữ cảnh sẽ tốt hơn dự báo đơn đầu ra trong hỗ trợ quyết định vận hành
- cho phép defer hoặc observe more sẽ giảm các quyết định dừng máy hoặc can thiệp sai
- tái phối hợp giữa bảo trì và điều độ khi có sự kiện mới sẽ tốt hơn tối ưu cục bộ
- risk-budgeted autonomy sẽ tạo cân bằng tốt hơn giữa hiệu quả và an toàn so với ngưỡng cảnh báo tĩnh

## 7. Phạm vi nghiên cứu

### 7.1. Phạm vi bao gồm

- domain chính: smart manufacturing / predictive maintenance
- bài toán trung tâm: vận hành thiết bị và dây chuyền dưới rủi ro hỏng hóc và gián đoạn động
- nguồn dữ liệu: cảm biến, logs, alarms, maintenance history, production context
- đánh giá offline trên dataset công khai và kịch bản mô phỏng

### 7.2. Phạm vi không bao gồm

- không claim triển khai đầy đủ trên production factory
- không tập trung vào robot control thời gian thực mức thấp
- không tối ưu foundation model mới
- không mở rộng đồng thời sang quá nhiều domain khác

## 8. Phương pháp nghiên cứu đề xuất

### 8.1. Lớp 1: State Grounding

Lớp này hợp nhất:

- sensor streams
- alarm history
- machine logs
- operational context
- maintenance records

Đầu ra là một `belief state` cho từng thiết bị hoặc cụm thiết bị, bao gồm:

- trạng thái vận hành ước lượng
- uncertainty score
- bằng chứng ủng hộ
- bằng chứng mâu thuẫn
- nguy cơ tác động đến dây chuyền

### 8.2. Lớp 2: Uncertainty-Aware Action Gating

Agent có thể chọn một trong các hành động:

- `act`: thực hiện khuyến nghị vận hành hoặc bảo trì
- `defer`: trì hoãn quyết định
- `observe_more`: thu thêm tín hiệu hoặc yêu cầu kiểm tra bổ sung
- `escalate`: chuyển chuyên gia/kỹ sư xác minh

Trong manufacturing, `act` có thể bao gồm:

- giảm tải
- đổi mode vận hành
- đề xuất dừng kiểm tra
- đề xuất bảo trì ngắn hạn
- đề xuất thay đổi lịch sản xuất

### 8.3. Lớp 3: Event-Triggered Joint Coordination

Khi xuất hiện rủi ro mới, hệ cần tái phối hợp giữa:

- bảo trì
- điều độ sản xuất
- phân bổ nhân lực kỹ thuật
- phân bổ phụ tùng hoặc tài nguyên hỗ trợ

Mục tiêu là tránh quyết định cục bộ tốt nhưng toàn hệ kém.

### 8.4. Lớp 4: Risk-Budgeted Closed-Loop Autonomy

Lớp này điều tiết mức tự động hóa theo rủi ro tích lũy:

- rủi ro thấp: AI được đề xuất hoặc tự điều chỉnh nhẹ
- rủi ro trung bình: AI phải yêu cầu quan sát thêm hoặc xác minh
- rủi ro cao: AI chỉ được recommend, không được tự hành động
- rủi ro rất cao: bắt buộc human approval

## 9. Dữ liệu và tài nguyên thực nghiệm

### 9.1. NASA C-MAPSS

Nguồn:

`https://data.nasa.gov/dataset/c-mapss-aircraft-engine-simulator-data`

Vai trò:

- benchmark chính cho degradation modeling và RUL-oriented state reasoning
- xây dựng belief state trên chuỗi suy giảm của thiết bị

### 9.2. AI4I 2020 Predictive Maintenance Dataset

Nguồn:

`https://archive.ics.uci.edu/dataset/601/ai4i+2020+predictive+maintenance+dataset`

Vai trò:

- benchmark cho fault prediction và maintenance decision support
- phù hợp để xây scenario false alarm, missed detection, early intervention

### 9.3. MetroPT 3 Dataset

Nguồn:

`https://zenodo.org/records/6854240`

Vai trò:

- dữ liệu công nghiệp thực cho predictive maintenance
- phù hợp cho state grounding và event-triggered decision

### 9.4. Các bộ dữ liệu phụ khác

Có thể mở rộng thêm theo khả năng:

- IMS Bearing Dataset
- MIMII hoặc MIMII DG cho industrial sound anomaly detection
- SECOM manufacturing data

Vai trò:

- stress test generalization
- đánh giá robustness khi đổi loại thiết bị hoặc modality dữ liệu

## 10. Thiết kế thực nghiệm

### 10.1. Đơn vị đánh giá

Mỗi `episode` mô phỏng một tình huống vận hành:

1. dấu hiệu xuống cấp hoặc fault risk tăng
2. agent nhận một phần quan sát ban đầu
3. agent xây belief state
4. agent chọn `act`, `defer`, `observe_more`, hoặc `escalate`
5. môi trường trả về evidence mới, cost và outcome
6. risk budget được cập nhật

### 10.2. Action Space

- query sensor window
- inspect alarm history
- inspect maintenance record
- estimate degradation trend
- classify severity
- recommend reduced load
- recommend inspection
- recommend maintenance slot
- escalate to engineer
- trigger simulated intervention

### 10.3. Mô hình rủi ro

Rủi ro có thể được mô hình hóa bởi:

```text
risk = cost(unnecessary_stop)
     + cost(missed_failure)
     + cost(delayed_maintenance)
     + cost(unnecessary_escalation)
     + cost(schedule_disruption)
     + cost(safety_violation)
```

### 10.4. Baselines

- anomaly-only baseline
- fault classification baseline
- predictive maintenance baseline
- threshold-based intervention policy
- always-escalate policy
- proposed risk-budgeted agent

### 10.5. Metrics

- fault detection / diagnosis accuracy
- safe intervention rate
- false stop rate
- missed failure rate
- mean time to intervention
- maintenance cost
- production disruption cost
- cumulative risk
- human intervention efficiency

Metric trung tâm nên là:

`safe operational success under bounded cumulative risk`

## 11. Đóng góp khoa học dự kiến

Luận án dự kiến đóng góp:

1. một mô hình `belief-state grounding` cho vận hành công nghiệp
2. một cơ chế `uncertainty-aware action gating` cho quyết định bảo trì/vận hành
3. một cơ chế `event-triggered joint coordination` giữa maintenance và scheduling
4. một bộ điều khiển `risk-budgeted autonomy` cho Agentic AI trong manufacturing
5. một giao thức đánh giá nhấn mạnh an toàn và hiệu quả toàn hệ, không chỉ accuracy

## 12. Đóng góp thực tiễn dự kiến

Nếu thành công, luận án có thể:

- hỗ trợ thiết kế hệ AI đáng tin cậy cho predictive maintenance thế hệ mới
- giảm can thiệp sai hoặc dừng máy không cần thiết
- cải thiện phối hợp giữa bảo trì và điều độ sản xuất
- cung cấp framework quyết định có thể triển khai từng phần trong nhà máy
- nâng mức chấp nhận của doanh nghiệp đối với AI có quyền tự động hóa giới hạn

## 13. Kế hoạch công bố theo 4 bài báo

### Paper 1

`Belief-State Grounding for Smart Manufacturing under Partial Observability`

### Paper 2

`Uncertainty-Aware Action Gating for Predictive Maintenance Agents`

### Paper 3

`Event-Triggered Joint Coordination of Maintenance and Scheduling under Dynamic Risk`

### Paper 4

`Risk-Budgeted Autonomy for Reliable Agentic Manufacturing Operations`

## 14. Kế hoạch thực hiện dự kiến trong 4 năm

### Năm 1

- tổng quan tài liệu
- chốt bài toán và dữ liệu
- xây baseline và Paper 1

### Năm 2

- phát triển action gating
- đánh giá với nhiều cost setting
- hoàn thiện Paper 2

### Năm 3

- phát triển coordination giữa maintenance và scheduling
- xây scenario gián đoạn động
- hoàn thiện Paper 3

### Năm 4

- formal hóa risk-budgeted autonomy
- đánh giá tích hợp
- hoàn thiện Paper 4 và luận án

## 15. Rủi ro nghiên cứu và phương án giảm thiểu

### Rủi ro 1: dataset công khai chưa đủ phong phú ở mức toàn nhà máy

Giảm thiểu:

- dùng nhiều dataset bổ sung
- mô phỏng incident episodes
- giới hạn claim ở mức benchmarked manufacturing settings

### Rủi ro 2: bài toán coordination quá rộng

Giảm thiểu:

- chỉ chọn phối hợp giữa maintenance và scheduling
- không mở rộng sang toàn bộ supply chain

### Rủi ro 3: action space trong nhà máy quá khó để triển khai thật

Giảm thiểu:

- đánh giá trên simulated interventions
- tập trung vào recommend/approve workflow thay vì full autonomous control

## 16. Kết luận

Đề tài `Risk-Budgeted Agentic AI for Reliable Smart Manufacturing Operations under Uncertainty` là một hướng mở rộng hợp lý từ khung luận án gốc sang một domain khác có tính thực tiễn cao. Domain này phù hợp vì:

- có nhu cầu industry rõ ràng
- có dữ liệu công khai để thực nghiệm
- có bài toán quyết định dưới bất định thật sự
- có không gian để đóng góp ở mức PhD thay vì chỉ xây ứng dụng

Điểm mạnh của hướng này là giữ được trục khoa học thống nhất của luận án, đồng thời bám sát một bài toán công nghiệp cụ thể và có giá trị triển khai thực tế.
