# Bản Triển Khai Lộ Trình 4 Bài Báo Q1 Cho CAMAS

## 1. Định vị nghiên cứu

Tài liệu này chuyển đề xuất CAMAS hiện tại thành một lộ trình nghiên cứu hướng công bố gồm 4 bài báo:

1. Bài 1: Perception
2. Bài 2: Coordination
3. Bài 3: Alignment
4. Bài 4: Tích hợp closed-loop

Mục tiêu không phải là khẳng định chắc chắn sẽ có "4 bài Q1". Mục tiêu là cấu trúc lại chương trình nghiên cứu sao cho mỗi bài đều có:

- một novelty hẹp, rõ và có thể bảo vệ được
- một domain neo đủ mạnh để đánh giá
- baseline và ablation rõ ràng
- độ chồng lặp novelty thấp với các bài còn lại

Bài tích hợp cuối cùng là bài duy nhất nên claim CAMAS như một kiến trúc closed-loop hoàn chỉnh.

## 2. Logic công bố tổng thể

### Nguyên tắc cốt lõi

Mỗi bài theo module phải có khả năng đứng độc lập để công bố mà không cần phụ thuộc vào toàn bộ stack CAMAS.

### Domain neo

- Bài 1 neo vào Maintenance/Knowledge
- Bài 2 neo vào FJSP/Scheduling
- Bài 3 neo vào Smart Grid
- Bài 4 tích hợp cả 3 domain

### Chính sách tái sử dụng giữa các bài

Những gì được phép tái sử dụng:

- phần động cơ nghiên cứu về hệ đa tác nhân công nghiệp
- động cơ chung của CAMAS
- ký hiệu chung cho state, action, reward, constraint
- hạ tầng thực nghiệm dùng chung khi phù hợp

Những gì không được chồng lặp:

- cùng một novelty claim chính ở hai bài
- cùng một câu chuyện ablation được tái dùng làm đóng góp thực nghiệm chính
- cùng một benchmark đóng vai trò bằng chứng chính cho hai bài module mà không có câu hỏi nghiên cứu khác biệt

## 3. Bài 1: Perception

### Tên hướng bài báo

Đồ thị tri thức bộ nhớ kép có neo quan sát thực tế cho tác nhân giảm ảo giác trong bảo trì công nghiệp

### Câu hỏi nghiên cứu

Việc lập luận dựa trên dual-memory có neo observability giúp giảm hallucination tốt hơn bao nhiêu so với semantic-only memory hoặc retrieval-only memory trong các tác nhân phục vụ bảo trì?

### Novelty chính

Đưa ra một dual-memory knowledge graph gồm:

- semantic memory cho tri thức miền ổn định
- observability memory cho log, trace, trạng thái và chuyển trạng thái động

Đóng góp không nằm ở việc "dùng KG", mà nằm ở cơ chế grounding giúp kiểm tra tính nhất quán giữa điều tác nhân tin và điều hệ thống thực sự quan sát được.

### Phương pháp đề xuất

#### Nguồn đầu vào

- đồ thị tri thức bảo trì
- log bảo trì
- lịch sử cảnh báo
- dữ liệu cảm biến và chuyển trạng thái
- thông tin availability của thiết bị và lịch sử can thiệp

#### Kiến trúc

1. Xây semantic subgraph từ thực thể, quan hệ, quy trình và tri thức thành phần.
2. Xây observability subgraph từ log có đóng dấu thời gian, trace, alarm, action và outcome.
3. Liên kết hai subgraph qua thực thể chung, thời gian và tham chiếu sự kiện.
4. Truy xuất bằng chứng từ cả hai bộ nhớ bằng retrieval có xét ngữ cảnh truy vấn và độ hiệu lực theo thời gian.
5. Tính các tín hiệu bất nhất:
   - mâu thuẫn semantic-observability
   - phát hiện tri thức lỗi thời
   - phát hiện hành động hoặc kế hoạch không có bằng chứng hỗ trợ
6. Sinh đầu ra grounded:
   - grounded state
   - evidence set
   - inconsistency score
   - uncertainty score

#### Mở rộng tùy chọn

Có thể thêm confidence estimator để dự đoán xác suất hallucination từ các đặc trưng bất nhất bằng chứng.

### Cải tiến gì, ở đâu

- So với semantic-only KG:
  - bổ sung grounding từ vận hành thực tế
- So với RAG hoặc KG-RAG:
  - bổ sung observability memory và conflict checking tường minh
- So với retrieval tĩnh:
  - bổ sung temporal validity và execution-grounded evidence

### Dữ liệu

Dữ liệu chính:

- MAKG + maintenance logs

Dữ liệu phụ:

- một benchmark reasoning có evidence chain nếu cần tăng tính hấp dẫn với nhóm AI/Expert Systems

### Baseline

- semantic-only KG retrieval
- single-memory graph memory
- RAG không có observability memory
- dual-memory nhưng không có conflict validation
- retrieval không có temporal filtering

### Ablation

- bỏ observability memory
- bỏ temporal update
- bỏ conflict checking
- bỏ uncertainty/confidence estimation

### Metric

- hallucination rate
- factual consistency
- task success rate
- evidence grounding score
- calibration/confidence quality nếu dùng confidence model

### Stress test

- log lỗi thời
- nhiễu cảm biến
- thiếu một phần quan sát
- record bảo trì mâu thuẫn nhau

### Ranh giới bài báo

Bài này dừng ở perception và grounding. Không nên phụ thuộc vào full CAMAS để bảo vệ novelty.

## 4. Bài 2: Coordination

### Tên hướng bài báo

Điều phối đa tác nhân phân cấp thích ứng theo ngữ cảnh với mô hình hóa trạng thái bằng đồ thị cho FJSP động

### Câu hỏi nghiên cứu

Liệu điều phối đa tác nhân phân cấp với biểu diễn đồ thị thích ứng theo ngữ cảnh có vượt được các tiếp cận MARL phẳng hoặc biểu diễn tĩnh trong môi trường scheduling động có ràng buộc hay không?

### Novelty chính

Kết hợp bốn thành phần trong một framework điều phối:

- hierarchical MARL để phân rã quyết định
- MD-MDP để mô hình hóa action/reward đa chiều
- graph-based encoder để nắm cấu trúc phụ thuộc giữa agent, job, machine
- LRMP như lớp biểu diễn thích ứng theo ngữ cảnh

Đây là vị trí phù hợp để đặt LRMP trong lộ trình công bố. Không nên để LRMP xuất hiện nửa ở perception, nửa ở coordination.

### Phương pháp đề xuất

#### Môi trường

- flexible job shop scheduling có nhiễu động
- thay đổi availability của máy
- áp lực deadline
- ràng buộc tương thích operation-machine

#### Kiến trúc

1. Biểu diễn trạng thái scheduling thành heterogeneous graph trên job, operation, machine và các biến trạng thái theo thời gian.
2. Dùng temporal và relational encoding để nắm phụ thuộc thay đổi.
3. Dùng policy phân cấp:
   - master policy chọn chiến lược hoặc subgoal
   - worker policy chọn dispatch/assignment cụ thể
4. Dùng MD-MDP để mô hình hóa nhiều chiều hành động và nhiều thành phần reward.
5. Áp dụng LRMP lên graph embedding để biểu diễn điều phối thích ứng theo context thay vì cố định.

### Cải tiến gì, ở đâu

- So với flat MARL:
  - tách quyết định chiến lược và vận hành tốt hơn
- So với graph-only coordination:
  - thêm cấu trúc phân cấp và biểu diễn thích ứng theo ngữ cảnh
- So với MDP chuẩn:
  - mô hình hóa đa chiều phù hợp hơn với quyết định scheduling thực tế

### Dữ liệu

Dữ liệu chính:

- Barnes FJSP benchmarks

Dữ liệu phụ:

- một benchmark FJSP động hoặc kịch bản perturbation tự sinh

### Baseline

- rule-based dispatching
- PPO hoặc DQN
- flat MARL
- hierarchical MARL không có graph encoder
- graph RL không có attention hoặc temporal modeling
- graph coordination không có MD-MDP

### Ablation

- bỏ hierarchy
- bỏ MD-MDP
- bỏ graph encoder
- bỏ temporal modeling
- bỏ LRMP

### Metric

- makespan
- total tardiness
- machine utilization
- robustness under perturbation
- convergence stability

Metric HHS hiện mơ hồ. Chỉ nên giữ nếu được định nghĩa toán học rất chặt. Mặc định nên thay bằng metric chuẩn của scheduling và robustness.

### Stress test

- machine breakdown
- urgent job insertion
- demand spike
- delayed operation

### Ranh giới bài báo

Bài này tập trung vào chất lượng điều phối trong môi trường động có ràng buộc. Không cần kéo alignment hoặc human feedback vào để bảo vệ bài.

## 5. Bài 3: Alignment

### Tên hướng bài báo

Cooperative RLHF có xét ràng buộc cho ra quyết định đa tác nhân an toàn trong smart grid

### Câu hỏi nghiên cứu

Liệu một framework cooperative RLHF có xét constraint có thể cải thiện điều khiển an toàn tuân thủ ràng buộc tốt hơn RLHF chuẩn và các baseline safe RL trong môi trường đa tác nhân có ràng buộc hay không?

### Novelty chính

Mở rộng CoRLHF sang bối cảnh cyber-physical bằng cách tách:

- utility/preference learning
- feasibility/safety learning theo ràng buộc vật lý

Đóng góp chính không phải chỉ là "thêm penalty", mà là làm cho reward learning và policy learning nhận thức được hard constraints theo cách có cấu trúc.

### Phương pháp đề xuất

#### Môi trường

- vận hành smart grid đa tác nhân
- ràng buộc capacity của đường dây
- ràng buộc cân bằng công suất
- luật an toàn và độ tin cậy

#### Kiến trúc

1. Thu thập trajectory từ mô phỏng lưới điện.
2. Xây nhãn preference từ chuyên gia, heuristic expert hoặc simulated human preference.
3. Xây nhãn safety trực tiếp từ đánh giá constraint vật lý.
4. Huấn luyện reward model hai đầu:
   - utility head
   - safety/feasibility head
5. Tối ưu policy bằng cooperative RLHF dưới ràng buộc an toàn tường minh.
6. Thêm constrained optimization layer:
   - Lagrangian safety control, hoặc
   - policy update có safety budget

### Cải tiến gì, ở đâu

- So với RLHF chuẩn:
  - bổ sung nhận thức hard constraints
- So với safe RL:
  - bổ sung preference information và alignment logic
- So với reward penalty thủ công:
  - học utility và safety theo hai tín hiệu riêng, thích ứng hơn

### Dữ liệu

Dữ liệu chính:

- IEEE 30/118/300 bus

Mở rộng tùy chọn:

- dữ liệu EVN nếu đủ sạch, nhất quán và công bố được

### Baseline

- RLHF chuẩn
- constrained RL không human feedback
- safe RL với handcrafted rewards
- CoRLHF không mô hình hóa hard constraints

### Ablation

- bỏ safety head
- bỏ cooperative reward refinement
- bỏ hard-constraint optimizer
- chỉ dùng preference feedback

### Metric

- safety violation rate
- constraint satisfaction rate
- return hoặc profit
- robustness under disturbances
- stability khi tải hoặc nguồn phát thay đổi

### Stress test

- demand thay đổi đột ngột
- dao động nguồn tái tạo
- line congestion
- preference label bị nhiễu hoặc không nhất quán

### Ranh giới bài báo

Bài này nói về safe alignment cho ra quyết định có ràng buộc. Không nên dựa vào novelty của perception để giải thích bài.

## 6. Bài 4: Integration

### Tên hướng bài báo

CAMAS: kiến trúc đa tác nhân nhận thức closed-loop với grounded perception, adaptive coordination và safe alignment

### Câu hỏi nghiên cứu

Việc tích hợp closed-loop giữa grounded perception, adaptive coordination và safe alignment có tạo ra lợi ích ở mức hệ thống tốt hơn các cấu hình open-loop hoặc chỉ tích hợp từng cặp module hay không?

### Novelty chính

Chứng minh CAMAS không phải là phép ghép lỏng lẻo của ba kỹ thuật, mà là một kiến trúc closed-loop có interface rõ ràng, có feedback semantics và có lợi ích emergent đo được.

### Thiết kế interface

#### Đầu ra của Perception

- grounded state representation
- evidence set
- inconsistency score
- uncertainty score

#### Đầu ra của Coordination

- action set hoặc policy distribution
- context embedding
- coordination confidence

#### Đầu ra của Alignment

- updated reward model
- updated preference model
- updated constraint model
- policy update signal

#### Feedback loop

- alignment gửi tín hiệu ngược về perception qua:
  - policy priors
  - retrieval/attention bias
  - uncertainty-aware re-grounding trigger
- cần định nghĩa lịch phản hồi:
  - mỗi bước
  - mỗi episode
  - hoặc event-triggered

### Quy trình tích hợp đề xuất

1. Perception sinh grounded state và uncertainty profile.
2. Coordination sinh action candidate hoặc policy output từ grounded state.
3. Alignment đánh giá utility và safety, sau đó cập nhật policy và feedback priors.
4. Perception dùng feedback từ alignment ở vòng tiếp theo để retrieval có chọn lọc hơn hoặc ưu tiên xử lý conflict.
5. Lặp online qua nhiều episode và nhiều nhiễu động.

### Cải tiến gì, ở đâu

- So với hệ chỉ có module rời:
  - thêm feedback giữa chất lượng hành động và grounding ở bước sau
- So với open-loop pipeline:
  - có thích nghi lặp, không phải xử lý một chiều
- So với pairwise integration:
  - có synergy ở cấp hệ thống giữa cả ba module

### Dữ liệu và logic đánh giá

- Maintenance để chứng minh grounding và xử lý uncertainty
- FJSP để chứng minh adaptive coordination dưới perturbation
- Smart Grid để chứng minh trade-off safety-profit dưới hard constraints

Bài tích hợp không nên cố chứng minh novelty sâu của từng module thêm một lần nữa. Nó phải chứng minh lợi ích hệ thống do đóng vòng.

### Baseline

- perception only
- perception + coordination
- coordination + alignment
- full CAMAS nhưng không có feedback loop
- open-loop sequential pipeline
- strong end-to-end system baselines nếu tìm được

### Ablation

- tắt alignment-to-perception feedback
- tắt uncertainty propagation
- tắt conflict-aware re-grounding
- thay event-triggered loop bằng fixed schedule

### Metric

- end-to-end task performance
- safety
- efficiency/profit
- robustness
- latency/compute overhead
- cross-domain generalization

### Stress test

- distribution shift
- noisy observations
- delayed feedback
- human preference không nhất quán
- domain transfer hoặc partial transfer

## 7. Bản đồ công bố

| Bài | Novelty cốt lõi | Domain neo | Baseline chính | Loại đóng góp |
|---|---|---|---|---|
| Bài 1 | Grounded dual-memory perception | Maintenance | semantic KG, RAG, single-memory | grounding cho tác nhân |
| Bài 2 | Hierarchical context-adaptive coordination | FJSP | rule-based, flat MARL, graph-only | điều phối dưới ràng buộc động |
| Bài 3 | Constraint-aware cooperative RLHF | Smart Grid | RLHF, safe RL, constrained RL | safe alignment |
| Bài 4 | Closed-loop CAMAS integration | 3 domain | open-loop, pairwise integration | synergy ở cấp kiến trúc |

## 8. Những sửa đổi cần thực hiện trong proposal

### Mục 1: Phần nêu vấn đề

Giữ ba vấn đề cốt lõi, nhưng làm rõ rằng mỗi vấn đề sẽ ánh xạ sang một đơn vị công bố, không chỉ là một module trong một hệ đơn khối.

### Mục 2: Mục tiêu và câu hỏi nghiên cứu

Cần viết lại theo hướng:

- RQ1 chỉ dành cho perception
- RQ2 chỉ dành cho coordination
- RQ3 chỉ dành cho alignment
- thêm RQ4 cho closed-loop integration

Gợi ý RQ4:

Mức lợi ích hệ thống do tích hợp closed-loop mang lại là bao nhiêu so với cấu hình open-loop hoặc tích hợp từng cặp module trên ba domain công nghiệp?

### Mục 3: Nền tảng lý thuyết

- chuyển LRMP hoàn toàn sang coordination, trừ khi sau này có bằng chứng rất mạnh rằng nó thực sự thuộc perception
- định nghĩa observability memory là grounding động từ vận hành thực tế, không phải chỉ là thêm một bộ nhớ
- định nghĩa alignment có xét ràng buộc là mô hình hóa utility và safety riêng, không chỉ là penalty term

### Mục 4: Logic closed-loop

Cần thêm interface rõ ràng và semantics của feedback. Nếu không, CAMAS rất dễ bị phản biện là một stack khái niệm chứ chưa phải kiến trúc thực thụ.

### Mục 5: Thiết kế thực nghiệm

Tách theo bài và theo domain neo:

- Bài 1: Maintenance
- Bài 2: FJSP
- Bài 3: Smart Grid
- Bài 4: cả 3 domain

Với mỗi bài, cần chỉ rõ:

- họ baseline
- ablation
- robustness test
- compute budget và reproducibility plan nếu có thể

### Mục 6: Lộ trình thực hiện

Thay cách ghi chung chung "Paper 1, Paper 2, Paper 3, Paper 4" bằng publication map thực:

- hướng tiêu đề bài báo
- novelty statement
- domain neo
- nhóm venue mục tiêu

### Mục 7: Kết quả kỳ vọng

Chuyển từ phát biểu chắc chắn sang giả thuyết nghiên cứu.

Cách viết nên dùng:

- target reduction in hallucination rate
- target improvement in safety compliance
- expected gain về profit/efficiency cần được kiểm chứng

Không nên viết như thể các con số này gần như chắc chắn đạt được.

## 9. Bộ RQ và giả thuyết đề xuất

### RQ1

Liệu lập luận bằng dual-memory có neo observability có thể giảm hallucination và tăng factual grounding trong tác nhân bảo trì tốt hơn các hệ semantic-only hoặc retrieval-only hay không?

Giả thuyết:

Dual-memory có neo observability sẽ giảm hallucination và cải thiện chất lượng ra quyết định có bằng chứng trong điều kiện bảo trì nhiễu và quan sát không đầy đủ.

### RQ2

Liệu điều phối đa tác nhân phân cấp với biểu diễn đồ thị thích ứng theo ngữ cảnh có thể cải thiện chất lượng scheduling và độ bền trước nhiễu động tốt hơn các tiếp cận phẳng hoặc biểu diễn tĩnh hay không?

Giả thuyết:

Điều phối phân cấp dựa trên đồ thị kết hợp LRMP sẽ cải thiện makespan, tardiness và robustness trước perturbation tốt hơn flat MARL và các baseline không dùng graph.

### RQ3

Liệu cooperative RLHF có xét constraint có thể cải thiện điều khiển đa tác nhân an toàn trong smart grid tốt hơn RLHF chuẩn và constrained RL hay không?

Giả thuyết:

Việc tách utility learning và safety feasibility learning sẽ giảm vi phạm constraint mà không làm sụp hiệu năng hệ thống.

### RQ4

Liệu tích hợp closed-loop giữa grounded perception, adaptive coordination và safe alignment có tạo ra lợi ích mức hệ thống vượt hơn cấu hình open-loop và pairwise integration trên các domain công nghiệp dị thể hay không?

Giả thuyết:

CAMAS closed-loop sẽ vượt các cấu hình module rời và open-loop về robustness, safety và long-horizon performance, với overhead chấp nhận được.

## 10. Nhóm venue mục tiêu

Nhóm venue ưu tiên:

- Knowledge-Based Systems
- Expert Systems with Applications
- Information Sciences

Gợi ý phù hợp:

- Bài 1 hợp với Knowledge-Based Systems hoặc ESWA
- Bài 2 hợp với ESWA, Information Sciences hoặc tạp chí Industrial AI nếu phần thực nghiệm đủ mạnh
- Bài 3 hợp với ESWA, Information Sciences hoặc venue AI cho smart grid
- Bài 4 hợp với Knowledge-Based Systems hoặc ESWA nếu phần kiến trúc và cross-domain validation đủ tốt

## 11. Rủi ro và giảm thiểu

### Rủi ro 1: novelty overlap

Giảm thiểu:

- Bài 1 chỉ nói về grounding
- Bài 2 chỉ nói về coordination
- Bài 3 chỉ nói về safe alignment
- Bài 4 chỉ nói về loop closure và architectural synergy

### Rủi ro 2: scope ba domain quá lớn

Giảm thiểu:

- mỗi bài module có một domain neo sâu
- phạm vi cả ba domain được dồn chủ yếu vào bài tích hợp

### Rủi ro 3: metric yếu hoặc mơ hồ

Giảm thiểu:

- thay metric mơ hồ bằng metric đã được cộng đồng công nhận
- nếu dùng metric mới thì phải định nghĩa toán học trước khi dùng làm kết quả headline

### Rủi ro 4: bị phản biện là chỉ ghép kỹ thuật có sẵn

Giảm thiểu:

- định nghĩa interface mới
- định nghĩa data flow mới
- định nghĩa feedback semantics
- tạo claim thực nghiệm mới xoay quanh closed-loop

## 12. Deliverable tối thiểu cho mỗi bài

Mỗi bài nên kết thúc với:

- một câu novelty claim
- một hình phương pháp
- một phát biểu bài toán hình thức
- một bộ dataset/domain neo
- ít nhất 3 baseline có ý nghĩa
- ít nhất 3 ablation
- một robustness experiment

Bài 4 cần thêm:

- sơ đồ interface
- giao thức chạy loop
- so sánh open-loop và closed-loop
- phân tích overhead

