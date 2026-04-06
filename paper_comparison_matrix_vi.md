# Ma Trận Đối Sánh 4 Paper CAMAS

## 1. Mục đích của ma trận

File này dùng để kiểm tra nhanh xem bốn bài báo trong roadmap CAMAS đã tách biệt novelty đủ rõ hay chưa, có logic nối sang luận án tiến sĩ hay chưa, và bài nào nên được ưu tiên để tối đa hóa tính khả thi và tiềm năng công bố.

## 2. Ma trận đối sánh tổng thể

| Paper | Bài toán trung tâm | Domain neo | Novelty claim một câu | Baseline mạnh nhất cần vượt | Metric headline | Rủi ro khả thi lớn nhất | Venue family phù hợp | Vai trò trong luận án |
|---|---|---|---|---|---|---|---|---|
| Paper 1: Perception | Làm thế nào để giảm hallucination trong tác nhân công nghiệp khi trạng thái thực thay đổi liên tục? | Maintenance/Knowledge | Dual-memory KG có observability grounding giúp phát hiện mâu thuẫn giữa tri thức nền và bằng chứng vận hành để tạo grounded state đáng tin cậy hơn | Semantic-only KG, RAG/KG-RAG, retrieval-only, dual-memory không conflict checking | Hallucination rate | Dữ liệu log và evidence mapping không đủ sạch | Knowledge-Based Systems, Expert Systems with Applications | Tạo chương nền tảng về grounded perception và cung cấp `grounded_state` cho các bước sau |
| Paper 2: Coordination | Làm thế nào để điều phối đa tác nhân trong FJSP động khi phụ thuộc giữa job-operation-machine thay đổi liên tục? | FJSP/Scheduling | Hierarchical coordination với graph encoder và context adaptation giúp ra quyết định scheduling tốt hơn policy phẳng và graph-only coordination | Heuristic dispatch rules, flat MARL, hierarchical MARL không graph, graph RL không context adaptation | Makespan | Phương pháp bị quá dày thành phần, khó chứng minh vai trò riêng của từng phần | Engineering Applications of Artificial Intelligence, Expert Systems with Applications, Applied Soft Computing | Tạo chương về adaptive coordination và cung cấp `action_candidates/context_embedding` cho CAMAS |
| Paper 3: Alignment | Làm thế nào để học policy vừa tối ưu utility vừa không vi phạm hard constraints trong smart grid? | Smart Grid | Dual-head reward model kết hợp preference learning và safety learning trong constrained policy optimization giúp giảm violation mà không làm utility sụp đổ | RLHF chuẩn, safe RL, constrained RL, CoRLHF không safety head | Safety violation rate | Preference data strategy yếu hoặc quá phụ thuộc human labeling thật | Applied Energy, International Journal of Electrical Power and Energy Systems, Expert Systems with Applications | Tạo chương về safe alignment và cung cấp `constraint_model/policy_update_signal` |
| Paper 4: Integration | Việc đóng vòng perception, coordination, alignment có tạo lợi ích hệ thống đo được hay không? | Cả 3 domain | Closed-loop protocol với mandatory feedback và event-triggered re-grounding tạo `closed-loop gain` dương so với open-loop và pairwise integration | Open-loop pipeline, perception+coordination, coordination+alignment, full CAMAS không feedback loop | Closed-loop gain | Claim quá rộng, giao thức không đủ chặt, khó cô lập tác dụng của feedback | Information Sciences, Knowledge-Based Systems, Expert Systems with Applications | Tạo chương kiến trúc tích hợp và là luận điểm thống nhất của toàn bộ luận án |

## 3. Ma trận tách biệt novelty để tránh overlap

| Paper | Cái bài này phải claim | Cái bài này không được claim lại |
|---|---|---|
| Paper 1 | Grounded perception từ dual-memory và observability | Hierarchical coordination, safe RLHF, closed-loop gain toàn hệ |
| Paper 2 | Context-adaptive coordination trong scheduling động | Hallucination reduction như claim chính, reward alignment, kiến trúc tích hợp toàn hệ |
| Paper 3 | Alignment có xét hard constraints trong môi trường đa tác nhân | Grounded perception như novelty chính, graph scheduling như novelty chính, kiến trúc closed-loop hoàn chỉnh |
| Paper 4 | Architectural loop closure và feedback semantics | Novelty sâu của dual-memory, novelty sâu của hierarchy/graph encoder, novelty sâu của dual-head reward model |

## 4. Ma trận mức độ khả thi thực tế

| Paper | Khả thi triển khai | Độ mới học thuật | Tiềm năng Q1 | Kết luận thực dụng |
|---|---:|---:|---:|---|
| Paper 1 | 9.0/10 | 8.0/10 | 8.5/10 | Nên làm đầu tiên; đây là bài mạnh nhất để tạo đà khoa học và tiến độ luận án |
| Paper 2 | 7.0/10 | 7.5/10 | 7.5/10 | Nên làm thứ hai nhưng phải khóa novelty vào `hierarchical graph-based coordination` |
| Paper 3 | 5.5/10 | 8.0/10 | 6.5/10 | Có thể thành bài mạnh nếu kiểm soát tốt dữ liệu preference; nếu không sẽ rất rủi ro |
| Paper 4 | 7.0/10 | 7.0/10 | 7.0/10 | Có giá trị luận án rất cao, nhưng chỉ mạnh khi ba interface và protocol được định nghĩa chặt |

## 5. Khuyến nghị thứ tự triển khai

1. Paper 1 để khóa được bài toán, metric và pipeline dữ liệu khả thi nhất.
2. Paper 2 để mở rộng từ grounded state sang quyết định thích ứng trong môi trường động.
3. Paper 4 sau khi Paper 1 và Paper 2 đã đủ ổn định, vì đây là lúc closed-loop gain mới có cơ sở kiểm chứng.
4. Paper 3 có thể song song chuẩn bị dữ liệu, nhưng chỉ nên đẩy mạnh khi chiến lược preference labeling đã vững.

## 6. Cách dùng ma trận này khi làm luận án

- Dùng phần 2 khi trình bày roadmap công bố với giáo viên hướng dẫn hoặc hội đồng.
- Dùng phần 3 để tự kiểm tra xem bản thảo từng bài có đang bị trùng novelty hay không.
- Dùng phần 4 để quyết định ưu tiên đầu tư thời gian, compute và dữ liệu.
- Dùng phần 5 để giải thích vì sao roadmap không chỉ mang tính tham vọng mà còn có logic triển khai thực tế.
