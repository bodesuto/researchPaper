# Checklist Chọn Repo/Codebase Để Bắt Đầu Triển Khai CAMAS

## 1. Mục tiêu của file này

File này dùng để chọn repo/codebase nền cho từng paper theo hướng khả thi nhất. Mục tiêu không phải là tìm repo “nghe mạnh”, mà là chọn repo giúp bạn:

- chạy được baseline nhanh
- sửa được để tạo novelty của riêng mình
- không bị chìm vào việc debug một hệ quá lớn
- đủ sạch để dùng làm nền cho paper và luận án

## 2. Nguyên tắc chọn repo

Mỗi paper chỉ nên có:

- 1 repo chính
- tối đa 1 repo phụ

Không nên lấy nhiều repo rồi ghép chắp vá.

Repo được chọn phải thỏa phần lớn các tiêu chí sau:

- gần với bài toán thật của paper
- có môi trường/dataset hoặc benchmark rõ
- có baseline tái lập được
- cấu trúc code đủ rõ để sửa
- không phụ thuộc vào hạ tầng quá nặng
- có đầu ra/metric phù hợp với paper của bạn

## 3. Tiêu chí chấm một repo

Chấm theo thang `1-5` cho từng tiêu chí:

- `Độ gần bài toán`: repo có gần đúng domain và objective của paper không
- `Dễ chạy`: cài đặt, dependency, dữ liệu có dễ khởi động không
- `Dễ sửa`: code có rõ, module hóa đủ để thêm novelty không
- `Baseline value`: repo có giúp tạo baseline mạnh không
- `Risk`: repo có quá cũ, quá rối hoặc quá khó debug không

Bạn nên chọn repo có:

- tổng điểm cao
- `Độ gần bài toán` và `Dễ sửa` là hai điểm cao nhất

## 4. Checklist chung trước khi chọn repo

Trước khi quyết định dùng một repo làm nền, bạn phải tự trả lời:

1. Repo này giúp tôi chạy baseline hay giúp tôi hiện thực novelty?
2. Nếu dùng repo này, phần novelty của tôi sẽ nằm ở module nào?
3. Tôi có hiểu đủ code để sửa không?
4. Repo này có đưa tôi đi xa khỏi domain thật không?
5. Nếu repo lỗi hoặc dừng được bảo trì, tôi có tự cứu được không?

Nếu không trả lời rõ được 3 câu đầu, không nên chọn repo đó.

## 5. Checklist theo từng paper

## 5.1. Paper 1: Perception

### Mục tiêu chọn repo

Tìm nền đủ nhẹ để:

- ingest dữ liệu
- retrieval evidence
- đánh giá grounding/hallucination

### Repo chính nên có

- module retrieval hoặc KG cơ bản
- code rõ để tự thêm dual-memory
- evaluation pipeline đơn giản

### Không nên chọn

- full agent framework quá nặng
- repo LLM orchestration phức tạp
- hệ yêu cầu cloud/service ngoài ngay từ đầu

### Điều phải tự viết

- dual-memory graph schema
- observability memory
- conflict checking
- temporal retrieval logic

### Quyết định thực dụng

Nếu có repo retrieval/KG đơn giản thì dùng làm baseline scaffold. Nếu không có, tự dựng từ đầu vẫn là lựa chọn tốt hơn là kéo một agent framework quá to.

## 5.2. Paper 2: Coordination

### Mục tiêu chọn repo

Tìm repo gần nhất với:

- FJSP hoặc scheduling RL
- graph-based decision making
- training loop ổn định

### Repo chính nên có

- environment scheduling rõ
- baseline heuristics hoặc RL sẵn
- chỗ để gắn graph encoder hoặc policy module mới

### Repo phụ nếu cần

- graph encoder/attention implementation nhỏ, dễ cấy vào

### Không nên chọn

- repo MARL quá tổng quát nhưng không có scheduling
- repo chỉ có graph model mà không có môi trường quyết định
- repo quá phụ thuộc vào distributed training nặng

### Điều phải tự viết

- hierarchical master-worker controller
- context-adaptive logic
- LRMP
- ablation hooks

### Quyết định thực dụng

Nếu tìm được repo FJSP + RL đủ gần thì chọn ngay làm repo chính. Nếu không, chọn repo graph RL có môi trường gần scheduling rồi tự làm environment wrapper.

## 5.3. Paper 3: Alignment

### Mục tiêu chọn repo

Tìm repo nền cho:

- constrained RL hoặc safe RL
- control/smart-grid-like environment
- training loop có constraint handling

### Repo chính nên có

- optimizer constrained rõ
- logging violation/safety metric
- policy training ổn định

### Repo phụ nếu cần

- reward model hoặc preference ranking model đơn giản

### Không nên chọn

- repo RLHF cho LLM làm xương sống chính
- repo chỉ mạnh ở language model training nhưng không có control environment
- repo cần lượng lớn human feedback thật

### Điều phải tự viết

- simulated preference generator
- dual-head reward model
- bridge giữa reward model và constrained optimizer
- validation subset protocol

### Quyết định thực dụng

Chọn repo constrained RL trước, rồi mới gắn lớp preference. Không làm ngược lại.

## 5.4. Paper 4: Integration

### Mục tiêu chọn repo

Paper 4 không cần một repo ngoài làm xương sống. Mục tiêu là chọn cách tổ chức code để ghép các module 1-2-3 lại với nhau.

### Repo chính nên có

- chính là workspace CAMAS của bạn sau khi đã có module Paper 1-3

### Không nên chọn

- một framework agent orchestration quá to rồi cố nhét các module vào

### Điều phải tự viết

- interface specification
- feedback protocol
- event-triggered re-grounding scheduler
- closed-loop evaluation harness

## 6. Quy trình chọn repo thật sự

Khi bạn tìm được một repo tiềm năng, hãy làm đúng 7 bước này:

1. Ghi tên repo, paper liên quan, link.
2. Ghi repo này dùng cho paper nào trong CAMAS.
3. Chấm 5 tiêu chí ở Mục 3.
4. Ghi rõ phần nào của repo sẽ reuse.
5. Ghi rõ phần nào bạn sẽ sửa hoặc viết mới.
6. Chạy thử một baseline tối thiểu.
7. Chỉ sau khi baseline chạy được mới khóa repo đó làm nền.

## 7. Mẫu bảng chọn repo

Bạn nên lưu theo mẫu:

| Repo | Paper CAMAS | Vai trò | Độ gần bài toán | Dễ chạy | Dễ sửa | Baseline value | Risk | Quyết định |
|---|---|---:|---:|---:|---:|---:|---:|---|
| repo A | Paper 1 | chính/phụ | 4 | 4 | 5 | 4 | 2 | Giữ/Bỏ |

## 8. Quyết định mặc định nên dùng ngay

Nếu chưa có thời gian khảo sát sâu repo, đây là quyết định mặc định hợp lý nhất:

- Paper 1: tự xây codebase perception
- Paper 2: tìm 1 repo FJSP hoặc scheduling RL gần nhất làm nền
- Paper 3: tìm 1 repo constrained RL/safe RL làm nền
- Paper 4: tự xây lớp integration từ các module trước

## 9. Dấu hiệu repo không nên dùng

- repo không có hướng dẫn tái lập cơ bản
- code quá cũ hoặc phụ thuộc nặng, khó chạy
- metric trong repo không liên quan trực tiếp đến paper của bạn
- muốn dùng repo nhưng không biết novelty của mình sẽ nằm ở đâu
- repo khiến bạn phải đổi luôn bài toán nghiên cứu để hợp code

## 10. Kết luận thực dụng

Chọn repo đúng không phải để tiết kiệm vài ngày code, mà để tránh mất vài tháng đi sai hướng.

Hướng khả thi nhất vẫn là:

- Paper 1 tự xây
- Paper 2 chọn repo scheduling/graph RL gần nhất
- Paper 3 chọn repo constrained RL gần nhất
- Paper 4 tự tích hợp

Sau khi chọn xong repo, việc tiếp theo không phải là thêm nhiều kỹ thuật mới, mà là chạy baseline đầu tiên thật sạch.
