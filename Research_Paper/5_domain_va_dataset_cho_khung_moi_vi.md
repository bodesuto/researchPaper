# Năm Domain Và Dataset Để Áp Dụng Khung Luận Án Mới

## 1. Mục tiêu của tài liệu này

Tài liệu này được viết để bạn có thể đọc lại sau và nhanh chóng trả lời các câu hỏi sau:

- ngoài industrial operations thì khung luận án này còn áp dụng sang domain nào?
- mỗi domain có những dataset hoặc benchmark nào phù hợp?
- domain nào hợp nhất với từng paper?
- domain nào chỉ hợp ở mức ý tưởng, domain nào đủ tốt để làm thực nghiệm nghiêm túc?
- nên chọn domain nào nếu muốn mở rộng hoặc kiểm chứng transfer của khung?

Tài liệu này không thay thế cho proposal chính.  
Nó là một `bản đồ thực nghiệm mở rộng` để bạn không bị mất định hướng khi muốn đem khung nghiên cứu sang domain mới.

## 2. Nhắc lại khung 4 paper

Khung mới của luận án gồm 4 lớp:

1. `Paper 1`: State Grounding  
   - ước lượng trạng thái vận hành đáng tin cậy dưới partial observability

2. `Paper 2`: Uncertainty-Aware Decision Gating  
   - quyết định act / defer / observe more / escalate khi state chưa chắc chắn

3. `Paper 3`: Event-Triggered Joint Coordination  
   - chỉ tái phối hợp khi có biến động hoặc rủi ro đủ lớn

4. `Paper 4`: Risk-Budgeted Closed-Loop Autonomy  
   - quản lý mức tự động hóa bằng ngân sách rủi ro

Không phải domain nào cũng hợp đều với cả 4 lớp.  
Có domain mạnh ở Paper 1-2, có domain lại mạnh ở Paper 3-4.

## 3. Tiêu chí chọn domain

Một domain hợp với khung này nếu có các tính chất sau:

- `partial observability`
- `dynamic disruptions`
- `costly or asymmetric decisions`
- `safety or service constraints`
- có dữ liệu hoặc benchmark đủ rõ để làm thực nghiệm

Nếu thiếu 1-2 yếu tố, domain vẫn dùng được nhưng yếu hơn.  
Nếu thiếu nhiều yếu tố, khung này có thể không còn là lựa chọn tốt nhất.

## 4. Domain 1: Logistics / Last-Mile Delivery

## 4.1. Vì sao domain này hợp

Logistics là một domain rất tự nhiên cho khung này vì:

- hệ không bao giờ nhìn thấy toàn bộ trạng thái giao thông và vận chuyển theo thời gian thực
- quyết định dispatch, delay hoặc reroute thường có chi phí bất đối xứng
- các sự cố như kẹt xe, xe hỏng, nhu cầu tăng đột ngột là các `dynamic disruptions` rất điển hình
- rủi ro chính là trễ đơn, fail SLA, hoặc phân bổ tài nguyên kém

Nói cách khác:

- Paper 1 hợp vì phải hiểu trạng thái thật của đội xe, tuyến đường, tiến độ giao hàng
- Paper 2 hợp vì không phải lúc nào cũng nên dispatch ngay
- Paper 3 hợp vì nhiều xe, kho, tuyến phải phối hợp lại khi có sự cố
- Paper 4 hợp nếu bạn muốn quản lý tổng mức rủi ro giao hàng hoặc fail SLA

## 4.2. Dataset phù hợp

### A. Amazon Last Mile Routing Research Challenge Dataset

Đây là một bộ dữ liệu rất có giá trị vì nó đến từ một bối cảnh giao hàng thực tế.

Phù hợp cho:

- route planning
- dispatch quality
- coordination under delivery constraints

Rất hợp với:

- Paper 2
- Paper 3

Hợp vừa phải với:

- Paper 4

Hợp ít hơn với:

- Paper 1, nếu bạn muốn state grounding rất sâu từ telemetry thật

Link:

https://www.amazon.science/publications/2021-amazon-last-mile-routing-research-challenge-data-set

### B. NYC TLC Trip Record Data

Đây là dữ liệu giao thông đô thị quy mô rất lớn.

Phù hợp cho:

- mobility demand
- trip flow
- dispatching
- delay/reroute behavior

Rất hợp với:

- Paper 2
- Paper 3

Hợp ở mức ý tưởng cho:

- Paper 4

Hợp yếu hơn cho:

- Paper 1, nếu bạn cần hidden operational state sâu

Link:

https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page

## 4.3. Mức độ phù hợp theo 4 paper

| Paper | Mức phù hợp | Ghi chú |
|---|---:|---|
| Paper 1 | Trung bình | state grounding khó nếu thiếu telemetry giàu ngữ cảnh |
| Paper 2 | Cao | act / defer / reroute rất tự nhiên |
| Paper 3 | Cao | event-triggered coordination rất hợp |
| Paper 4 | Khá | dùng risk budget cho SLA/delay risk được |

## 4.4. Kết luận cho domain logistics

Nếu bạn muốn một domain:

- dễ kể câu chuyện
- gần vận hành thật
- mạnh ở phối hợp và trigger

thì logistics là lựa chọn rất tốt.

## 5. Domain 2: Cloud / Data Center Operations

## 5.1. Vì sao domain này hợp

Cloud operations cực hợp với khung này vì:

- logs, metrics, traces bản chất đã phản ánh `partial observability`
- anomaly state thường là latent, không quan sát trực tiếp được
- hệ không phải lúc nào cũng nên scale, rollback, migrate ngay
- các sự kiện như workload spike, node failure, anomaly burst là trigger rất rõ
- risk budget có thể định nghĩa bằng SLO violation risk hoặc outage risk

Đây là một trong những domain sạch nhất về mặt logic cho khung mới.

## 5.2. Dataset phù hợp

### A. Google Cluster Data

Đây là trace workload quy mô lớn, rất phù hợp cho:

- resource state modeling
- scheduling under uncertainty
- cluster-level coordination

Rất hợp với:

- Paper 1
- Paper 2
- Paper 3

Hợp khá với:

- Paper 4

Link:

https://github.com/google/cluster-data

### B. OpenStack Fault Injection Dataset

Đây là dataset rất phù hợp nếu bạn nghiêng về:

- anomaly handling
- incident response
- uncertain intervention decisions

Rất hợp với:

- Paper 1
- Paper 2
- Paper 4

Hợp vừa với:

- Paper 3

Link:

https://github.com/dessertlab/Fault-Injection-Dataset

## 5.3. Mức độ phù hợp theo 4 paper

| Paper | Mức phù hợp | Ghi chú |
|---|---:|---|
| Paper 1 | Rất cao | state grounding từ logs/metrics/traces rất tự nhiên |
| Paper 2 | Rất cao | scale / wait / rollback / escalate rất hợp |
| Paper 3 | Cao | service coordination, workload migration, failover |
| Paper 4 | Cao | risk budget bằng SLO/outage risk rất mạnh |

## 5.4. Kết luận cho cloud operations

Nếu bạn muốn một domain:

- logic rất sạch
- data phù hợp tự nhiên với thesis
- có thể nối cả 4 paper khá mượt

thì cloud operations là một trong những lựa chọn tốt nhất.

## 6. Domain 3: Robotics / Warehouse Robotics

## 6.1. Vì sao domain này hợp

Robotics rất hợp ở góc nhìn:

- environment chỉ quan sát được một phần
- robot không phải lúc nào cũng nên tiếp tục hành động
- khi có chướng ngại vật hoặc robot khác lỗi, phải phối hợp lại
- mức tự động hóa cần bị giảm nếu risk va chạm hoặc mission failure tăng

Domain này rất mạnh nếu bạn muốn nhấn vào:

- autonomy
- safety
- multi-agent coordination

## 6.2. Dataset / benchmark phù hợp

### A. Open X-Embodiment

Đây là bộ dữ liệu robot lớn, đa nguồn.

Phù hợp cho:

- state grounding
- uncertainty-aware perception-action

Rất hợp với:

- Paper 1
- Paper 2

Hợp ít hơn với:

- Paper 3, nếu bạn cần coordination benchmark chuẩn

Link:

https://github.com/google-deepmind/open_x_embodiment

https://robotics-transformer-x.github.io/

### B. Moving AI MAPF Benchmarks

Đây là benchmark chuẩn cho multi-agent path finding.

Rất hợp với:

- Paper 3
- Paper 4

Hợp vừa với:

- Paper 2

Hợp ít hơn với:

- Paper 1, vì phần state grounding không sâu như embodied perception datasets

Link:

https://movingai.com/benchmarks/

## 6.3. Mức độ phù hợp theo 4 paper

| Paper | Mức phù hợp | Ghi chú |
|---|---:|---|
| Paper 1 | Khá | tốt nếu dùng embodied datasets giàu quan sát |
| Paper 2 | Cao | continue / pause / reobserve / handover rất tự nhiên |
| Paper 3 | Cao | multi-robot coordination rất mạnh |
| Paper 4 | Cao | collision risk / mission risk rất hợp cho risk budget |

## 6.4. Kết luận cho robotics

Nếu bạn muốn một domain:

- giàu tính AI
- giàu coordination
- dễ nói về autonomy

thì robotics rất hấp dẫn.  
Tuy nhiên, để gắn chặt đủ cả 4 paper, bạn cần chọn dataset và benchmark cẩn thận hơn.

## 7. Domain 4: Transportation Operations

## 7.1. Vì sao domain này hợp

Transportation operations hợp với khung này vì:

- thông tin giao thông và hệ vận chuyển luôn không đầy đủ
- có rất nhiều disruption:
  - tai nạn
  - tắc đường
  - thời tiết xấu
  - chậm chuỗi
- quyết định dispatch / reroute / hold có chi phí lớn
- rủi ro dịch vụ và an toàn đều hiện diện

## 7.2. Dataset phù hợp

### A. NYC TLC Trip Record Data

Đây là dataset giao thông đô thị thuận tiện nhất để bắt đầu.

Phù hợp cho:

- trip flow
- dispatch
- congestion-aware routing

Link:

https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page

### B. Amazon Last Mile Routing Dataset

Có thể xem đây cũng là một dạng transportation operations ở mức route execution.

Link:

https://www.amazon.science/publications/2021-amazon-last-mile-routing-research-challenge-data-set

## 7.3. Mức độ phù hợp theo 4 paper

| Paper | Mức phù hợp | Ghi chú |
|---|---:|---|
| Paper 1 | Trung bình | hidden state không sâu bằng cloud/healthcare |
| Paper 2 | Cao | dispatch/defer/reroute rất tự nhiên |
| Paper 3 | Cao | coordination mạnh khi network disruption xảy ra |
| Paper 4 | Khá | risk budget theo delay propagation / service risk |

## 7.4. Kết luận cho transportation

Transportation hợp nếu bạn muốn:

- bài toán dễ kể
- gắn với mobility systems
- nhấn vào rerouting và event-triggered coordination

Nhưng domain này hơi chồng với logistics nếu không xác định scope đủ rõ.

## 8. Domain 5: Healthcare Operations / Critical Care Operations

## 8.1. Vì sao domain này hợp

Healthcare operations rất mạnh về mặt học thuật vì:

- state thật của bệnh nhân hoặc hệ chăm sóc thường chỉ quan sát một phần
- dữ liệu có thể thiếu, trễ, mâu thuẫn
- quyết định act/defer/observe/escalate cực kỳ quan trọng
- rủi ro an toàn cao

Đây là domain rất mạnh cho:

- state grounding
- uncertainty-aware decision making
- risk-governed autonomy

## 8.2. Dataset phù hợp

### A. MIMIC-IV

Là dataset ICU/hospital chuẩn, phổ biến nhất.

Rất hợp với:

- Paper 1
- Paper 2
- Paper 4

Link:

https://physionet.org/content/mimiciv/

### B. HiRID

Dataset critical care tần suất cao, rất hợp cho temporal state grounding.

Rất hợp với:

- Paper 1
- Paper 2

Hợp khá với:

- Paper 4

Link:

https://physionet.org/content/hirid/

### C. eICU-CRD

Hữu ích để kiểm tra transfer giữa nhiều trung tâm.

Phù hợp cho:

- external validation
- domain shift

Link:

https://physionet.org/content/eicu-crd/

## 8.3. Mức độ phù hợp theo 4 paper

| Paper | Mức phù hợp | Ghi chú |
|---|---:|---|
| Paper 1 | Rất cao | hidden state và uncertainty cực mạnh |
| Paper 2 | Rất cao | act / wait / observe / escalate rất tự nhiên |
| Paper 3 | Trung bình | coordination ở mức operations cần thiết kế thêm |
| Paper 4 | Cao | autonomy under risk rất mạnh |

## 8.4. Kết luận cho healthcare

Healthcare rất mạnh nếu bạn muốn:

- luận án có chiều sâu học thuật lớn
- state uncertainty là trọng tâm
- risk và escalation là trọng tâm

Nhược điểm:

- truy cập dữ liệu phức tạp hơn
- yêu cầu cẩn thận hơn về đạo đức và diễn giải

## 9. Bảng so sánh tổng hợp 5 domain

| Domain | Paper 1 | Paper 2 | Paper 3 | Paper 4 | Độ dễ triển khai | Nhận định ngắn |
|---|---:|---:|---:|---:|---:|---|
| Logistics | 3/5 | 5/5 | 5/5 | 4/5 | 4/5 | mạnh về coordination |
| Cloud operations | 5/5 | 5/5 | 4/5 | 5/5 | 5/5 | sạch nhất về logic tổng thể |
| Robotics | 4/5 | 4/5 | 5/5 | 5/5 | 3/5 | rất hay cho autonomy |
| Transportation | 3/5 | 5/5 | 5/5 | 4/5 | 4/5 | dễ kể nhưng gần logistics |
| Healthcare | 5/5 | 5/5 | 3/5 | 5/5 | 2/5 | rất mạnh học thuật nhưng khó hơn |

## 10. Khuyến nghị chọn domain

## 10.1. Nếu muốn dễ triển khai và logic rõ nhất

Chọn:

- `Cloud operations`

Vì:

- dữ liệu rất hợp với state grounding
- action gating rất tự nhiên
- coordination và risk budget cũng dễ định nghĩa

## 10.2. Nếu muốn dễ kể câu chuyện và gần vận hành đời thực

Chọn:

- `Logistics`

Vì:

- mọi người đều hiểu dispatch, delay, reroute, SLA
- event-triggered coordination rất trực quan

## 10.3. Nếu muốn nhấn vào AI autonomy và multi-agent

Chọn:

- `Robotics`

## 10.4. Nếu muốn chiều sâu học thuật mạnh về uncertainty và risk

Chọn:

- `Healthcare`

Nhưng chỉ nên chọn nếu bạn chấp nhận rào cản dữ liệu và validation cao hơn.

## 10.5. Nếu muốn một domain phụ gần logistics nhưng thiên mobility

Chọn:

- `Transportation`

## 11. Cách dùng tài liệu này trong thực tế

Bạn có thể dùng tài liệu này theo 3 cách:

### Cách 1: chọn domain phụ cho luận án

Ví dụ:

- domain chính: industrial operations
- domain phụ để bàn về transfer: cloud operations

### Cách 2: chọn hẳn một domain mới để triển khai khung

Ví dụ:

- bỏ industrial, chuyển hẳn sang cloud operations

### Cách 3: dùng để viết phần future work

Ví dụ:

- “The proposed framework could be extended to logistics, cloud operations, robotics, transportation, and healthcare operations.”

## 12. Kết luận cuối cùng

Nếu nhìn theo logic của khung mới, thì:

- `Cloud operations` là domain phụ mạnh nhất để mở rộng
- `Logistics` là domain phụ dễ trình bày nhất
- `Robotics` là domain phụ đẹp nhất nếu muốn nhấn vào tự động hóa
- `Healthcare` là domain phụ học thuật rất mạnh nhưng khó triển khai hơn
- `Transportation` là lựa chọn tốt nếu bạn muốn giữ gần với bài toán vận hành mạng lưới

Nói ngắn gọn:

- muốn `logic sạch và dễ triển khai`: chọn `cloud operations`
- muốn `dễ kể và dễ hình dung`: chọn `logistics`
- muốn `autonomy + coordination`: chọn `robotics`
- muốn `uncertainty + risk` cực mạnh: chọn `healthcare`

Tài liệu này nên được giữ như một bản đồ tham chiếu khi bạn cần cân nhắc mở rộng luận án sang các domain khác.
