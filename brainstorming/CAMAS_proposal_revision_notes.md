# Ghi Chú Sửa Proposal CAMAS

Tài liệu này là hướng dẫn chỉnh sửa trực tiếp proposal hiện tại để biến nó thành một đề xuất mạnh hơn theo hướng công bố.

## 1. Đổi cách định khung proposal

Điểm yếu hiện tại:

- Proposal đang giống một kiến trúc lớn ghép nhiều ý tưởng có sẵn.
- Logic công bố mới đang ẩn, chưa được viết tường minh.

Cần thay bằng:

- CAMAS là một chương trình nghiên cứu gồm 4 đơn vị công bố.
- Ba bài module dùng để xác lập novelty riêng.
- Một bài cuối dùng để xác thực kiến trúc closed-loop.

Câu gợi ý:

"Thay vì trình bày CAMAS như một khối thuật toán đơn lẻ, đề xuất này cấu trúc chương trình nghiên cứu thành bốn đơn vị công bố: ba đóng góp theo module và một đóng góp tích hợp vòng lặp khép kín."

## 2. Sửa hệ câu hỏi nghiên cứu

Vấn đề hiện tại:

- Proposal mới có RQ1-RQ3.
- Phần tích hợp đang được xem như đầu ra, chưa phải một câu hỏi nghiên cứu.

Cần sửa:

- thêm RQ4 tường minh

Cấu trúc nên dùng:

- RQ1: grounded perception
- RQ2: adaptive coordination
- RQ3: safe alignment
- RQ4: closed-loop integration

Câu gợi ý cho RQ4:

"RQ4: Kiến trúc CAMAS vòng lặp khép kín mang lại lợi ích hệ thống ở mức nào so với các cấu hình open-loop hoặc tích hợp từng cặp module trên ba domain công nghiệp?"

## 3. Chuyển LRMP về Coordination

Vấn đề hiện tại:

- LRMP đang xuất hiện dở dang ở cả Perception và Coordination.

Cần sửa:

- mặc định gán LRMP hoàn toàn cho Coordination

Lý do:

- Dễ bảo vệ LRMP như một cơ chế biểu diễn thích ứng theo ngữ cảnh cho quyết định điều phối hơn là cho grounding của perception.
- Giảm nhòe novelty giữa Bài 1 và Bài 2.

Câu gợi ý:

"Trong lộ trình công bố, LRMP được định vị là cơ chế biểu diễn thích ứng theo ngữ cảnh cho Coordination, thay vì trải rộng sang Perception."

## 4. Viết lại từng module như một đơn vị công bố

### Perception

Cần thêm:

- observability memory
- temporal validity
- conflict checking
- grounded output definitions

Cần tránh:

- claim lợi ích full CAMAS trong tiểu mục này

### Coordination

Cần thêm:

- hierarchical controller
- MD-MDP
- graph encoder
- LRMP
- dynamic scheduling setting

Cần tránh:

- dùng HHS như metric headline nếu chưa định nghĩa chặt

### Alignment

Cần thêm:

- dual-head reward model
- hard-constraint aware optimization
- tách preference và feasibility

Cần tránh:

- mô tả phương pháp như chỉ là "constraint penalty"

## 5. Thêm mục publications mapping

Vấn đề hiện tại:

- Proposal có nói đến các bài theo giai đoạn, nhưng chưa có ranh giới học thuật rõ.

Cần thêm một tiểu mục riêng:

"Publication Mapping and Novelty Separation"

Tiểu mục này cần trả lời:

- hướng tiêu đề từng bài
- novelty chính
- domain neo
- baseline chính
- phần nào được tái sử dụng từ bài trước
- phần nào không được lặp lại như đóng góp mới

## 6. Sửa thiết kế thực nghiệm

Vấn đề hiện tại:

- Proposal đang nói đánh giá rộng, nhưng chưa tách logic domain neo của từng bài với logic tích hợp.

Cần sửa:

### Đánh giá cho bài module

- Bài 1 dùng Maintenance là domain chính
- Bài 2 dùng FJSP là domain chính
- Bài 3 dùng Smart Grid là domain chính

### Đánh giá cho bài tích hợp

- dùng cả 3 domain
- so sánh open-loop, pairwise integration và full CAMAS

Câu gợi ý:

"Ba domain được giữ lại trong tổng thể đề xuất, nhưng mỗi bài module chỉ có một domain neo chính để đảm bảo độ sâu thực nghiệm và tính khả thi công bố."

## 7. Đổi cách viết kết quả kỳ vọng

Vấn đề hiện tại:

- Các chỉ số như hallucination reduction, safety index và profit gain đang được viết quá chắc.

Cần sửa:

Thay bằng:

- target hypotheses
- validation objectives
- expected trends cần kiểm chứng

Câu gợi ý:

"Các giá trị như giảm hallucination, cải thiện safety hoặc tăng profit được xem là các giả thuyết mục tiêu để kiểm chứng, không phải các kết quả gần như chắc chắn."

## 8. Định nghĩa interface giữa các module

Vấn đề hiện tại:

- Proposal mới mô tả tương tác ở mức ý tưởng, chưa ở mức interface.

Cần thêm một tiểu mục ngắn:

- Perception output:
  - grounded state
  - evidence set
  - inconsistency score
  - uncertainty score
- Coordination output:
  - action candidates hoặc policy distribution
  - context embedding
  - coordination confidence
- Alignment output:
  - updated reward model
  - constraint model
  - policy update signal

Việc này cần thiết để CAMAS được nhìn như một kiến trúc, không phải chỉ là tổ hợp khái niệm.

## 9. Bỏ hoặc định nghĩa lại HHS

Vấn đề hiện tại:

- HHS chưa rõ và dễ bị reviewer hỏi vặn.

Cần sửa:

Hoặc:

- định nghĩa HHS bằng toán học và giải thích rõ ý nghĩa

Hoặc:

- thay bằng metric chuẩn:
  - makespan
  - tardiness
  - utilization
  - robustness under perturbation
  - convergence stability

Khuyến nghị mặc định:

- không dùng HHS như metric headline nếu chưa có định nghĩa chặt

## 10. Thêm đoạn tự vệ trước phản biện

Proposal nên trả lời thẳng câu hỏi:

"Tại sao CAMAS không chỉ là việc ghép nhiều kỹ thuật có sẵn?"

Các điểm tự vệ nên có:

- mỗi module có một điều chỉnh mới cho đúng bài toán mục tiêu
- bài tích hợp đóng góp feedback semantics rõ ràng
- claim giá trị nằm ở loop closure và emergent system-level behavior
- output của các module được chuẩn hóa thành interface, từ đó phân tích được ở mức kiến trúc

## 11. Gợi ý lộ trình triển khai sửa lại

- Giai đoạn 1:
  - xây và kiểm chứng grounded dual-memory perception
  - đầu ra mục tiêu: draft Bài 1
- Giai đoạn 2:
  - xây và kiểm chứng hierarchical adaptive coordination
  - đầu ra mục tiêu: draft Bài 2
- Giai đoạn 3:
  - xây và kiểm chứng constraint-aware alignment
  - đầu ra mục tiêu: draft Bài 3
- Giai đoạn 4:
  - tích hợp tất cả module vào CAMAS và đánh giá closed-loop trên các domain
  - đầu ra mục tiêu: draft Bài 4

## 12. Khuyến nghị cách viết

Nên ưu tiên các cụm diễn đạt:

- "lộ trình nghiên cứu gồm bốn công bố"
- "giả thuyết mục tiêu"
- "domain neo"
- "tách biệt novelty"
- "closed-loop interface"
- "so sánh open-loop và closed-loop"

Nên tránh các cách diễn đạt:

- "chắc chắn có bốn bài Q1"
- "phương pháp đã chứng minh"
- "các metric kỳ vọng chắc chắn đạt được"

