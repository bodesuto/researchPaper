# Hướng Dẫn Thực Thi Từng Bước Cho Roadmap Luận Án CAMAS

## 1. Mục tiêu của file này

File này là bản hướng dẫn thực thi theo từng bước cho toàn bộ lộ trình nghiên cứu CAMAS ở mức luận án tiến sĩ. Mục tiêu không phải chỉ là nêu ý tưởng, mà là chỉ rõ bạn cần làm gì trước, làm gì sau, điều kiện nào mới được chuyển giai đoạn, và mỗi giai đoạn phải tạo ra các đầu ra học thuật nào.

File này được viết theo nguyên tắc:

- làm luận án trước, publish papers sau
- mỗi bước phải có đầu ra cụ thể
- mỗi giai đoạn phải có tiêu chí dừng
- không mở rộng sang bước tiếp theo khi bước hiện tại chưa đủ chắc

## 2. Cách đọc roadmap này

Toàn bộ quá trình được chia thành 6 lớp công việc:

1. Khóa bài toán và phạm vi luận án
2. Chuẩn bị hạ tầng nghiên cứu chung
3. Thực hiện Paper 1: Perception
4. Thực hiện Paper 2: Coordination
5. Thực hiện Paper 3: Alignment
6. Thực hiện Paper 4: Integration và hoàn thiện luận án

Trong mỗi lớp công việc, bạn cần theo cùng một chu trình:

1. đọc literature và khóa gap
2. khóa problem statement
3. khóa novelty claim
4. xác định dữ liệu và benchmark
5. xây baseline
6. xây phương pháp đề xuất
7. chạy ablation
8. chạy robustness test
9. viết paper draft
10. map kết quả vào chương luận án

## 2.1. Nếu bắt đầu từ hôm nay thì phải làm gì ngay

Đây là thứ tự thực thi thực tế nhất nếu hôm nay bạn bắt đầu làm luận án.

### Ngày 1

- Đọc lại [proposal_rewritten_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\proposal_rewritten_vi.md) và [paper_comparison_matrix_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\paper_comparison_matrix_vi.md).
- Tự viết lại bằng tay 4 ý sau vào một file note riêng:
  - bài toán trung tâm của luận án
  - 4 câu hỏi nghiên cứu
  - 4 novelty claim của 4 paper
  - thứ tự ưu tiên `Paper 1 -> Paper 2 -> Paper 4 -> Paper 3`
- Nếu bạn chưa tự viết lại trôi chảy được 4 ý này, chưa được bắt đầu thực nghiệm.

### Ngày 2

- Tạo cấu trúc thư mục nghiên cứu chuẩn.
- Tạo file literature tracking dạng bảng.
- Tạo file `experiment_template.md` hoặc bảng mẫu để lưu:
  - dataset
  - baseline
  - config
  - seed
  - metrics
  - kết quả chính
  - ablation
  - robustness

### Ngày 3

- Chỉ tập trung vào Paper 1.
- Chốt định nghĩa vận hành cho:
  - hallucination rate
  - evidence grounding score
  - grounded state
  - evidence set
- Nếu các khái niệm này còn mơ hồ, không chuyển sang code.

### Ngày 4-7

- Thu thập và chuẩn hóa dữ liệu maintenance.
- Viết tài liệu schema dữ liệu đầu tiên:
  - trường nào là entity
  - trường nào là timestamp
  - trường nào là log type
  - trường nào là source reliability
- Chạy một baseline rất đơn giản trước để biết dữ liệu có dùng được hay không.

### Tuần 2

- Hoàn thành toàn bộ baseline của Paper 1.
- Chưa làm mô hình đề xuất nếu baseline còn chưa chạy sạch.

### Tuần 3-4

- Làm mô hình đề xuất của Paper 1.
- Chạy thực nghiệm chính, ablation, stress test.
- Viết skeleton draft của Paper 1 ngay khi có bảng kết quả đầu tiên.

## 2.2. Nguyên tắc ra quyết định để giữ giải pháp khả thi

Trong toàn bộ quá trình, mỗi khi đứng giữa một phương án “đẹp hơn” và một phương án “làm được thật”, bạn phải chọn phương án làm được thật.

Cụ thể:

- Nếu một module có hơn 4 thành phần mới cùng lúc, phải giảm bớt.
- Nếu một benchmark chưa chạy được baseline sạch, không thêm phương pháp mới.
- Nếu một novelty không tạo ra chênh lệch rõ trong ablation, không giữ nó làm novelty trung tâm.
- Nếu một bài cần dữ liệu quá khó thu thập, phải đổi framing trước khi cố ép phương pháp.
- Nếu Paper 3 chưa có preference strategy chắc chắn, không được đẩy nó thành hướng ưu tiên số 1.
- Nếu Paper 4 chưa có interface rõ trên giấy, không được viết code tích hợp.

## 2.3. Mỗi bước phải tạo ra đầu ra gì

Đây là quy tắc bắt buộc để tránh nghiên cứu bị trôi vào đọc nhiều nhưng không tích lũy được.

### Sau mỗi bước đọc literature

Bạn phải tạo:

- 1 note tóm tắt paper
- 1 dòng trong bảng literature tracking
- 1 câu trả lời cho câu hỏi: “paper này giúp tôi khóa gap nào hoặc tránh overlap nào?”

### Sau mỗi bước chuẩn bị dữ liệu

Bạn phải tạo:

- 1 file mô tả schema
- 1 file mô tả cleaning rules
- 1 bảng thống kê số lượng mẫu trước và sau làm sạch
- 1 file nêu các lỗi dữ liệu còn tồn tại

### Sau mỗi bước chạy baseline

Bạn phải tạo:

- 1 config cố định
- 1 bảng kết quả baseline
- 1 đoạn nhận xét baseline nào là mạnh nhất
- 1 quyết định rõ: phương pháp đề xuất phải vượt cái gì

### Sau mỗi bước chạy phương pháp đề xuất

Bạn phải tạo:

- 1 bảng kết quả chính
- 1 bảng ablation
- 1 bảng robustness
- 1 đoạn error analysis
- 1 kết luận tạm thời: novelty đã đủ đứng chưa

### Sau mỗi giai đoạn paper

Bạn phải tạo:

- 1 draft bài báo
- 1 phần nội dung map vào luận án
- 1 danh sách reviewer risks
- 1 danh sách việc còn thiếu trước khi submit

## 3. Giai đoạn 0: Khóa bài toán luận án

### 3.1. Bạn phải làm gì

- Chốt một câu phát biểu bài toán trung tâm của luận án.
- Chốt bốn câu hỏi nghiên cứu RQ1-RQ4.
- Chốt bốn giả thuyết H1-H4.
- Chốt phạm vi domain:
  - Maintenance cho Paper 1
  - FJSP cho Paper 2
  - Smart Grid cho Paper 3
  - cả 3 domain cho Paper 4
- Chốt nguyên tắc: ba paper đầu là module papers, paper cuối là integration paper.

### 3.2. Đầu ra bắt buộc

- `proposal_rewritten_vi.md` phải ổn định ở phần:
  - problem statement
  - gap nghiên cứu
  - research insight
  - 4 RQ
  - publication mapping
- `paper_comparison_matrix_vi.md` phải ổn định để tránh overlap novelty.

### 3.3. Điều kiện mới được qua bước tiếp theo

- Bạn phải trả lời rõ được 6 câu sau mà không mâu thuẫn:
  - luận án giải bài toán gì
  - gap chính là gì
  - CAMAS khác gì với các hướng hiện có
  - mỗi paper đóng góp gì riêng
  - mỗi paper dùng domain nào để chứng minh
  - paper 4 tích hợp cái gì và không claim lại cái gì

## 4. Giai đoạn 1: Chuẩn bị hạ tầng nghiên cứu chung

### 4.1. Mục tiêu

Tạo toàn bộ nền tảng chung để sau này các paper không bị đứt đoạn vì thiếu dữ liệu, thiếu baseline, thiếu metric, hoặc thiếu pipeline thực nghiệm.

### 4.2. Bạn phải làm gì

#### Bước 1: Tạo thư mục nghiên cứu chuẩn

Bạn nên tổ chức workspace thành các phần:

- `data/maintenance`
- `data/fjsp`
- `data/smartgrid`
- `src/perception`
- `src/coordination`
- `src/alignment`
- `src/integration`
- `experiments/paper1`
- `experiments/paper2`
- `experiments/paper3`
- `experiments/paper4`
- `results/`
- `notes/`
- `drafts/`

Đầu ra cụ thể của bước này:

- bạn nhìn vào workspace là biết ngay file nào thuộc paper nào
- code, dữ liệu và kết quả không để lẫn nhau
- mỗi paper có chỗ lưu config và kết quả riêng

#### Bước 2: Tạo bảng theo dõi literature

Bạn cần một file bảng theo dõi tối thiểu các cột:

- paper title
- venue
- problem solved
- method core
- baseline used
- metrics
- limitation
- gap useful for me
- reusable idea
- not to overlap

Đầu ra cụ thể của bước này:

- sau 1-2 tuần bạn phải có một bảng đủ để nhìn vào là biết:
  - paper nào là closest baseline
  - paper nào reviewer có thể dùng để phản biện bạn
  - chỗ nào bạn không được claim lại

#### Bước 3: Chuẩn hóa nguyên tắc thực nghiệm

Bạn phải khóa ngay từ đầu:

- metric nào là metric headline của mỗi paper
- baseline nào là baseline bắt buộc
- mỗi paper phải có ít nhất 3 ablation
- mỗi paper phải có ít nhất 1 stress test
- mọi thực nghiệm phải có seed, config, log, bảng kết quả và script tái lập

Đầu ra cụ thể của bước này:

- bạn phải có một template thống nhất cho tất cả thực nghiệm
- mọi bảng kết quả sau này đều theo cùng format
- khi viết luận án và viết paper không phải dựng lại từ đầu

#### Bước 4: Chuẩn hóa cách viết note nghiên cứu

Mỗi khi đọc một paper, bạn phải ghi 5 ý:

- paper này giải bài toán gì
- novelty thật nằm ở đâu
- điểm mạnh nhất là gì
- điểm yếu nhất là gì
- mình có thể cải tiến ở đâu mà vẫn khả thi

### 4.3. Đầu ra bắt buộc

- cấu trúc thư mục nghiên cứu rõ ràng
- file theo dõi literature
- mẫu lưu config thực nghiệm
- mẫu lưu kết quả baseline, ablation, robustness

### 4.4. Sai lầm phải tránh

- đọc rất nhiều paper nhưng không trích ra gap cụ thể
- đổi ý liên tục về metric
- cài quá nhiều mô hình nhưng không có baseline sạch
- bắt đầu viết phương pháp trước khi hiểu benchmark

## 5. Giai đoạn 2: Thực hiện Paper 1 - Perception

### 5.1. Mục tiêu khoa học

Chứng minh rằng `observability-grounded dual-memory knowledge graph` giúp giảm hallucination và tăng grounding trong tác nhân bảo trì công nghiệp.

### 5.2. Từng bước bạn phải làm

#### Bước 1: Khóa bài toán cực cụ thể

Bạn phải viết rõ:

- hallucination trong bài này được định nghĩa vận hành như thế nào
- đầu ra của tác nhân là gì
- evidence set gồm những loại bằng chứng nào
- grounded state gồm những trường thông tin nào

Nếu chưa định nghĩa được 4 ý trên, chưa được code.

#### Bước 2: Chuẩn bị dữ liệu

Bạn phải thu thập và chuẩn hóa:

- knowledge graph nền hoặc tri thức thiết bị
- maintenance logs
- alarm/event traces
- execution history

Bạn cần làm:

- chuẩn hóa schema dữ liệu
- nối timestamp
- đánh dấu nguồn bằng chứng
- loại bỏ record thiếu nghiêm trọng
- xây mapping giữa log và thực thể trong KG

Đầu ra cụ thể của bước này:

- `schema_maintenance.md`
- `data_cleaning_report_paper1.md`
- `entity_mapping_table.csv` hoặc bảng tương đương
- một tập dữ liệu đủ sạch để chạy baseline đầu tiên

#### Bước 3: Xây baseline trước

Bạn phải chạy tối thiểu:

- semantic-only KG retrieval
- retrieval-only baseline
- KG-RAG hoặc dạng tương đương
- dual-memory không conflict checking

Làm baseline trước để biết mức khó dễ thật của bài toán.

Đầu ra cụ thể của bước này:

- `baseline_results_paper1.md`
- một bảng xếp baseline theo metric headline
- một quyết định rõ baseline mạnh nhất là gì

#### Bước 4: Xây phương pháp đề xuất

Bạn triển khai theo thứ tự:

1. semantic memory
2. observability memory
3. temporal retrieval
4. conflict checking
5. uncertainty scoring
6. grounded output formatter

Không nên làm đồng thời tất cả ngay từ đầu.

Cách làm khả thi nhất:

- làm bản đơn giản chạy được trước
- xác nhận pipeline đúng
- sau đó mới thêm temporal retrieval
- sau đó mới thêm conflict checking
- cuối cùng mới thêm uncertainty scoring

Nếu bản đơn giản còn chưa ổn, không được thêm thành phần mới.

#### Bước 5: Chạy thực nghiệm chính

Bạn cần đo:

- hallucination rate
- evidence grounding score
- factual consistency
- task success

#### Bước 6: Chạy ablation

Tối thiểu gồm:

- bỏ observability memory
- bỏ temporal retrieval
- bỏ conflict checking
- bỏ uncertainty estimation

#### Bước 7: Chạy stress test

Tối thiểu gồm:

- log thiếu
- sensor noise
- evidence conflict
- temporal drift

#### Bước 8: Viết kết luận khoa học của Paper 1

Bạn phải trả lời được:

- observability có thật sự tạo khác biệt hay không
- thành phần nào tạo lợi ích chính
- bài toán này có đủ mạnh để thành paper Q1 hay chỉ là workshop-level

Bạn phải chốt ra được 1 câu kết luận kiểu:

- “Observability memory là thành phần tạo chênh lệch chính, conflict checking là thành phần giúp ổn định dưới evidence conflict.”

Nếu chưa viết ra được câu như vậy, nghĩa là novelty chưa đủ sắc.

### 5.3. Điều kiện hoàn thành Paper 1

- metric headline tốt hơn baseline mạnh
- ablation chứng minh được vai trò của observability
- định nghĩa hallucination đủ chặt
- kết quả có thể kể thành một câu chuyện học thuật rõ

### 5.4. Đầu ra bắt buộc

- draft Paper 1
- phần chương luận án về grounded perception
- pipeline dữ liệu maintenance tái sử dụng được

## 6. Giai đoạn 3: Thực hiện Paper 2 - Coordination

### 6.1. Mục tiêu khoa học

Chứng minh rằng điều phối đa tác nhân phân cấp có biểu diễn ngữ cảnh động giúp scheduling tốt hơn trong FJSP động.

### 6.2. Từng bước bạn phải làm

#### Bước 1: Khóa problem framing

Bạn phải viết rõ:

- agent là ai
- action là gì
- reward gồm những chiều nào
- decision hierarchy gồm mấy tầng
- graph gồm những node và edge nào

#### Bước 2: Chọn benchmark

Ưu tiên:

- Barnes FJSP
- dynamic FJSP benchmark

Bạn cần khóa:

- instance nào dùng train
- instance nào dùng validation
- instance nào dùng test
- perturbation nào dùng cho robustness

Đầu ra cụ thể của bước này:

- `benchmark_protocol_paper2.md`
- danh sách instance train/val/test cố định
- danh sách perturbation scenarios cố định

#### Bước 3: Chạy baseline sạch

Tối thiểu:

- dispatch heuristics
- PPO/DQN
- flat MARL
- hierarchical MARL không graph
- graph RL không LRMP

#### Bước 4: Xây phiên bản khả thi nhất trước

Bạn nên làm thứ tự:

1. graph-based state encoder
2. hierarchical policy
3. robust training loop
4. sau đó mới thêm LRMP
5. sau cùng mới thêm MD-MDP nếu thực sự cần

Không nên bắt đầu bằng bản đầy đủ quá phức tạp.

Nguyên tắc khả thi:

- novelty trung tâm phải là `hierarchical graph-based coordination`
- LRMP chỉ giữ nếu nó tạo cải thiện có ý nghĩa
- MD-MDP chỉ giữ nếu reviewer thực sự thấy nó giúp diễn giải reward/action rõ hơn

Nếu LRMP và MD-MDP không giúp đủ rõ, bỏ bớt để cứu bài.

#### Bước 5: Chạy thực nghiệm chính

Bạn phải đo:

- makespan
- tardiness
- machine utilization
- adaptation under perturbation

#### Bước 6: Chạy ablation

Tối thiểu:

- bỏ hierarchy
- bỏ graph encoder
- bỏ LRMP
- bỏ MD-MDP

#### Bước 7: Chạy robustness test

Tối thiểu:

- machine breakdown
- arrival changes
- due-date perturbation
- processing-time uncertainty

#### Bước 8: Khóa novelty thật

Bạn phải tự hỏi:

- novelty thật của bài là hierarchy hay graph hay LRMP
- nếu bỏ một phần mà kết quả gần như giữ nguyên thì phần đó không nên là novelty trung tâm

Bạn phải viết ra một quyết định cuối:

- novelty trung tâm
- novelty phụ
- phần nào bỏ khỏi title và abstract

### 6.3. Điều kiện hoàn thành Paper 2

- baseline mạnh bị vượt rõ ràng
- hierarchy chứng minh được giá trị riêng
- metric sử dụng đều là metric chuẩn của scheduling
- bài không bị reviewer nhìn như “ghép encoder với RL”

### 6.4. Đầu ra bắt buộc

- draft Paper 2
- chương luận án về adaptive coordination
- bộ benchmark và config scheduling dùng lại được cho paper 4

## 7. Giai đoạn 4: Thực hiện Paper 3 - Alignment

### 7.1. Mục tiêu khoa học

Chứng minh rằng alignment có xét hard constraints giúp giảm safety violation trong smart grid mà không làm utility sụp đổ.

### 7.2. Từng bước bạn phải làm

#### Bước 1: Giảm tham vọng về dữ liệu ngay từ đầu

Bạn phải chấp nhận ngay:

- không bắt đầu bằng full human RLHF
- dùng `simulated expert preference` là chính
- human feedback thật chỉ dùng cho validation subset

Đây là quyết định để bài khả thi.

#### Bước 2: Chuẩn bị môi trường smart grid

Ưu tiên:

- IEEE 30
- IEEE 118
- IEEE 300

Bạn phải khóa:

- state representation
- action space
- hard constraints
- disturbance scenarios

#### Bước 3: Xây label strategy

Bạn cần hai luồng nhãn:

- preference labels
- safety labels

Preference labels có thể sinh từ:

- expert rules
- utility ranking
- pairwise comparison trajectories

Safety labels lấy từ:

- overload
- infeasible dispatch
- power balance violation
- margin violation

Đầu ra cụ thể của bước này:

- `preference_label_protocol_paper3.md`
- `safety_label_protocol_paper3.md`
- một tập labels nhỏ để kiểm tra pipeline trước

#### Bước 4: Xây baseline trước

Tối thiểu:

- RLHF chuẩn
- constrained RL
- safe RL
- handcrafted penalty reward

#### Bước 5: Xây phương pháp đề xuất

Theo thứ tự:

1. utility head
2. safety head
3. reward aggregation logic
4. Lagrangian constrained update
5. cooperative multi-agent update

Nguyên tắc khả thi:

- không nói quá nhiều biến thể tối ưu hóa
- khóa một lựa chọn chính là `Lagrangian constrained policy optimization`
- mọi thứ còn lại chỉ là phần phụ trợ

#### Bước 6: Chạy thực nghiệm chính

Bạn phải đo:

- safety violation rate
- constraint satisfaction rate
- return/profit
- robustness under disturbances

#### Bước 7: Chạy ablation

Tối thiểu:

- bỏ safety head
- bỏ Lagrangian constraint
- chỉ dùng preference
- chỉ dùng handcrafted penalty

#### Bước 8: Chạy robustness test

Tối thiểu:

- load surge
- line fault
- renewable fluctuation
- demand uncertainty

#### Bước 9: Khóa narrative học thuật

Bạn phải kể bài này theo hướng:

- bài toán chính là safe alignment under constraints
- RLHF chỉ là công cụ framing, không phải điểm phô diễn

Bạn phải tự kiểm:

- nếu bỏ cụm RLHF khỏi title, bài còn đứng được không

Nếu câu trả lời là không, bài đang quá phụ thuộc vào buzzword thay vì đóng góp thật.

### 7.3. Điều kiện hoàn thành Paper 3

- strategy tạo preference labels đủ thuyết phục
- violation giảm rõ
- utility không sụp đổ
- reviewer không thể bác ngay vì “không phải RLHF thật”

### 7.4. Đầu ra bắt buộc

- draft Paper 3
- chương luận án về safe alignment
- pipeline sinh preference labels và safety labels

## 8. Giai đoạn 5: Thực hiện Paper 4 - Integration

### 8.1. Mục tiêu khoa học

Chứng minh rằng việc đóng vòng giữa perception, coordination và alignment tạo ra `closed-loop gain` ở mức hệ thống.

### 8.2. Từng bước bạn phải làm

#### Bước 1: Không bắt đầu từ code tích hợp

Trước tiên bạn phải khóa trên giấy:

- interface của perception
- interface của coordination
- interface của alignment
- feedback nào là mandatory
- trigger nào dùng cho re-grounding

#### Bước 2: Chuẩn hóa interface

Tối thiểu phải có:

- perception output:
  - grounded_state
  - evidence_set
  - inconsistency_score
  - uncertainty_score
- coordination output:
  - action_candidates
  - policy_distribution
  - context_embedding
  - coordination_confidence
- alignment output:
  - updated_reward_model
  - updated_constraint_model
  - policy_update_signal
  - risk_aware_prior

Đầu ra cụ thể của bước này:

- `camas_interface_spec_vi.md`
- sơ đồ data flow giữa 3 module
- bảng mô tả trigger nào kích hoạt feedback nào

#### Bước 3: Xây open-loop baseline trước

Bạn phải có:

- perception only
- perception + coordination
- coordination + alignment
- full CAMAS không feedback
- full CAMAS có feedback

#### Bước 4: Xây feedback protocol

Bạn làm theo thứ tự:

1. static interface passing
2. episodic feedback
3. event-triggered feedback
4. uncertainty-aware re-grounding

Đây là thứ tự bắt buộc. Không được nhảy cóc sang feedback động phức tạp khi interface tĩnh còn chưa ổn.

#### Bước 5: Chạy thực nghiệm trên 3 domain

Bạn không cần chứng minh mọi thứ ở mọi domain. Bạn chỉ cần:

- maintenance để đo grounding improvement
- FJSP để đo coordination adaptation
- smart grid để đo safety-aware decision quality

#### Bước 6: Chạy ablation ở mức kiến trúc

Tối thiểu:

- bỏ mandatory feedback
- bỏ event-triggered re-grounding
- bỏ uncertainty propagation
- thay feedback động bằng fixed periodic feedback

#### Bước 7: Chạy overhead analysis

Bạn phải đo:

- latency
- compute cost
- update frequency
- gain so với overhead

Bạn phải trả lời được câu hỏi phản biện rất thực tế:

- “tăng chất lượng bao nhiêu và phải trả giá compute/latency bao nhiêu?”

### 8.3. Điều kiện hoàn thành Paper 4

- closed-loop gain dương và ổn định
- pairwise integration bị vượt
- feedback semantics chứng minh được tác dụng riêng
- bài không biến thành “siêu bài” ôm quá rộng

### 8.4. Đầu ra bắt buộc

- draft Paper 4
- chương luận án tích hợp
- sơ đồ kiến trúc cuối cùng của CAMAS

## 9. Giai đoạn 6: Viết luận án tiến sĩ hoàn chỉnh

### 9.1. Cấu trúc viết khuyến nghị

Bạn nên viết luận án theo cấu trúc:

1. Giới thiệu
2. Bối cảnh, bài toán, gap, research questions
3. Khung lý thuyết và tổng quan liên quan
4. Grounded Perception
5. Adaptive Coordination
6. Safe Alignment
7. Closed-Loop CAMAS Integration
8. Thảo luận tổng hợp
9. Kết luận và hướng phát triển

### 9.2. Cách map từ papers sang luận án

- Paper 1 không được copy nguyên văn thành chương 4, mà phải thêm phần nền tảng lý thuyết và liên hệ với CAMAS
- Paper 2 phải được viết như bước phát triển tiếp theo từ grounded state
- Paper 3 phải được viết như cơ chế kiểm soát tính khả thi và an toàn
- Paper 4 phải là chương kết nối và thống nhất toàn bộ luận án

### 9.3. Bạn phải làm gì trong giai đoạn viết luận án

- thống nhất notation giữa 4 bài
- thống nhất tên module
- thống nhất định nghĩa metric
- thống nhất câu chuyện nghiên cứu
- loại bỏ chỗ claim chồng nhau
- viết rõ giới hạn nghiên cứu

## 10. Tiến độ khuyến nghị theo thứ tự thực tế

### 10.1. Thứ tự nên làm

1. khóa proposal và ma trận 4 paper
2. dựng hạ tầng nghiên cứu chung
3. làm Paper 1
4. làm Paper 2
5. chuẩn bị dữ liệu Paper 3 song song
6. làm Paper 4 khi Paper 1 và 2 đủ ổn
7. hoàn thiện Paper 3
8. viết luận án hoàn chỉnh

### 10.2. Lý do của thứ tự này

- Paper 1 khả thi nhất, nên dùng để tạo kết quả sớm
- Paper 2 nối logic tự nhiên từ perception sang decision
- Paper 4 cần module đủ ổn mới chứng minh được gain
- Paper 3 rủi ro dữ liệu cao nên không nên đặt làm điểm mở màn

## 10.3. Kế hoạch thực thi theo 12 bước nối tiếp

Nếu bạn muốn nhìn toàn bộ roadmap như một chuỗi hành động tuyến tính, hãy đi đúng 12 bước này:

1. Chốt proposal, RQ, publication mapping.
2. Tạo hệ thống lưu literature, config, kết quả.
3. Chuẩn bị và làm sạch dữ liệu Paper 1.
4. Chạy baseline Paper 1.
5. Xây và kiểm chứng phương pháp Paper 1.
6. Viết draft Paper 1 và map sang chương luận án.
7. Chuẩn bị benchmark và baseline Paper 2.
8. Xây và kiểm chứng phương pháp Paper 2.
9. Chuẩn bị label strategy và môi trường cho Paper 3, nhưng chưa đẩy mạnh nếu chưa chắc dữ liệu.
10. Chuẩn hóa interface và xây open-loop baselines cho Paper 4.
11. Tích hợp closed-loop CAMAS và kiểm chứng gain.
12. Quay lại hoàn thiện Paper 3, rồi thống nhất 4 paper thành bản luận án hoàn chỉnh.

Mỗi bước chỉ được qua khi đã có đầu ra cụ thể bằng file, bảng kết quả hoặc draft.

## 11. Checklist bạn phải tự kiểm trước khi submit từng paper

### 11.1. Checklist học thuật

- problem statement có sắc không
- gap có thật không
- novelty có một câu rõ không
- baseline có đủ mạnh không
- ablation có chỉ ra được vai trò từng phần không
- metric headline có hợp domain không
- reviewer có thể bảo đây chỉ là ghép kỹ thuật hay không

### 11.2. Checklist thực nghiệm

- có seed cố định
- có config lưu lại
- có script tái lập
- có bảng kết quả baseline
- có bảng ablation
- có bảng robustness
- có phân tích lỗi

### 11.3. Checklist viết bài

- abstract có nói rõ problem-gap-method-result không
- introduction có nêu rõ limitation của literature không
- method section có đủ cụ thể để tái lập không
- experiments có trả lời trực tiếp RQ không
- conclusion có không overclaim không

## 12. Sai lầm lớn nhất bạn phải tránh trong toàn bộ roadmap

- cố làm đồng thời cả 4 paper từ đầu
- để novelty của các paper chồng lên nhau
- viết proposal theo hướng “hệ thống có rất nhiều kỹ thuật” thay vì “giải quyết một bài toán khoa học”
- dùng các con số kỳ vọng như thể kết quả chắc chắn
- không khóa baseline từ sớm
- chọn phương pháp quá đẹp trên giấy nhưng không đủ dữ liệu để làm thật
- làm Paper 4 quá sớm khi module còn chưa ổn
- biến Paper 3 thành bài RLHF quá rộng và không khả thi

## 13. Kết luận thực dụng

Nếu đi theo đúng roadmap này, bạn sẽ có một lộ trình đủ chặt để làm luận án tiến sĩ theo logic:

- bắt đầu từ một bài perception khả thi và dễ tạo kết quả
- mở rộng sang coordination với novelty vừa đủ mạnh vừa thực tế
- kiểm soát rủi ro alignment bằng cách dùng preference strategy thực dụng
- chỉ tích hợp closed-loop khi các module đã có bằng chứng độc lập

Đây là cách đi thực tế nhất để vừa bảo vệ được logic luận án, vừa tối đa hóa xác suất tạo ra các bài báo có profile Q1.
