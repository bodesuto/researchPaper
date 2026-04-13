# CAMAS Final Brainstorm Và Research Plan

## 1. Mục tiêu của file này

File này là bản tổng hợp cuối cùng của toàn bộ quá trình brainstorm và đề xuất cho CAMAS. Nội dung gom lại các quyết định quan trọng nhất từ các file đã xây dựng trước đó:

- [proposal_rewritten_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\proposal_rewritten_vi.md)
- [CAMAS_4Q1_implementation_blueprint.md](f:\Luận văn thạc sĩ\Paper\purpose\CAMAS_4Q1_implementation_blueprint.md)
- [paper1_perception_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\paper1_perception_vi.md)
- [paper2_coordination_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\paper2_coordination_vi.md)
- [paper3_alignment_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\paper3_alignment_vi.md)
- [paper4_integration_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\paper4_integration_vi.md)
- [paper_by_paper_q1_analysis_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\paper_by_paper_q1_analysis_vi.md)
- [improvement_actions_per_module_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\improvement_actions_per_module_vi.md)
- [final_novelty_and_q1_positioning_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\final_novelty_and_q1_positioning_vi.md)
- [deep_technical_novelty_analysis_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\deep_technical_novelty_analysis_vi.md)
- [improved_proposed_methods_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\improved_proposed_methods_vi.md)
- [step_by_step_master_plan_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\step_by_step_master_plan_vi.md)
- [repo_selection_checklist_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\repo_selection_checklist_vi.md)

File này có thể được xem như bản “chốt tư duy nghiên cứu” để bạn trao đổi với giáo viên hướng dẫn, chuẩn bị proposal, và bắt đầu triển khai luận án.

## 2. Luận điểm trung tâm của CAMAS

Luận điểm trung tâm của CAMAS là:

`Các tác nhân công nghiệp thất bại vì nhận thức không được neo vào dữ liệu vận hành, điều phối thiếu cấu trúc thích ứng, và căn chỉnh policy chưa xét hard constraints. CAMAS giải quyết ba điểm yếu này bằng một kiến trúc closed-loop liên kết grounded perception, adaptive coordination và safe alignment.`

Viết theo hướng paper:

`Industrial agents fail because they perceive without operational grounding, coordinate without adaptive structure, and align policies without hard-constraint awareness. CAMAS addresses these failures through a closed-loop architecture that links grounded perception, adaptive coordination, and safe alignment.`

Điều quan trọng: CAMAS không nên được viết như một hệ thống ghép nhiều kỹ thuật, mà phải được viết như một chuỗi nghiên cứu có logic tích lũy:

- state phải grounded
- decision phải adaptive
- policy phải safe
- loop phải tạo gain đo được

## 3. Nỗi đau thực tế khiến đề tài này cần phải nghiên cứu

Điểm còn thiếu trong nhiều proposal kỹ thuật không phải là thiếu thuật toán, mà là chưa làm người đọc cảm thấy `nếu không nghiên cứu bài này thì hệ thống ngoài thực tế sẽ tiếp tục thất bại ở đâu`. Với CAMAS, nỗi đau cần phải làm nổi bật không nằm ở mức “AI còn chưa tốt”, mà nằm ở chỗ các tác nhân hiện tại rất dễ thất bại đúng ở những điểm gây thiệt hại vận hành thật trong công nghiệp.

### 3.1. Nỗi đau 1: Quyết định có vẻ đúng nhưng sai với trạng thái vận hành thật

Trong môi trường công nghiệp, một khuyến nghị sai không chỉ là lỗi nội dung. Nó có thể dẫn đến:

- chuẩn đoán sai nguyên nhân lỗi
- kích hoạt sai quy trình bảo trì
- bỏ sót tín hiệu hỏng hóc quan trọng
- tăng downtime
- gây thay thế thiết bị không cần thiết
- kéo dài thời gian khôi phục hệ thống

Điểm đau ở đây là nhiều hệ hiện nay vẫn “trả lời hợp lý” nhưng không “đúng với trạng thái hệ thống đang diễn ra”. Đây là lý do grounded perception không chỉ là một cải tiến AI, mà là điều kiện bắt buộc để tác nhân được dùng trong vận hành thật.

### 3.2. Nỗi đau 2: Điều phối tốt ở benchmark nhưng yếu khi môi trường đổi trạng thái

Trong sản xuất và scheduling, giá trị thực không nằm ở việc tối ưu tốt trên một cấu hình tĩnh, mà ở việc hệ có còn điều phối tốt khi:

- máy hỏng đột ngột
- đơn hàng gấp xuất hiện
- deadline thay đổi
- tài nguyên bị nghẽn

Nhiều phương pháp hiện nay đạt kết quả tốt ở môi trường chuẩn hóa, nhưng khi bước sang môi trường có perturbation thật thì hiệu quả giảm mạnh. Điều này tạo ra một nỗi đau rất rõ trong công nghiệp: hệ điều độ có thể “thông minh trong mô phỏng” nhưng “thiếu tin cậy trong ca vận hành”.

### 3.3. Nỗi đau 3: Policy tối ưu utility nhưng không thể triển khai vì vi phạm ràng buộc

Trong smart grid hay các hệ cyber-physical, lợi ích kinh tế không thể được tối ưu bằng cách đánh đổi an toàn một cách ngầm định. Một policy tăng profit nhưng:

- vi phạm giới hạn đường dây
- tạo mất cân bằng tải
- làm tăng xác suất vượt ngưỡng an toàn
- đẩy hệ đến vùng vận hành rủi ro

thì vẫn là policy không thể đưa vào vận hành.

Nỗi đau ở đây là khoảng cách giữa “policy tốt trên mục tiêu tối ưu” và “policy chấp nhận được trong hệ vật lý thật”. Đây là lý do alignment trong CAMAS phải được viết như safe alignment dưới hard constraints, không phải preference learning chung chung.

### 3.4. Nỗi đau 4: Các module AI mạnh riêng lẻ nhưng không tạo được giá trị hệ thống

Một tổ chức công nghiệp có thể có:

- hệ chẩn đoán tốt
- hệ điều độ tốt
- hệ kiểm soát an toàn tốt

nhưng nếu ba lớp này không chia sẻ tín hiệu uncertainty, conflict và risk cho nhau thì toàn hệ vẫn ra quyết định kém.

Nỗi đau ở cấp kiến trúc là:

- perception không biết policy vừa suýt vi phạm constraint
- coordination không biết grounded state đang thiếu chắc chắn
- alignment không tác động ngược để perception re-ground đúng lúc

Từ đó, toàn hệ hoạt động như một pipeline rời rạc thay vì một tác nhân có vòng phản hồi thật sự. Đây chính là lý do bài tích hợp của CAMAS cần thiết về mặt khoa học và thực tiễn.

### 3.5. Vì sao nỗi đau này đủ lớn để thành luận án tiến sĩ

Đề tài này đáng làm ở mức luận án tiến sĩ vì nó không xử lý một lỗi cục bộ của một mô hình, mà xử lý một cấu trúc thất bại lặp lại trong nhiều hệ công nghiệp:

- nhận thức sai do thiếu grounding
- điều phối yếu do thiếu thích ứng
- policy không triển khai được do thiếu safety-aware alignment
- kiến trúc không tạo được lợi ích tổng thể do thiếu feedback loop

Nói cách khác, CAMAS không chỉ giải một bài toán mô hình, mà giải một lớp bài toán quyết định công nghiệp có tính hệ thống.

## 4. Tiềm năng ứng dụng công nghiệp của CAMAS

Một proposal mạnh không chỉ nói “có thể áp dụng”, mà phải chỉ ra `ai dùng`, `dùng ở đâu`, `giá trị vận hành nào được tạo ra`, và `lộ trình triển khai thực tế là gì`.

### 4.1. Ứng dụng trong bảo trì công nghiệp

Trong bảo trì công nghiệp, CAMAS có thể được triển khai như một lớp `decision support` cho kỹ sư bảo trì hoặc trung tâm vận hành.

Giá trị ứng dụng cụ thể:

- tổng hợp tri thức nền và tín hiệu vận hành để hỗ trợ chuẩn đoán sự cố
- phát hiện recommendation thiếu evidence hoặc mâu thuẫn với trạng thái thật
- ưu tiên kiểm tra những thành phần có uncertainty cao hoặc conflict cao
- hỗ trợ tạo explanation có thể truy vết bằng chứng

Người dùng cuối:

- kỹ sư bảo trì
- kỹ sư vận hành
- trung tâm giám sát thiết bị
- hệ thống quản lý tài sản kỹ thuật

Giá trị công nghiệp:

- giảm sai chuẩn đoán
- giảm thời gian downtime
- tăng độ tin cậy của hỗ trợ quyết định
- giảm chi phí bảo trì không cần thiết

### 4.2. Ứng dụng trong sản xuất linh hoạt và điều độ

Trong FJSP và sản xuất linh hoạt, CAMAS có thể được triển khai như một `adaptive scheduling assistant` hoặc một bộ lõi ra quyết định cho hệ điều độ thông minh.

Giá trị ứng dụng cụ thể:

- cập nhật chiến lược điều độ khi có máy hỏng hoặc đơn hàng gấp
- phân rã quyết định giữa tầng chiến lược và tầng dispatch để phản ứng nhanh hơn
- giảm makespan và tardiness trong môi trường có nhiễu động
- tạo cơ chế điều phối nhiều thực thể dưới ràng buộc tài nguyên biến đổi

Người dùng cuối:

- quản đốc sản xuất
- hệ MES/APS
- bộ phận lập kế hoạch và điều độ
- trung tâm vận hành nhà máy

Giá trị công nghiệp:

- tăng hiệu quả sử dụng máy
- giảm trễ đơn hàng
- giảm chi phí tái điều độ
- tăng độ bền vận hành khi môi trường thay đổi

### 4.3. Ứng dụng trong smart grid và điều hành năng lượng

Trong smart grid, CAMAS có thể được triển khai theo lộ trình:

- mô phỏng trước
- decision support
- human-in-the-loop
- autonomous-with-constraints

Giá trị ứng dụng cụ thể:

- hỗ trợ dispatch có xét tradeoff giữa utility và safety
- phát hiện trajectory có nguy cơ vi phạm constraint trước khi ra quyết định
- cập nhật policy dưới ràng buộc vật lý thay vì chỉ tối ưu kinh tế
- phản hồi ngược để perception tăng độ nhạy với tín hiệu risk và near-violation

Người dùng cuối:

- điều độ viên hệ thống điện
- trung tâm điều hành lưới
- hệ EMS/DMS
- đơn vị vận hành DER/VPP

Giá trị công nghiệp:

- giảm vi phạm an toàn
- giữ utility kinh tế ở mức chấp nhận được
- tăng độ tin cậy khi vận hành dưới bất định
- tạo nền cho tự động hóa có kiểm soát trong hệ năng lượng

### 4.4. Giá trị ở cấp doanh nghiệp và hệ thống

Nếu CAMAS thành công, giá trị của nó không chỉ nằm ở từng domain riêng lẻ, mà ở một lớp công nghệ lõi có thể tái sử dụng cho các hệ vận hành thông minh:

- lớp nhận thức có grounding vận hành
- lớp ra quyết định thích ứng theo ngữ cảnh
- lớp căn chỉnh policy dưới hard constraints
- lớp feedback kiến trúc giúp hệ cải thiện qua thời gian

Điều này tạo ra tiềm năng ứng dụng rộng hơn cho:

- nhà máy thông minh
- hạ tầng năng lượng
- hệ giám sát kỹ thuật
- nền tảng điều hành công nghiệp có AI

### 4.5. Lộ trình triển khai thực tế

CAMAS nên được trình bày với lộ trình ứng dụng thực tế theo 3 mức:

#### Mức 1: Decision Support

Hệ chưa ra quyết định tự động hoàn toàn, mà:

- tổng hợp evidence
- đề xuất action
- cảnh báo conflict và uncertainty

Đây là mức triển khai phù hợp nhất cho giai đoạn đầu và có tính chấp nhận cao trong công nghiệp.

#### Mức 2: Human-in-the-Loop

Hệ đề xuất action hoặc policy, con người phê duyệt hoặc chỉnh sửa.

Giá trị:

- tận dụng AI nhưng giữ kiểm soát vận hành
- tạo dữ liệu phản hồi chất lượng cao cho cải tiến tiếp theo

#### Mức 3: Autonomous-with-Constraints

Chỉ áp dụng khi:

- module perception đã đủ đáng tin
- coordination đủ ổn định
- alignment đủ mạnh để kiểm soát safety

Đây là mức triển khai dài hạn, phù hợp hơn cho một lộ trình nghiên cứu tiến sĩ và sau tiến sĩ.

## 5. Tên đề tài đề xuất

Tên đề tài nên giữ theo hướng:

`CAMAS: Kiến Trúc Đa Tác Nhân Nhận Thức Closed-Loop Cho Grounded Perception, Adaptive Coordination Và Safe Alignment Trong Các Hệ Kỹ Thuật Phức Tạp`

Tên tiếng Anh:

`CAMAS: A Closed-Loop Cognitive Multi-Agent Architecture for Grounded Perception, Adaptive Coordination, and Safe Alignment in Complex Engineering Systems`

Tên này rõ hơn các phiên bản liệt kê quá nhiều kỹ thuật vì nó nhấn vào:

- kiến trúc
- closed-loop
- ba năng lực chính
- domain là complex engineering systems

## 6. Phát biểu bài toán nghiên cứu

Bài toán nghiên cứu trung tâm của luận án là:

`Làm thế nào để thiết kế một kiến trúc tác nhân đa thành phần cho các hệ kỹ thuật phức tạp sao cho tác nhân vừa nhận thức đúng trạng thái hệ thống từ dữ liệu vận hành thực, vừa tạo ra quyết định phối hợp thích ứng trong môi trường động, vừa bảo đảm các quyết định đó không vi phạm các ràng buộc an toàn và vận hành?`

Bài toán này không phải là:

- bài toán retrieval riêng lẻ
- bài toán scheduling riêng lẻ
- bài toán RLHF riêng lẻ
- bài toán system integration chung chung

Nó là bài toán thiết kế kiến trúc ra quyết định cho hệ đa tác nhân dưới ba yêu cầu đồng thời:

- `grounding`: quyết định phải dựa trên trạng thái có căn cứ
- `adaptation`: quyết định phải thích ứng với phụ thuộc động và nhiễu môi trường
- `safety alignment`: quyết định phải thỏa hard constraints trong khi vẫn tối ưu utility

## 7. Gap nghiên cứu tổng thể

Gap nghiên cứu tổng thể có thể phát biểu như sau:

`Hiện chưa có một kiến trúc đa tác nhân closed-loop đủ rõ về phương pháp và đủ chặt về thực nghiệm để đồng thời giải quyết ba yêu cầu grounding, adaptive coordination và safety-aware alignment trong các hệ kỹ thuật phức tạp.`

Các gap thành phần:

- Các nghiên cứu hallucination/RAG/KG-RAG còn thiếu operational grounding dựa trên observability data có timestamp và execution history.
- Các nghiên cứu scheduling/MARL còn thiếu strategic hierarchy rõ để tách strategy-level coordination khỏi dispatch-level execution trong dynamic FJSP.
- Các nghiên cứu RLHF/preference learning chưa xử lý đầy đủ hard constraints vật lý trong cyber-physical systems.
- Các kiến trúc agent tích hợp thường thiếu interface chuẩn hóa, feedback semantics và metric đo closed-loop gain.

## 8. Kiến trúc nghiên cứu 4 paper

Roadmap CAMAS nên được tổ chức theo chiến lược:

`3 module papers + 1 integration paper`

Trong đó:

- Paper 1: Perception
- Paper 2: Coordination
- Paper 3: Alignment
- Paper 4: Integration

Ba paper đầu không cần chứng minh toàn bộ CAMAS. Mỗi paper chỉ cần chứng minh một novelty hẹp, rõ, đo được. Paper 4 mới gánh claim về kiến trúc closed-loop.

## 9. Thứ tự thực hiện khuyến nghị

Thứ tự khả thi nhất là:

1. Paper 1: Perception
2. Paper 2: Coordination
3. Paper 4: Integration
4. Paper 3: Alignment

Lý do:

- Paper 1 khả thi nhất, giúp tạo kết quả sớm.
- Paper 2 nối logic tự nhiên từ grounded state sang decision.
- Paper 4 nên làm khi Paper 1 và Paper 2 đã có interface ổn định.
- Paper 3 rủi ro cao nhất vì phụ thuộc preference strategy và smart grid control setup, nên chuẩn bị song song nhưng không nên làm paper đầu tiên.

## 10. Paper 1: Perception

### 10.1. Tên bài đề xuất

`Observability-Grounded Dual-Memory Knowledge Graph for Hallucination-Aware Industrial Maintenance Agents`

### 10.2. Domain neo

- Maintenance/Knowledge

### 10.3. Problem statement

Tác nhân bảo trì công nghiệp thường tạo ra chẩn đoán hoặc khuyến nghị hành động có vẻ đúng về mặt ngữ nghĩa nhưng không được hỗ trợ bởi trạng thái vận hành hiện tại, vì quá trình suy luận chủ yếu dựa trên tri thức tĩnh thay vì log, trace và lịch sử thực thi.

### 10.4. Gap

RAG, KG-RAG và dual-memory agent hiện tại đã cải thiện grounding, nhưng chưa mô hình hóa đủ rõ tính hiệu lực theo thời gian và mâu thuẫn giữa tri thức nền với dữ liệu observability trong bối cảnh bảo trì công nghiệp.

### 10.5. Novelty cuối cùng

`Bài báo đề xuất một dual-memory knowledge graph có neo observability, kết hợp temporal evidence retrieval với semantic-observability conflict validation để tạo grounded state có thể truy vết và giảm hallucination trong suy luận bảo trì.`

### 10.6. Phương pháp cải tiến

Phương pháp nên được gọi là:

`Conflict-Validated Temporal Dual-Memory Grounding`

Các khối chính:

- `Semantic Memory`: lưu tri thức nền về thiết bị, thành phần, failure modes, maintenance procedures.
- `Observability Memory`: lưu log, trace, sensor/event history, execution outcomes dưới dạng evidence có timestamp.
- `Temporal Evidence Retrieval`: truy xuất evidence theo semantic relevance, entity match, temporal recency, source reliability và execution consistency.
- `Semantic-Observability Conflict Validation`: phát hiện mâu thuẫn giữa tri thức nền và trạng thái vận hành hiện tại.
- `Grounded State Output`: sinh `grounded_state`, `evidence_set`, `inconsistency_score`, `uncertainty_score`.

### 10.7. Cải tiến kỹ thuật lõi

Lõi thật không phải dual-memory, mà là:

- temporal validity trở thành điều kiện của grounding
- observability có quyền bác bỏ semantic memory
- conflict trở thành tín hiệu đánh giá độ tin cậy của reasoning

### 10.8. Baseline bắt buộc

- semantic-only KG
- vector RAG
- KG-RAG
- MAKG-like maintenance RAG
- dual-memory without temporal retrieval
- dual-memory without conflict validation

Baseline mạnh nhất phải vượt:

- `KG-RAG/MAKG-like maintenance reasoning baseline`

### 10.9. Metric

Metric headline:

- hallucination rate

Metric phụ:

- evidence grounding score
- factual consistency
- maintenance task success
- inconsistency detection accuracy

### 10.10. Thực nghiệm

Main experiments:

- so sánh với RAG/KG-RAG/MAKG-like baseline

Ablation:

- bỏ observability memory
- bỏ temporal retrieval
- bỏ conflict validation
- bỏ uncertainty scoring

Stress test:

- missing logs
- noisy logs
- temporal drift
- conflicting evidence
- outdated semantic facts

### 10.11. Điều kiện đủ để Q1

Paper 1 có profile Q1 nếu:

- conflict validation tạo gain rõ so với dual-memory retrieval thông thường
- hallucination được định nghĩa bằng evidence trace rõ
- stress test chứng minh robustness khi dữ liệu vận hành thiếu, nhiễu hoặc mâu thuẫn
- baseline gần-domain được so sánh công bằng

## 11. Paper 2: Coordination

### 11.1. Tên bài đề xuất

`Hierarchical Graph-Based Multi-Agent Coordination for Dynamic Flexible Job Shop Scheduling`

### 11.2. Domain neo

- FJSP/Scheduling

### 11.3. Problem statement

Dynamic FJSP đòi hỏi các tác nhân điều phối dưới các phụ thuộc thay đổi giữa job, operation, machine và nhiễu động, trong khi flat MARL và graph-only scheduling thường thiếu cơ chế phân rã chiến lược rõ ràng.

### 11.4. Gap

Các phương pháp graph-attention MARL như MAMHSAN cải thiện biểu diễn và scheduling, nhưng chưa tách đủ rõ chiến lược điều độ tầng cao khỏi hành động dispatch tầng thấp trong điều kiện dynamic perturbations.

### 11.5. Novelty cuối cùng

`Bài báo đề xuất một framework điều phối đa tác nhân phân cấp dựa trên graph, tách quyết định chiến lược điều độ khỏi hành động dispatch và dùng biểu diễn graph thích ứng theo ngữ cảnh để tăng robustness trong dynamic FJSP.`

### 11.6. Phương pháp cải tiến

Phương pháp nên được gọi là:

`Hierarchical Context-Adaptive Graph Coordination`

Các khối chính:

- `Heterogeneous Graph State Modeling`: biểu diễn job, operation, machine, precedence, machine eligibility và resource contention.
- `Master Policy`: chọn strategy/subgoal/priority mode/bottleneck focus.
- `Worker Policies`: chọn machine assignment, operation dispatch, local sequencing.
- `Context-Adaptive Representation`: điều chỉnh embedding theo due-date pressure, machine congestion, breakdown status, tardiness risk.
- `MD-MDP`: chỉ nên giữ như formulation support cho action/reward đa chiều.

### 11.7. Cải tiến kỹ thuật lõi

Lõi thật không phải graph + MARL, mà là:

- tách strategy-level coordination khỏi dispatch-level execution
- chứng minh hierarchy tạo gain dưới dynamic perturbation
- context shift ảnh hưởng trực tiếp tới chiến lược điều phối

### 11.8. Baseline bắt buộc

- dispatch rules
- single-agent PPO/DQN
- flat MARL
- graph RL without hierarchy
- hierarchy without graph
- MAMHSAN-like graph-attention MARL baseline

Baseline mạnh nhất phải vượt:

- `MAMHSAN-like baseline`

### 11.9. Metric

Metric headline:

- makespan
- total tardiness

Metric phụ:

- machine utilization
- rescheduling cost
- robustness under perturbation
- convergence stability

### 11.10. Thực nghiệm

Main experiments:

- static FJSP benchmark
- dynamic FJSP benchmark hoặc perturbation scenarios

Ablation:

- no hierarchy
- no graph encoder
- no context adaptation/LRMP
- flat policy instead of master-worker
- no MD-MDP if MD-MDP được giữ

Stress test:

- machine breakdown
- urgent job arrival
- due-date shift
- processing-time uncertainty
- scale-up instance size

### 11.11. Điều kiện đủ để Q1

Paper 2 có profile Q1 nếu:

- hierarchy tạo gain riêng, không chỉ graph encoder tạo gain
- MAMHSAN-like baseline bị vượt công bằng
- dynamic perturbation là trục kiểm chứng chính
- LRMP chỉ giữ nếu ablation chứng minh có ích

## 12. Paper 3: Alignment

### 12.1. Tên bài đề xuất

`Constraint-Aware Preference-Guided Multi-Agent Optimization for Safe Smart Grid Control`

### 12.2. Domain neo

- Smart Grid

### 12.3. Problem statement

Trong smart grid, một policy tối ưu utility kinh tế nhưng vi phạm ràng buộc vật lý hoặc an toàn là không thể chấp nhận, trong khi RLHF và preference-based methods chuẩn không trực tiếp bảo đảm feasibility dưới hard constraints.

### 12.4. Gap

CoRLHF xử lý policy-reward mismatch trong LLM alignment, còn constrained RL/safe RL xử lý feasibility nhưng thiếu preference-guided utility modeling. Gap nằm ở việc kết hợp preference learning với hard-constraint control cho smart grid.

### 12.5. Novelty cuối cùng

`Bài báo đề xuất một framework tối ưu có hướng dẫn preference và xét ràng buộc, trong đó utility preference và safety feasibility được tách bằng dual-head reward model, còn policy được cập nhật bằng Lagrangian constrained optimization.`

### 12.6. Phương pháp cải tiến

Phương pháp nên được gọi là:

`Constraint-Aware Preference-Guided Policy Optimization`

Các khối chính:

- `Preference Generation Protocol`: simulated expert preference, utility-safety-aware ranking, expert-rule consistency, human validation subset nhỏ.
- `Dual-Head Reward Model`: utility head và safety/feasibility head.
- `Lagrangian Constrained Policy Update`: tối ưu utility dưới safety budget.
- `Utility-Safety Frontier Analysis`: báo cáo tradeoff thay vì chỉ báo cáo một điểm.

### 12.7. Cải tiến kỹ thuật lõi

Lõi thật không phải RLHF, mà là:

- tách utility preference khỏi safety feasibility
- ghép hai loại tín hiệu này trong constrained policy update
- biến safety từ penalty mềm thành constraint tối ưu

### 12.8. Baseline bắt buộc

- constrained RL
- safe RL
- handcrafted penalty reward
- preference-only without safety
- safety-only without preference
- dual-head without Lagrangian
- RLHF-like preference optimization without safety head

Baseline mạnh nhất phải vượt:

- `constrained RL/safe RL baseline`

### 12.9. Metric

Metric headline:

- safety violation rate

Metric phụ:

- constraint satisfaction rate
- return/profit
- operating cost
- load shedding
- utility-safety frontier
- robustness under disturbances

### 12.10. Thực nghiệm

Main experiments:

- IEEE 30 bus
- IEEE 118 bus
- IEEE 300 bus nếu đủ compute

Ablation:

- no safety head
- no utility head
- no Lagrangian
- no preference
- scalar penalty reward

Stress test:

- load surge
- line outage
- renewable fluctuation
- demand uncertainty
- forecast error

### 12.11. Điều kiện đủ để Q1

Paper 3 có profile Q1 nếu:

- dual-head reward model tốt hơn scalar reward/penalty
- constrained RL baseline bị vượt trên utility-safety frontier
- preference simulated được kiểm bằng human/expert validation subset
- không overclaim RLHF theo nghĩa có human feedback lớn

## 13. Paper 4: Integration

### 13.1. Tên bài đề xuất

`CAMAS: A Closed-Loop Cognitive Multi-Agent Architecture with Grounded Perception, Adaptive Coordination, and Safe Alignment`

### 13.2. Domain neo

- Maintenance
- FJSP
- Smart Grid

Nhưng claim chính không phải cross-domain generalization, mà là:

- `closed-loop gain`

### 13.3. Problem statement

Perception, coordination và alignment thường được phát triển như module độc lập hoặc pipeline một chiều, khiến chưa rõ feedback giữa các lớp này có tạo lợi ích đo được ở cấp hệ thống hay không.

### 13.4. Gap

Các kiến trúc agent hiện tại thường thiếu interface chuẩn hóa, feedback semantics và controlled open-loop versus closed-loop evaluation để đo architectural gain.

### 13.5. Novelty cuối cùng

`Bài báo đề xuất một giao thức tích hợp closed-loop cho hệ đa tác nhân nhận thức, chuẩn hóa interface và feedback semantics giữa các module, đồng thời chứng minh closed-loop gain đo được so với open-loop và tích hợp từng cặp.`

### 13.6. Phương pháp cải tiến

Phương pháp nên được gọi là:

`Closed-Loop Feedback-Semantic Integration Protocol`

Các khối chính:

- `Standardized Interface Layer`
- `Mandatory Feedback Semantics`
- `Event-Triggered Re-Grounding`
- `Closed-Loop Gain Evaluation`

### 13.7. Interface chuẩn

Perception output:

- grounded_state
- evidence_set
- inconsistency_score
- uncertainty_score

Coordination output:

- action_candidates
- policy_distribution
- context_embedding
- coordination_confidence

Alignment output:

- updated_reward_model
- updated_constraint_model
- policy_update_signal
- risk_aware_prior

### 13.8. Feedback semantics

Feedback từ Alignment phải tác động lại:

- Perception: điều chỉnh retrieval priority, conflict sensitivity, uncertainty threshold.
- Coordination: điều chỉnh action filtering, policy prior, risk-aware action selection.

Re-grounding được kích hoạt nếu:

- uncertainty vượt ngưỡng
- conflict score tăng
- near-violation xuất hiện
- safety risk tăng

### 13.9. Baseline bắt buộc

- perception only
- perception + coordination
- coordination + alignment
- full pipeline without feedback
- full pipeline with fixed feedback
- full pipeline with event-triggered feedback

Baseline mạnh nhất phải vượt:

- `full pipeline without feedback`

### 13.10. Metric

Metric headline:

- closed-loop gain

Metric phụ:

- end-to-end task success
- safety violation
- robustness
- efficiency/profit
- latency overhead
- compute overhead

### 13.11. Điều kiện đủ để Q1

Paper 4 có profile Q1 nếu:

- full closed-loop vượt full no-feedback
- feedback ablation chứng minh feedback semantics tạo lợi ích riêng
- closed-loop gain có công thức rõ
- overhead analysis trung thực
- không claim lại novelty của Paper 1-3

## 14. Bảng chốt final cho 4 paper

| Paper | Core novelty | Phương pháp cải tiến | Must-beat baseline | Headline metric | Q1 condition |
|---|---|---|---|---|---|
| Paper 1 | Temporal conflict-aware operational grounding | Conflict-Validated Temporal Dual-Memory Grounding | KG-RAG/MAKG-like | Hallucination rate | Conflict validation tạo gain rõ |
| Paper 2 | Strategic hierarchy under dynamic perturbation | Hierarchical Context-Adaptive Graph Coordination | MAMHSAN-like | Makespan/tardiness | Hierarchy tạo gain riêng |
| Paper 3 | Utility-safety separation under constrained update | Constraint-Aware Preference-Guided Policy Optimization | Constrained RL/safe RL | Safety violation rate | Frontier utility-safety tốt hơn baseline |
| Paper 4 | Formal feedback protocol with measurable gain | Closed-Loop Feedback-Semantic Integration Protocol | Full pipeline without feedback | Closed-loop gain | Feedback tạo gain riêng, overhead chấp nhận được |

## 15. Codebase strategy

Hiện tại workspace chưa có repo code nền. Các PDF và file markdown mới là thiết kế nghiên cứu.

Chiến lược codebase khả thi nhất:

- Paper 1: tự xây codebase perception, chỉ dùng retrieval/KG repo nhẹ nếu cần baseline.
- Paper 2: chọn một repo FJSP/scheduling RL hoặc graph RL gần nhất làm xương sống.
- Paper 3: chọn một repo constrained RL/safe RL cho control/smart grid làm xương sống; không dùng CoRLHF-LLM làm codebase chính.
- Paper 4: tự tích hợp từ module 1-2-3.

Nguyên tắc:

- mỗi paper chỉ có 1 repo chính
- tối đa 1 repo phụ
- baseline phải chạy sạch trước khi thêm method mới

## 16. Step-by-step triển khai

Thứ tự hành động:

1. Chốt proposal hiện tại làm bản chính.
2. Chốt 4 novelty statements.
3. Tạo literature tracking file.
4. Tạo experiment tracking template.
5. Bắt đầu Paper 1 bằng schema dữ liệu maintenance.
6. Làm sạch dữ liệu Paper 1.
7. Chạy baseline Paper 1.
8. Xây temporal dual-memory grounding.
9. Thêm conflict validation.
10. Chạy ablation và stress test Paper 1.
11. Viết draft Paper 1.
12. Chuyển sang Paper 2 với benchmark FJSP.
13. Chạy MAMHSAN-like/graph MARL baseline.
14. Thêm hierarchy.
15. Chỉ thêm LRMP nếu ablation chứng minh có ích.
16. Chuẩn bị Paper 3 bằng constrained RL baseline và preference protocol.
17. Chuẩn hóa interface cho Paper 4.
18. Chạy full pipeline without feedback.
19. Thêm mandatory feedback và event-triggered re-grounding.
20. Quay lại hoàn thiện Paper 3.
21. Ghép thành luận án.

## 17. Rủi ro lớn và cách giảm thiểu

### 17.1. Rủi ro 1: Reviewer nói “ghép kỹ thuật có sẵn”

Cách giảm:

- mỗi paper chỉ claim một novelty trung tâm
- dùng ablation chứng minh novelty đó tạo gain riêng
- Paper 4 chỉ claim closed-loop gain, không claim lại module novelty

### 17.2. Rủi ro 2: Paper 2 bị xem là MAMHSAN + thêm module

Cách giảm:

- định vị contribution là strategic hierarchy
- dynamic perturbation phải là trục evaluation chính
- LRMP chỉ là phụ trợ

### 17.3. Rủi ro 3: Paper 3 bị bác vì không phải RLHF thật

Cách giảm:

- đổi framing sang preference-guided constrained optimization
- dùng simulated expert preference và human/expert validation subset
- báo utility-safety frontier

### 17.4. Rủi ro 4: Paper 4 bị xem là system integration

Cách giảm:

- formalize interface
- formalize feedback semantics
- định nghĩa closed-loop gain
- có feedback ablation và overhead analysis

## 18. Kết luận cuối cùng

CAMAS có tiềm năng Q1 nếu bạn không viết nó như một hệ thống có quá nhiều kỹ thuật. Cách viết đúng là:

- Paper 1: `không phải dual-memory`, mà là `conflict-validated temporal operational grounding`.
- Paper 2: `không phải graph + MARL`, mà là `strategic hierarchy under dynamic perturbation`.
- Paper 3: `không phải RLHF for smart grid`, mà là `utility-safety separation under constrained policy optimization`.
- Paper 4: `không phải system integration`, mà là `formal feedback protocol with measurable closed-loop gain`.

Nếu giữ đúng bốn trục này, roadmap của bạn vừa có logic luận án tiến sĩ, vừa có profile công bố Q1 thực tế hơn.
