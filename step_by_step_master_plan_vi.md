# Step-by-Step Master Plan Cho CAMAS

## 1. Mục tiêu

File này chỉ trả lời một câu hỏi: từ bây giờ bạn phải làm gì, theo đúng thứ tự nào, để hoàn thiện proposal, bắt đầu nghiên cứu, làm paper và ghép thành luận án.

Nguyên tắc:

- chỉ làm theo thứ tự
- chưa xong bước trước thì chưa qua bước sau
- mỗi bước phải có đầu ra cụ thể

## 2. Bước 1: Chốt bản proposal chính

### Việc phải làm

- Mở [proposal_rewritten_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\proposal_rewritten_vi.md).
- Đọc lại toàn bộ từ đầu đến cuối.
- Chỉ kiểm 5 thứ:
  - problem statement
  - gap nghiên cứu
  - insight nghiên cứu
  - 4 RQ
  - roadmap 4 paper

### Đầu ra phải có

- một bản proposal mà bạn xác nhận là `bản chính`
- không đổi cấu trúc lớn nữa

### Điều kiện qua bước tiếp

- bạn phải tự nói được trong 2 phút:
  - luận án giải bài toán gì
  - 4 paper khác nhau ở đâu

## 3. Bước 2: Chốt novelty từng paper

### Việc phải làm

- Mở:
  - [paper1_perception_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\paper1_perception_vi.md)
  - [paper2_coordination_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\paper2_coordination_vi.md)
  - [paper3_alignment_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\paper3_alignment_vi.md)
  - [paper4_integration_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\paper4_integration_vi.md)
- Với mỗi file, viết ra một câu:
  - novelty chính là gì
  - cái gì không claim lại

### Đầu ra phải có

- 4 câu novelty riêng
- 4 câu “không claim lại cái gì”

### Điều kiện qua bước tiếp

- không còn overlap novelty giữa 4 bài

## 4. Bước 3: Chốt thứ tự thực hiện

### Việc phải làm

- Khóa thứ tự cố định:
  1. Paper 1
  2. Paper 2
  3. Paper 4
  4. Paper 3

### Đầu ra phải có

- một ghi chú rõ trong note của bạn: đây là thứ tự triển khai chính thức

### Điều kiện qua bước tiếp

- bạn không còn ý định làm cả 4 paper cùng lúc

## 5. Bước 4: Dựng cấu trúc thư mục nghiên cứu

### Việc phải làm

- Tạo các thư mục:
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
  - `results`
  - `notes`

### Đầu ra phải có

- workspace sạch, nhìn vào biết từng phần nằm ở đâu

### Điều kiện qua bước tiếp

- không còn để dữ liệu, note và kết quả lẫn lộn

## 6. Bước 5: Tạo bảng theo dõi literature

### Việc phải làm

- Tạo một file bảng gồm các cột:
  - paper
  - problem
  - method
  - baseline
  - metric
  - limitation
  - gap useful for me
  - not to overlap

### Đầu ra phải có

- một file literature tracking

### Điều kiện qua bước tiếp

- ít nhất các paper nền chính của 4 module đã được điền vào bảng

## 7. Bước 6: Chọn codebase chiến lược

### Việc phải làm

- Dùng [repo_selection_checklist_vi.md](f:\Luận văn thạc sĩ\Paper\purpose\repo_selection_checklist_vi.md)
- Chốt:
  - Paper 1: tự xây
  - Paper 2: tìm repo scheduling RL hoặc graph RL
  - Paper 3: tìm repo constrained RL hoặc safe RL
  - Paper 4: tự tích hợp

### Đầu ra phải có

- một note quyết định codebase cho từng paper

### Điều kiện qua bước tiếp

- bạn biết Paper 1 sẽ code từ đâu

## 8. Bước 7: Bắt đầu Paper 1 bằng dữ liệu

### Việc phải làm

- Thu thập dữ liệu maintenance
- Chọn knowledge source/KG nền
- Xác định:
  - entity
  - event
  - timestamp
  - evidence source

### Đầu ra phải có

- `schema_maintenance.md`
- một tập dữ liệu thô đầu tiên

### Điều kiện qua bước tiếp

- bạn mô tả được dữ liệu của Paper 1 có những trường gì

## 9. Bước 8: Làm sạch dữ liệu Paper 1

### Việc phải làm

- chuẩn hóa timestamp
- bỏ record thiếu nặng
- map log vào entity trong KG
- chuẩn hóa kiểu event

### Đầu ra phải có

- `data_cleaning_report_paper1.md`
- dữ liệu sạch để chạy baseline

### Điều kiện qua bước tiếp

- baseline đầu tiên chạy được

## 10. Bước 9: Chạy baseline cho Paper 1

### Việc phải làm

- chạy semantic-only baseline
- chạy retrieval-only baseline
- nếu được, chạy KG-RAG baseline đơn giản

### Đầu ra phải có

- `baseline_results_paper1.md`
- bảng baseline đầu tiên

### Điều kiện qua bước tiếp

- biết baseline mạnh nhất là gì

## 11. Bước 10: Xây phương pháp Paper 1

### Việc phải làm

- xây semantic memory
- xây observability memory
- thêm temporal retrieval
- thêm conflict checking
- thêm uncertainty scoring

### Đầu ra phải có

- phiên bản đầu của mô hình đề xuất Paper 1

### Điều kiện qua bước tiếp

- mô hình chạy được trên cùng protocol với baseline

## 12. Bước 11: Chạy ablation và stress test cho Paper 1

### Việc phải làm

- ablation:
  - bỏ observability memory
  - bỏ temporal retrieval
  - bỏ conflict checking
- stress test:
  - log thiếu
  - noise
  - evidence conflict

### Đầu ra phải có

- bảng ablation
- bảng stress test

### Điều kiện qua bước tiếp

- biết thành phần nào là lõi của novelty

## 13. Bước 12: Viết draft đầu Paper 1

### Việc phải làm

- viết abstract
- viết introduction
- viết method
- viết experiments
- viết conclusion

### Đầu ra phải có

- draft đầu tiên của Paper 1

### Điều kiện qua bước tiếp

- bạn có thể gửi thầy hoặc tự review vòng 1

## 14. Bước 13: Bắt đầu Paper 2

### Việc phải làm

- chọn benchmark FJSP
- khóa state/action/reward
- chạy heuristics
- chạy baseline RL cơ bản

### Đầu ra phải có

- `benchmark_protocol_paper2.md`
- baseline table của Paper 2

### Điều kiện qua bước tiếp

- bạn biết bài toán scheduling này đo bằng metric gì

## 15. Bước 14: Xây core model Paper 2

### Việc phải làm

- thêm graph encoder
- thêm hierarchical policy
- đo kết quả
- chỉ sau đó mới cân nhắc LRMP

### Đầu ra phải có

- bản core model của Paper 2

### Điều kiện qua bước tiếp

- hierarchy + graph đã tạo chênh lệch rõ

## 16. Bước 15: Hoàn thiện Paper 2

### Việc phải làm

- thêm LRMP nếu thực sự có ích
- giữ MD-MDP chỉ khi cần
- chạy ablation
- chạy robustness
- viết draft

### Đầu ra phải có

- draft Paper 2

### Điều kiện qua bước tiếp

- novelty của Paper 2 đủ gọn và đủ mạnh

## 17. Bước 16: Chuẩn bị nền cho Paper 3

### Việc phải làm

- chọn environment smart grid
- định nghĩa safety constraints
- thiết kế simulated preference protocol

### Đầu ra phải có

- `preference_label_protocol_paper3.md`
- `safety_label_protocol_paper3.md`

### Điều kiện qua bước tiếp

- bạn biết nhãn preference và nhãn safety sẽ sinh ra thế nào

## 18. Bước 17: Bắt đầu Paper 4

### Việc phải làm

- viết interface chuẩn:
  - perception output
  - coordination output
  - alignment output
- xây open-loop baseline

### Đầu ra phải có

- `camas_interface_spec_vi.md`

### Điều kiện qua bước tiếp

- interface rõ trước khi tích hợp code

## 19. Bước 18: Tích hợp closed-loop cho Paper 4

### Việc phải làm

- thêm mandatory feedback
- thêm event-triggered re-grounding
- chạy open-loop vs closed-loop
- đo overhead

### Đầu ra phải có

- bảng closed-loop gain
- draft Paper 4

### Điều kiện qua bước tiếp

- Paper 4 chứng minh được lợi ích hệ thống

## 20. Bước 19: Quay lại hoàn thiện Paper 3

### Việc phải làm

- chạy constrained RL baseline
- thêm dual-head reward model
- thêm preference-guided update
- chạy utility-safety tradeoff
- viết draft

### Đầu ra phải có

- draft Paper 3

### Điều kiện qua bước tiếp

- Paper 3 không còn mơ hồ về dữ liệu preference

## 21. Bước 20: Ghép thành luận án

### Việc phải làm

- map từng paper vào từng chương
- thống nhất notation
- thống nhất metric
- thống nhất luận điểm trung tâm

### Đầu ra phải có

- skeleton hoàn chỉnh của luận án

### Điều kiện hoàn thành

- luận án đọc như một câu chuyện nghiên cứu thống nhất, không phải 4 bài ghép cơ học

## 22. Bước phải làm ngay hôm nay

Nếu chỉ chọn đúng việc để bắt đầu ngay hôm nay, bạn làm đúng 3 việc:

1. Chốt bản proposal hiện tại.
2. Tạo literature tracking file.
3. Bắt đầu schema dữ liệu cho Paper 1.

Nếu làm được 3 việc này, bạn đã bắt đầu đúng hướng.
