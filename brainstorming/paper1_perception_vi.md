# Paper 1: Grounded Perception Cho Tác Nhân Công Nghiệp

## 1. Problem statement

Các tác nhân AI dùng trong bảo trì công nghiệp thường đưa ra chẩn đoán, giải thích hoặc đề xuất hành động không nhất quán với trạng thái vận hành thực tế. Vấn đề này không chỉ làm giảm độ tin cậy của hệ thống mà còn có thể dẫn tới quyết định bảo trì sai, trì hoãn xử lý sự cố hoặc kích hoạt hành động không cần thiết.

## 2. Gap nghiên cứu

Các nghiên cứu hiện có về hallucination và grounded reasoning chủ yếu tập trung vào semantic retrieval, reflection hoặc evidence retrieval từ kho tri thức tĩnh. Tuy nhiên, trong môi trường bảo trì công nghiệp, dữ liệu quan trọng nhất để xác nhận tính đúng sai của một kết luận lại nằm ở `observability data` như log vận hành, trace hệ thống, cảnh báo, trạng thái cảm biến và execution history. Khoảng trống nghiên cứu nằm ở chỗ chưa có nhiều công trình kết hợp mạnh giữa tri thức nền và observability memory trong một cấu trúc đủ chặt để hỗ trợ grounding theo thời gian thực.

Nói cách khác, literature hiện vẫn thiếu một cơ chế cho phép tác nhân đồng thời:

- hiểu tri thức kỹ thuật nền
- đối chiếu tri thức đó với dữ liệu vận hành mới nhất
- phát hiện mâu thuẫn giữa tri thức nền và thực tế quan sát
- lượng hóa mức độ bất định của kết luận đưa ra

## 3. Câu hỏi nghiên cứu và giả thuyết

### RQ

Liệu một cơ chế `observability-grounded dual-memory knowledge graph` có thể làm giảm hallucination và tăng factual grounding trong tác nhân bảo trì công nghiệp tốt hơn semantic-only memory, retrieval-only memory và các biến thể dual-memory không có conflict checking hay không?

### Giả thuyết

Việc kết hợp `semantic memory` với `observability memory`, cùng temporal retrieval và conflict checking, sẽ giúp giảm hallucination rate, tăng evidence grounding score và cải thiện chất lượng chẩn đoán trong điều kiện log nhiễu, cảm biến thiếu hoặc tri thức vận hành bị trôi theo thời gian.

## 4. Đóng góp và novelty claim

### Novelty claim một câu

Bài báo đề xuất một cơ chế `observability-grounded dual-memory knowledge graph` cho tác nhân công nghiệp, trong đó tri thức nền và bằng chứng vận hành được liên kết động để phát hiện mâu thuẫn, giảm hallucination và tạo grounded state có thể truy vết bằng chứng.

### Đóng góp chính

- Đề xuất cấu trúc `dual-memory knowledge graph` gồm semantic memory và observability memory.
- Đề xuất cơ chế `temporal retrieval` để ưu tiên bằng chứng còn hiệu lực theo thời gian.
- Đề xuất cơ chế `memory conflict checking` để phát hiện mâu thuẫn giữa tri thức nền và observability memory.
- Đề xuất đầu ra nhận thức chuẩn hóa gồm `grounded_state`, `evidence_set`, `inconsistency_score`, `uncertainty_score`.
- Định nghĩa vận hành cho `hallucination rate` trong bối cảnh bảo trì công nghiệp.

### Cải tiến gì và cải tiến ở đâu

- So với semantic-only KG: bổ sung observability memory làm nguồn grounding động.
- So với RAG/KG-RAG: bổ sung conflict checking giữa tri thức nền và thực tế vận hành.
- So với retrieval tĩnh: bổ sung temporal validity và execution-grounded evidence.
- So với dual-memory đơn giản: bổ sung cơ chế định lượng bất nhất và bất định.

## 5. Phương pháp đề xuất

### 5.1. Đầu vào

- tri thức nền về thiết bị, thành phần, quy trình bảo trì, quan hệ nhân quả kỹ thuật
- maintenance logs
- alarm traces
- sensor/event history
- execution history

### 5.2. Kiến trúc

#### Semantic memory

Semantic memory lưu tri thức ổn định của miền, bao gồm:

- loại thiết bị
- cấu trúc hệ thống
- quan hệ thành phần
- quy trình và quy tắc kỹ thuật
- tri thức về lỗi, nguyên nhân và hành động xử lý

#### Observability memory

Observability memory lưu bằng chứng động có dấu thời gian, bao gồm:

- log cảnh báo
- trace hành vi hệ thống
- sensor state transitions
- lịch sử hành động và outcome
- availability và trạng thái thiết bị

#### Temporal retrieval

Temporal retrieval truy xuất bằng chứng dựa trên:

- mức liên quan ngữ nghĩa với truy vấn
- độ gần thời gian
- độ tin cậy của nguồn quan sát
- tính nhất quán với execution history

#### Conflict checking

Conflict checking phát hiện ba dạng mâu thuẫn:

- tri thức nền nói A nhưng observability memory cho thấy non-A
- kết luận hiện tại trái với execution history đã xác thực
- đề xuất hành động không có bằng chứng hỗ trợ trong trạng thái vận hành hiện tại

#### Grounded output

Mỗi lần suy luận, tác nhân sinh ra:

- `grounded_state`
- `evidence_set`
- `inconsistency_score`
- `uncertainty_score`

### 5.3. Định nghĩa vận hành của hallucination rate

Một phát biểu, chẩn đoán hoặc đề xuất hành động được xem là hallucination nếu rơi vào ít nhất một trong ba trường hợp:

- không truy vết được tới một evidence set hợp lệ
- mâu thuẫn với observability memory tại thời điểm đánh giá
- kết luận về trạng thái thiết bị trái với execution history đã xác thực

`Hallucination rate` được tính là tỷ lệ đầu ra của tác nhân vi phạm ít nhất một trong ba điều kiện trên.

## 6. So sánh với literature

### Nhóm baseline cần so sánh

- semantic-only KG retrieval
- retrieval-only memory
- RAG không có observability memory
- single-memory graph memory
- dual-memory không conflict checking
- dual-memory không temporal retrieval

### Điểm literature dễ bị phản biện

- Nếu chỉ dùng observability như nguồn dữ liệu phụ, bài sẽ bị xem là engineering extension.
- Nếu không chứng minh conflict checking tạo ra khác biệt, dual-memory dễ bị xem là ghép bộ nhớ hình thức.
- Nếu không định nghĩa được hallucination theo ngữ cảnh maintenance, metric sẽ bị cho là mơ hồ.

## 7. Thiết kế thực nghiệm

### Domain neo

- Maintenance/Knowledge

### Dữ liệu

- MAKG
- maintenance logs
- alarm traces
- sensor/event history

### Thiết lập thực nghiệm

- xây tác nhân trả lời câu hỏi chẩn đoán hoặc đề xuất hành động xử lý
- đánh giá trong bối cảnh:
  - log đầy đủ
  - log thiếu
  - log lỗi thời
  - record mâu thuẫn

### Metrics

- hallucination rate
- factual consistency
- evidence grounding score
- task success rate
- uncertainty calibration nếu có confidence model

### Baselines

- semantic-only KG
- RAG không observability
- single-memory graph
- dual-memory không conflict checking

### Ablations

- bỏ observability memory
- bỏ temporal retrieval
- bỏ conflict checking
- bỏ uncertainty estimation

### Stress tests

- stale logs
- missing sensor values
- conflicting records
- noise injection vào observability stream

## 8. Điều kiện để đủ sức Q1

### Đánh giá thực dụng hiện tại

- Khả thi triển khai: `9/10`
- Độ mới học thuật: `8/10`
- Tiềm năng Q1: `8.5/10`

### Khuyến nghị chiến lược

Đây nên là bài mở đầu của toàn bộ lộ trình nghiên cứu. Lý do là hướng này vừa có logic phương pháp rõ, vừa khả thi về dữ liệu và đánh giá, lại có thể tạo ra một novelty đủ sắc mà không cần phụ thuộc vào toàn bộ CAMAS. Nếu cần dồn nguồn lực để có một bài mạnh sớm, nên ưu tiên hoàn thiện bài này trước.

### Venue family phù hợp

- Knowledge-Based Systems
- Expert Systems with Applications
- Information Sciences

### Điều kiện đủ tối thiểu

- Phải chứng minh được observability memory là nguồn tạo khác biệt thực sự, không chỉ thêm dữ liệu.
- Phải có định nghĩa hallucination rõ và có thể tái lập.
- Phải có ít nhất một nhóm baseline mạnh ngoài semantic KG.
- Phải có một insight rõ: grounding bằng observability mới là yếu tố quyết định, không phải chỉ tăng kích thước memory.
- Nên có thêm một baseline thực dụng mạnh kiểu retrieval-augmented diagnosis để chứng minh bài không chỉ hơn các baseline biểu diễn, mà còn hơn baseline gần ứng dụng.

### Điều gì sẽ kéo bài xuống Q2/Q3

- thí nghiệm chỉ có một baseline yếu
- metric không đủ chặt
- dual-memory nhưng không chứng minh được conflict checking có giá trị
- thiếu robustness test

### Cách làm thực tế nhất

- Không cố làm benchmark quá rộng ở phiên bản đầu.
- Tập trung vào một tác vụ rõ như fault diagnosis hoặc maintenance action recommendation.
- Dùng MAKG + logs làm xương sống; benchmark reasoning công khai chỉ nên là phần bổ sung nếu còn thời gian.

## 9. Rủi ro phản biện và cách phòng thủ

### Phản biện 1

“Bài này chỉ là thêm log vào knowledge graph.”

### Phòng thủ

Nhấn mạnh novelty nằm ở:

- temporal retrieval
- conflict checking
- grounded output
- định nghĩa vận hành của hallucination

### Phản biện 2

“Hallucination trong bảo trì không được định nghĩa chặt.”

### Phòng thủ

Đưa ra schema gán nhãn rõ, dựa trên evidence set, observability consistency và execution history.

### Phản biện 3

“Chưa đủ chứng minh tính tổng quát.”

### Phòng thủ

Không claim tổng quát quá rộng. Chỉ claim mạnh trên domain maintenance, và nếu cần có thêm benchmark reasoning làm bằng chứng phụ.

## 10. Vai trò trong luận án tiến sĩ

Paper 1 tạo ra `grounded_state`, là điều kiện cần để toàn bộ CAMAS tránh ra quyết định trên trạng thái sai. Đây là nền móng của luận án vì Coordination và Alignment chỉ có giá trị nếu đầu vào nhận thức đủ đáng tin cậy.

### Mapping vào luận án

- một chương hoặc một cụm nội dung về grounded perception
- một đóng góp phương pháp đầu tiên của luận án
- nền dữ liệu và interface cho các chương sau
