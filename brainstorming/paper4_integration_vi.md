# Paper 4: Closed-Loop Integration Cho CAMAS

## 1. Problem statement

Các hệ perception, coordination và alignment thường được phát triển như các module riêng lẻ hoặc được xếp thành pipeline một chiều. Cách tiếp cận này khó tạo ra lợi ích ở cấp độ hệ thống, vì kết quả của vòng quyết định hiện tại không đủ khả năng quay trở lại cải thiện nhận thức và điều phối của vòng kế tiếp.

## 2. Gap nghiên cứu

Literature hiện thiếu một kiến trúc đủ rõ về phương pháp và đủ chặt về thực nghiệm để chứng minh rằng:

- grounded perception
- adaptive coordination
- safe alignment

khi được đóng vòng bằng interface và feedback semantics rõ ràng, sẽ tạo ra `closed-loop gain` vượt hơn open-loop hoặc pairwise integration. Phần lớn công trình hoặc dừng ở module-level innovation, hoặc mô tả integrated agent theo cách quá rộng và thiếu protocol kiểm chứng cụ thể.

## 3. Câu hỏi nghiên cứu và giả thuyết

### RQ

Liệu một `closed-loop protocol` với `mandatory feedback`, `event-triggered re-grounding` và interface chuẩn hóa giữa perception, coordination và alignment có thể tạo ra `closed-loop gain` về chất lượng quyết định có xét an toàn tốt hơn open-loop và pairwise integration hay không?

### Giả thuyết

Khi ba module được kết nối theo một feedback protocol tối thiểu, full CAMAS sẽ cho closed-loop gain dương so với open-loop và pairwise integration trên các domain công nghiệp động có hard constraints.

## 4. Đóng góp và novelty claim

### Novelty claim một câu

Bài báo đề xuất một giao thức tích hợp closed-loop cho kiến trúc CAMAS, trong đó feedback từ alignment tác động ngược có kiểm soát lên perception và coordination để tạo ra cải thiện ở cấp hệ thống thay vì chỉ cộng cơ học các cải tiến cục bộ.

### Đóng góp chính

- Chuẩn hóa interface giữa `grounded_state`, `context_embedding`, `constraint_model`, `policy_update_signal`.
- Xác định `mandatory feedback` và `event-triggered re-grounding`.
- Định nghĩa `closed-loop gain` làm metric kiến trúc chính.
- So sánh full CAMAS với `open-loop`, `pairwise integration` và `full CAMAS không feedback loop`.

### Phiên bản khả thi nhất của phương pháp

Để bài này đủ sâu và tránh trở thành một “siêu bài” quá rộng, phiên bản khả thi nhất nên khóa claim vào đúng một ý chính:

- full CAMAS tạo ra `closed-loop gain` dương so với open-loop và pairwise integration

Các ý như cross-domain generalization, scalability rộng, hoặc architecture for general intelligence chỉ nên là luận điểm phụ. Bài này mạnh khi nó chứng minh được `feedback semantics` có tác dụng thực nghiệm, không phải khi nó cố bao trùm toàn bộ giá trị của ba module trước.

### Điều cần tránh

Bài này không claim lại novelty sâu của:

- dual-memory perception
- hierarchical coordination
- constraint-aware RLHF

Claim chính của bài 4 là `architectural loop closure`.

## 5. Phương pháp đề xuất

### 5.1. Interface chuẩn hóa

#### Perception output

- `grounded_state`
- `evidence_set`
- `inconsistency_score`
- `uncertainty_score`

#### Coordination output

- `action_candidates`
- `policy_distribution`
- `context_embedding`
- `coordination_confidence`

#### Alignment output

- `updated_reward_model`
- `updated_constraint_model`
- `policy_update_signal`
- `risk_aware_prior`

### 5.2. Mandatory feedback

Alignment phải trả về ít nhất:

- `policy_update_signal`
- `updated_constraint_model`
- `risk_aware_prior`

để vòng perception kế tiếp có thể điều chỉnh retrieval priority, conflict sensitivity và uncertainty threshold.

### 5.3. Event-triggered re-grounding

Re-grounding được kích hoạt ngay nếu:

- uncertainty vượt ngưỡng
- phát hiện violation hoặc near-violation
- conflict score tăng mạnh

Nếu không, feedback được cập nhật theo episode.

### 5.4. Closed-loop protocol

1. Perception tạo grounded state từ semantic memory, observability memory và prior hiện tại.
2. Coordination sinh action candidates và context embedding.
3. Alignment đánh giá utility, feasibility và risk, sau đó cập nhật policy.
4. Alignment trả feedback tối thiểu.
5. Nếu có trigger, Perception re-ground ngay; nếu không, update theo episode kế tiếp.

## 6. So sánh với literature

### Baseline families

- perception only
- perception + coordination
- coordination + alignment
- full CAMAS không feedback loop
- open-loop sequential pipeline

### Điểm literature dễ bị phản biện

- nếu interface không rõ, bài sẽ bị xem là system integration chung chung
- nếu metric chính quá rộng, bài sẽ bị thành “siêu bài” nhưng không sâu
- nếu không chứng minh được tác dụng của feedback semantics, closed-loop sẽ chỉ là claim khái niệm

## 7. Thiết kế thực nghiệm

### Domain sử dụng

- maintenance để đo grounding
- FJSP để đo coordination adaptation
- smart grid để đo safety-aware decision quality

### Metrics

- closed-loop gain
- end-to-end task performance
- safety
- efficiency/profit
- robustness
- latency/compute overhead

`Cross-domain generalization` chỉ giữ là bằng chứng phụ, không phải headline claim.

### Baselines

- perception only
- perception + coordination
- coordination + alignment
- full CAMAS không feedback loop
- open-loop pipeline

### Ablations

- tắt alignment-to-perception feedback
- tắt uncertainty propagation
- tắt conflict-aware re-grounding
- thay event-triggered bằng fixed-cycle feedback

### Stress tests

- noisy observations
- delayed feedback
- partial observability
- preference inconsistency

## 8. Điều kiện để đủ sức Q1

### Đánh giá thực dụng hiện tại

- Khả thi triển khai: `7/10`
- Độ mới học thuật: `7/10`
- Tiềm năng Q1: `7/10`

### Khuyến nghị chiến lược

Đây là bài có thể mạnh ở mức Q1 nếu được kiểm soát phạm vi rất chặt. Điểm mạnh của bài không nằm ở số lượng module được tích hợp, mà ở việc chứng minh được protocol đóng vòng và metric closed-loop gain. Nếu giữ claim gọn và thực nghiệm đủ chặt, bài này có thể trở thành chương tích hợp tốt của luận án.

### Venue family phù hợp

- Knowledge-Based Systems
- Expert Systems with Applications
- Information Sciences nếu framing methodological đủ mạnh

### Điều kiện đủ tối thiểu

- phải có metric kiến trúc rõ, ở đây là `closed-loop gain`
- phải chứng minh feedback semantics bằng thực nghiệm
- phải kiểm soát scope claim, không ôm quá nhiều novelty
- phải có comparison công bằng với pairwise integration
- nên giới hạn bài ở một số protocol integration chủ đạo thay vì thử quá nhiều biến thể feedback

### Điều gì sẽ kéo bài xuống Q2/Q3

- bài chỉ mô tả integration ở mức kiến trúc khái niệm
- thiếu protocol rõ
- closed-loop gain không ổn định
- claim quá rộng kiểu “general intelligence across domains”

### Cách làm thực tế nhất

- Chỉ chọn một closed-loop protocol chuẩn và một số ablation thật có ý nghĩa.
- Không mở quá nhiều claim về transfer hay generalization.
- Dùng ba domain như ba lát cắt xác thực, nhưng report headline result xoay quanh closed-loop gain.

## 9. Rủi ro phản biện và cách phòng thủ

### Phản biện 1

“Đây chỉ là ghép ba module đã có.”

### Phòng thủ

Nhấn mạnh:

- interface được chuẩn hóa như một contribution
- feedback semantics là contribution
- event-triggered re-grounding là contribution
- metric closed-loop gain là contribution

### Phản biện 2

“Bài quá rộng và thiếu chiều sâu.”

### Phòng thủ

Khống chế claim:

- không claim novelty sâu từng module
- chỉ claim kiến trúc closed-loop và system-level gain

### Phản biện 3

“Cross-domain generalization chưa đủ thuyết phục.”

### Phòng thủ

Không dùng cross-domain generalization làm điểm bán chính. Chỉ dùng làm bằng chứng phụ cho độ bền kiến trúc.

## 10. Vai trò trong luận án tiến sĩ

Paper 4 là chương tích hợp trung tâm của luận án. Nếu Paper 1-3 trả lời ba điều kiện cần của một tác nhân công nghiệp mạnh, thì Paper 4 trả lời câu hỏi cấp luận án: khi các điều kiện cần đó được đóng vòng, hệ thống có tạo ra một đóng góp kiến trúc thực sự hay không.

### Mapping vào luận án

- chương tích hợp trọng tâm của luận án
- nơi thống nhất toàn bộ luận điểm khoa học
- cơ sở để bảo vệ CAMAS như một kiến trúc chứ không chỉ là tập hợp module
