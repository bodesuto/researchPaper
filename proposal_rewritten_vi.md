# CAMAS: Kiến Trúc Đa Tác Nhân Vòng Lặp Khép Kín Cho Nhận Thức Có Grounding, Điều Phối Thích Ứng Và Căn Chỉnh An Toàn

## 1. Tóm tắt điều hành

Đề xuất này xây dựng CAMAS, viết tắt của `Closed-Loop Cognitive Multi-Agent System`, như một khung nghiên cứu cho tác nhân AI trong các hệ kỹ thuật phức tạp. Vấn đề trung tâm của đề tài là các tác nhân hiện nay thường thất bại khi triển khai trong môi trường công nghiệp và cyber-physical do ba hạn chế đồng thời: `nhận thức thiếu grounding`, `điều phối thiếu thích ứng`, và `căn chỉnh chưa bảo đảm an toàn dưới hard constraints`.

Luận điểm cốt lõi của đề xuất là chất lượng quyết định trong các hệ vận hành thông minh không chỉ phụ thuộc vào sức mạnh của từng mô hình thành phần, mà phụ thuộc vào việc ba lớp `perception`, `coordination` và `alignment` có được liên kết thành một vòng phản hồi nhất quán hay không. Từ luận điểm đó, CAMAS được đề xuất như một kiến trúc vòng lặp khép kín, trong đó `Perception` tạo grounded state từ tri thức nền và dữ liệu observability, `Coordination` sinh hành động thích ứng theo ngữ cảnh động, và `Alignment` cập nhật policy dưới ràng buộc an toàn để phản hồi trở lại vòng nhận thức tiếp theo.

Luận án được tổ chức theo chiến lược tăng tiến từ module đến kiến trúc tổng thể. Trước hết, từng lớp phương pháp được phát triển và kiểm chứng độc lập trên domain neo tương ứng nhằm xác lập tính mới và tính khả thi. Sau đó, các module được chuẩn hóa interface và tích hợp thành một kiến trúc closed-loop chung. Cách tiếp cận này bảo đảm rằng luận án không chỉ tạo ra các cải tiến cục bộ, mà còn chứng minh được một đóng góp ở cấp độ kiến trúc cho tác nhân công nghiệp.

Về mặt học thuật, đề tài hướng tới bốn lớp kết quả: grounded perception, adaptive coordination, safe alignment và architectural loop closure. Về mặt triển khai, đề tài ưu tiên lộ trình `decision support -> human-in-the-loop -> autonomous-with-constraints`, qua đó giữ được tính thực tiễn mà không làm suy yếu độ chặt chẽ khoa học của luận án.

## 2. Bối cảnh và động lực nghiên cứu

### 2.1. Bối cảnh

Các hệ thống công nghiệp hiện đại như lưới điện thông minh, sản xuất linh hoạt, bảo trì dự báo và các nền tảng vận hành kỹ thuật số ngày càng yêu cầu các tác nhân AI có khả năng:

- nhận thức đúng trạng thái hệ thống trong điều kiện dữ liệu không hoàn hảo
- phối hợp nhiều tác nhân dưới các ràng buộc vận hành thay đổi theo thời gian
- tối ưu mục tiêu kinh tế nhưng không vi phạm giới hạn an toàn hoặc quy trình kỹ thuật
- thích ứng liên tục khi môi trường thay đổi

Tuy nhiên, phần lớn các tác nhân AI hiện nay mới chỉ mạnh ở một số khía cạnh riêng lẻ. Các hệ dựa trên LLM và RAG cải thiện khả năng truy vấn tri thức nhưng vẫn dễ sinh ảo giác hoặc đưa ra kế hoạch không phù hợp với trạng thái hệ thống thực. Các hệ reinforcement learning có thể tối ưu hành vi tốt trên môi trường mô phỏng nhưng thường gặp khó khăn khi phải phối hợp nhiều tác nhân trong môi trường có phụ thuộc phức tạp. Các phương pháp alignment như RLHF cho thấy hiệu quả trong việc học preference, nhưng chưa trực tiếp giải quyết được các `hard constraints` trong các hệ cyber-physical, nơi một hành động sai có thể gây vi phạm an toàn hoặc tổn thất vật lý.

### 2.2. Ba vấn đề cốt lõi

#### Vấn đề 1: Hallucination trong nhận thức

Nhiều tác nhân hiện nay tạo ra phát biểu hoặc đề xuất hành động không nhất quán với trạng thái vận hành thực tế. Trong môi trường công nghiệp, dạng hallucination này không chỉ gây sai về mặt nội dung mà còn có thể dẫn đến quyết định vận hành không an toàn. Nguyên nhân sâu xa là phần lớn hệ chỉ dựa vào tri thức tĩnh hoặc retrieval không có neo vào dữ liệu quan sát đang diễn ra.

#### Vấn đề 2: Điều phối thiếu thích ứng và tri thức điều phối còn cứng

Trong các bài toán nhiều tác nhân như FJSP, smart grid dispatch hoặc bảo trì cộng tác, quyết định tối ưu thường phụ thuộc mạnh vào quan hệ động giữa các thực thể, các ràng buộc tài nguyên và các nhiễu động theo thời gian. Các biểu diễn tĩnh hoặc policy phẳng thường khó nắm được cấu trúc phụ thuộc này, làm cho điều phối kém linh hoạt.

#### Vấn đề 3: Khoảng cách căn chỉnh và an toàn

Các cơ chế alignment hiện có, kể cả RLHF, thường nhắm tới việc học preference hoặc tối ưu utility tổng quát. Tuy nhiên, trong các hệ kỹ thuật phức tạp, mục tiêu an toàn không thể chỉ xem là một phần thưởng mềm. Các ràng buộc như giới hạn công suất đường dây, thời gian xử lý máy, mức tải tối đa, availability hay safety budget là các ràng buộc cứng và phải được đảm bảo trong quá trình học cũng như quá trình ra quyết định.

### 2.3. Phát biểu bài toán nghiên cứu

Bài toán nghiên cứu trung tâm của luận án có thể được phát biểu như sau: làm thế nào để thiết kế một kiến trúc tác nhân đa thành phần cho các hệ kỹ thuật phức tạp sao cho tác nhân vừa nhận thức đúng trạng thái hệ thống từ dữ liệu vận hành thực, vừa tạo ra quyết định phối hợp thích ứng trong môi trường động, vừa bảo đảm các quyết định đó không vi phạm các ràng buộc an toàn và vận hành?

Xét dưới dạng bài toán hệ thống, đầu vào của bài toán gồm:

- dữ liệu tri thức nền của miền ứng dụng
- dữ liệu observability theo thời gian như log, trace, sensor stream hoặc execution history
- trạng thái môi trường động và quan hệ phụ thuộc giữa các tác nhân/thực thể
- tín hiệu preference và tín hiệu vi phạm hoặc thỏa mãn constraint

Đầu ra mong muốn của hệ là:

- một `grounded state` phản ánh đúng trạng thái hệ thống tại thời điểm ra quyết định
- một tập `action candidates` hoặc policy có khả năng thích ứng với ngữ cảnh động
- một cơ chế cập nhật policy bảo đảm utility không tách rời khỏi safety
- một vòng phản hồi giúp kết quả của vòng hiện tại cải thiện chất lượng nhận thức và điều phối của vòng kế tiếp

Về bản chất, đây không phải chỉ là bài toán tối ưu đơn mục tiêu, cũng không chỉ là bài toán retrieval hay control riêng lẻ. Đây là bài toán thiết kế kiến trúc quyết định cho hệ đa tác nhân dưới ba yêu cầu đồng thời:

- `grounding`: quyết định phải dựa trên trạng thái có căn cứ
- `adaptation`: quyết định phải thích ứng với phụ thuộc động và biến động môi trường
- `safety alignment`: quyết định phải thỏa các hard constraints trong khi vẫn tối ưu utility

Do đó, bài toán nghiên cứu của luận án không thể giải quyết đầy đủ nếu chỉ cải thiện một thành phần đơn lẻ. Nó đòi hỏi một kiến trúc tích hợp trong đó perception, coordination và alignment được thiết kế đồng thời và được liên kết qua một closed-loop có semantics rõ ràng.

### 2.4. Gap nghiên cứu

Qua khảo sát các công trình nền, có thể thấy:

- Các nghiên cứu về hallucination thường tập trung vào retrieval, reflection hoặc semantic grounding, nhưng ít khai thác `observability data` như log, trace, sensor stream và execution history như một dạng bộ nhớ vận hành.
- Các nghiên cứu MARL hoặc scheduling optimization mạnh về tối ưu cục bộ nhưng thường thiếu cơ chế biểu diễn ngữ cảnh động đủ tốt để điều phối thích ứng.
- Các nghiên cứu RLHF mạnh về preference alignment nhưng chưa xử lý đầy đủ việc học dưới ràng buộc vật lý cứng trong môi trường đa tác nhân.
- Phần lớn công trình hiện nay tách rời perception, coordination và alignment. Rất ít nghiên cứu chứng minh được rằng việc `đóng vòng phản hồi` giữa ba lớp này tạo ra lợi ích emergent ở mức kiến trúc.

Từ tổng quan trên, gap nghiên cứu của luận án có thể được phát biểu ở ba mức:

Thứ nhất, `gap ở mức nhận thức`: hiện chưa có nhiều công trình kết hợp tri thức nền với observability memory theo một cấu trúc đủ mạnh để hỗ trợ grounded reasoning cho tác nhân công nghiệp. Phần lớn phương pháp dừng ở semantic retrieval hoặc evidence retrieval, chưa xử lý tốt việc mâu thuẫn giữa tri thức nền với trạng thái vận hành thực tế.

Thứ hai, `gap ở mức điều phối`: các nghiên cứu coordination hiện có hoặc mạnh ở tối ưu hành động, hoặc mạnh ở biểu diễn cấu trúc quan hệ, nhưng còn thiếu một framework đồng thời xử lý được phân cấp quyết định, phụ thuộc động giữa các thực thể và biểu diễn thích ứng theo ngữ cảnh.

Thứ ba, `gap ở mức căn chỉnh và kiến trúc`: RLHF và các biến thể alignment hiện nay chủ yếu học theo preference, trong khi các hệ cyber-physical đòi hỏi cơ chế tối ưu có ràng buộc an toàn rõ ràng. Đồng thời, vẫn thiếu các công trình chứng minh được rằng khi grounded perception, adaptive coordination và safe alignment được đóng vòng trong một kiến trúc chung, hệ thống tạo ra lợi ích ở cấp độ toàn cục chứ không chỉ là phép cộng cơ học của các cải tiến cục bộ.

Từ đó, gap nghiên cứu trung tâm của đề tài là: hiện chưa có một kiến trúc đa tác nhân closed-loop đủ rõ về phương pháp và đủ chặt về thực nghiệm để đồng thời giải quyết ba yêu cầu `grounding`, `adaptive coordination` và `safety-aware alignment` trong các hệ kỹ thuật phức tạp.

### 2.4.1. Cấu trúc chung giữa ba domain mục tiêu

Mặc dù proposal sử dụng ba domain ứng dụng khác nhau là bảo trì công nghiệp, sản xuất linh hoạt và smart grid, ba domain này không được lựa chọn một cách rời rạc. Chúng cùng chia sẻ bốn đặc tính cấu trúc khiến CAMAS có thể được xem là một kiến trúc chung thay vì ba lời giải tách biệt:

- đều có `observability stream`, tức dữ liệu vận hành liên tục dưới dạng log, sự kiện, cảm biến hoặc trạng thái hệ thống
- đều có `quyết định đa tác nhân hoặc đa thực thể`, nơi hành vi của một thành phần ảnh hưởng đến phần còn lại
- đều tồn tại `hard constraints`, ví dụ giới hạn kỹ thuật, giới hạn tài nguyên, thời gian, an toàn hoặc availability
- đều có `nhiễu động theo thời gian`, khiến quyết định tối ưu không thể dựa trên biểu diễn tĩnh

Do đó, ba domain này được dùng như ba lát cắt khác nhau của cùng một lớp bài toán: hệ vận hành thông minh cần nhận thức có grounding, điều phối thích ứng và căn chỉnh an toàn dưới constraint. Đây là cơ sở học thuật để biện minh cho việc CAMAS vừa có domain neo riêng theo từng bài, vừa có thể tích hợp thành một kiến trúc chung.

### 2.5. Luận điểm trung tâm và insight nghiên cứu

Insight cốt lõi của đề xuất là: trong các hệ kỹ thuật phức tạp, chất lượng quyết định không chỉ phụ thuộc vào sức mạnh suy luận của từng mô hình thành phần, mà phụ thuộc vào việc ba lớp nhận thức, điều phối và căn chỉnh có được liên kết thành một vòng phản hồi nhất quán hay không. Nếu nhận thức không được neo vào observability, tác nhân dễ tạo ra trạng thái sai. Nếu điều phối không được biểu diễn theo ngữ cảnh động, tác nhân dễ tối ưu cục bộ nhưng phối hợp kém. Nếu alignment không mô hình hóa explicit hard constraints, tác nhân có thể tối ưu utility nhưng vẫn đưa ra quyết định không an toàn.

Từ insight đó, CAMAS không được xây như một hệ ghép nối tuyến tính giữa nhiều kỹ thuật, mà như một kiến trúc có logic lớp rõ ràng. `Perception` chịu trách nhiệm tạo grounded state từ tri thức nền và bằng chứng vận hành; `Coordination` tạo hành động thích ứng từ grounded state dưới các phụ thuộc động; `Alignment` cập nhật policy theo preference nhưng đồng thời kiểm soát feasibility và safety. Giá trị khoa học của CAMAS nằm ở giả thuyết rằng khi ba lớp này được đóng vòng và trao đổi qua các interface chuẩn hóa, hệ thống sẽ đạt lợi ích emergent về robustness, safety và long-horizon performance mà từng module rời rạc không tạo ra được.

## 3. Mục tiêu nghiên cứu

### 3.1. Mục tiêu tổng quát

Xây dựng và kiểm chứng CAMAS như một kiến trúc closed-loop cho các hệ kỹ thuật phức tạp, trong đó:

- Perception tạo ra biểu diễn trạng thái có grounding và có độ tin cậy
- Coordination tạo ra hành động thích ứng và cộng tác tốt dưới ràng buộc động
- Alignment cập nhật policy theo preference nhưng vẫn tuân thủ hard constraints
- tín hiệu phản hồi từ alignment quay trở lại perception để cải thiện vòng ra quyết định kế tiếp

### 3.2. Mục tiêu cụ thể

- Đề xuất một cơ chế `observability-grounded dual-memory knowledge graph` để giảm hallucination trong tác nhân bảo trì công nghiệp.
- Đề xuất một cơ chế `hierarchical context-adaptive multi-agent coordination` cho các bài toán scheduling động nhiều tác nhân.
- Đề xuất một cơ chế `constraint-aware cooperative RLHF` cho các môi trường smart grid có ràng buộc an toàn.
- Thiết kế và kiểm chứng giao diện closed-loop giữa ba module trên nhiều domain để chứng minh giá trị hệ thống của CAMAS.

### 3.3. Phương pháp nghiên cứu tổng thể của luận án

Luận án này được triển khai theo phương pháp `thiết kế - xây dựng - kiểm chứng - tích hợp`, kết hợp giữa nghiên cứu lý thuyết, phát triển phương pháp và thực nghiệm trên benchmark cùng dữ liệu vận hành. Thay vì xây toàn bộ hệ thống ngay từ đầu, luận án đi theo chiến lược tăng tiến từ module đến kiến trúc tổng thể. Cách đi này phù hợp với bản chất của bài toán vì CAMAS không phải một mô hình đơn lẻ, mà là một kiến trúc nhiều lớp trong đó tính đúng đắn của vòng tích hợp phụ thuộc vào độ vững của từng thành phần.

Phương pháp nghiên cứu được tổ chức theo bốn bước logic:

1. `Mô hình hóa vấn đề và xác lập giả thuyết`: xác định rõ ba điểm nghẽn khoa học gồm hallucination, điều phối thiếu thích ứng và alignment chưa bảo đảm an toàn; từ đó xây dựng các giả thuyết H1-H4 tương ứng.
2. `Thiết kế và kiểm chứng theo module`: mỗi vấn đề được giải quyết bằng một module phương pháp riêng, được phát triển và kiểm chứng độc lập trên domain neo để bảo đảm tính rõ ràng của novelty và tính khả thi thực nghiệm.
3. `Chuẩn hóa interface và tích hợp closed-loop`: sau khi từng module đạt được tiêu chí tối thiểu, tiến hành chuẩn hóa đầu vào, đầu ra và semantics của feedback để tạo thành một kiến trúc chung.
4. `Đánh giá hệ thống ở mức luận án`: thay vì chỉ báo cáo kết quả cục bộ của từng module, luận án phải chứng minh được lợi ích ở cấp hệ thống của CAMAS so với cấu hình open-loop hoặc tích hợp không đầy đủ.

Từ góc độ phương pháp khoa học, luận án sử dụng bốn loại kỹ thuật bổ trợ cho nhau:

- `nghiên cứu tổng quan và phân tích khoảng trống` để xác lập nền tảng lý thuyết
- `thiết kế thuật toán và mô hình` để hình thành các cơ chế mới cho perception, coordination và alignment
- `thực nghiệm đối sánh có kiểm soát` với baseline, ablation và stress test để kiểm chứng giả thuyết
- `đánh giá tích hợp đa miền` để xác minh rằng đóng góp của luận án không chỉ có giá trị ở một mô-đun riêng lẻ mà còn ở cấp kiến trúc chung

Như vậy, lộ trình luận án được tổ chức theo logic phụ thuộc: Perception là nền để hình thành grounded state; grounded state là đầu vào đáng tin cậy cho Coordination; Coordination chỉ có ý nghĩa thực tế khi được Alignment kiểm soát dưới hard constraints; và chỉ khi ba lớp này được đóng vòng, luận án mới chứng minh được đóng góp kiến trúc của CAMAS.

## 4. Câu hỏi nghiên cứu và giả thuyết

### RQ1

Liệu lập luận dựa trên dual-memory có neo observability có thể giảm hallucination và tăng factual grounding trong tác nhân bảo trì tốt hơn các hệ semantic-only hoặc retrieval-only hay không?

Giả thuyết H1:

Dual-memory có neo observability sẽ làm giảm hallucination và tăng chất lượng quyết định có bằng chứng, đặc biệt trong điều kiện log nhiễu, cảm biến thiếu hoặc tri thức vận hành bị trôi theo thời gian.

### RQ2

Liệu điều phối đa tác nhân phân cấp với biểu diễn đồ thị thích ứng theo ngữ cảnh có thể cải thiện chất lượng scheduling và độ bền trước nhiễu động tốt hơn các tiếp cận phẳng hoặc biểu diễn tĩnh hay không?

Giả thuyết H2:

Kết hợp hierarchical MARL, graph-based state modeling, MD-MDP và LRMP sẽ cải thiện các chỉ số makespan, tardiness, utilization và robustness trong FJSP động so với flat MARL và các baseline không dùng biểu diễn ngữ cảnh động.

### RQ3

Liệu cooperative RLHF có xét constraint có thể cải thiện điều khiển đa tác nhân an toàn trong smart grid tốt hơn RLHF chuẩn và constrained RL truyền thống hay không?

Giả thuyết H3:

Việc tách utility learning và safety feasibility learning trong reward model sẽ giúp giảm constraint violations trong khi vẫn duy trì hiệu quả kinh tế chấp nhận được.

### RQ4

Liệu tích hợp closed-loop giữa grounded perception, adaptive coordination và safe alignment có tạo ra lợi ích ở cấp độ hệ thống tốt hơn các cấu hình open-loop hoặc chỉ tích hợp từng cặp module hay không?

Giả thuyết H4:

CAMAS closed-loop sẽ vượt các cấu hình module rời hoặc open-loop về long-horizon performance, robustness và safety, với overhead tính toán ở mức chấp nhận được.

## 5. Khung lý thuyết và ánh xạ vấn đề - giải pháp

### 5.1. Từ hallucination đến grounded perception

Các công trình gần đây về generative agents cho thấy vấn đề hallucination không thể xử lý triệt để chỉ bằng retrieval từ tri thức tĩnh. Trong môi trường vận hành thực, log, trace, sensor reading và execution history đóng vai trò như một lớp bằng chứng có tính kiểm chứng. Do đó, proposal này xem `observability` không phải là dữ liệu phụ mà là thành phần cốt lõi của nhận thức.

Giải pháp đề xuất là `dual-memory knowledge graph`, gồm:

- `Semantic memory`: lưu tri thức miền tương đối ổn định như loại thiết bị, cấu trúc hệ thống, quy trình bảo trì, quan hệ thành phần.
- `Observability memory`: lưu bằng chứng vận hành có tính thời gian như cảnh báo, trạng thái cảm biến, lịch sử hành động, kết quả thực thi và trace.

Từ hai bộ nhớ này, tác nhân có thể kiểm tra:

- phát biểu nào có căn cứ từ quan sát gần nhất
- phát biểu nào chỉ đúng về mặt tri thức nền nhưng đã lỗi thời so với trạng thái hiện tại
- kế hoạch nào mâu thuẫn với execution history

Điểm mới ở đây là cơ chế `memory conflict checking`, cho phép phát hiện các mâu thuẫn giữa tri thức nền và thực tế quan sát được. Cơ chế này biến grounding từ một thao tác truy xuất dữ liệu sang một thao tác kiểm tra nhất quán giữa các loại bằng chứng.

### 5.2. Từ điều phối cứng đến coordination thích ứng theo ngữ cảnh

Các bài toán điều phối nhiều tác nhân trong sản xuất linh hoạt hoặc vận hành phân tán thường có ba đặc tính:

- phụ thuộc quan hệ giữa nhiều loại thực thể
- quyết định có cấu trúc phân cấp
- môi trường biến động theo thời gian

Do đó, một policy phẳng hoặc embedding tĩnh khó nắm được bản chất bài toán. Proposal này ánh xạ vấn đề trên sang một framework coordination gồm:

- `Hierarchical MARL` để tách quyết định chiến lược và tác nghiệp
- `MD-MDP` để biểu diễn bài toán có nhiều chiều hành động và reward
- `Heterogeneous/temporal graph encoding` để nắm quan hệ giữa operation, machine, job và trạng thái thời gian
- `LRMP` để cập nhật biểu diễn theo ngữ cảnh thay vì cố định

Trong logic này, `LRMP` được định vị rõ là một phần của `Coordination`, không thuộc `Perception`. Vai trò của nó là giúp coordinator thay đổi biểu diễn tùy theo trạng thái scheduling hiện tại, mức độ quá tải, thứ tự ưu tiên và cấu trúc phụ thuộc giữa các thực thể.

### 5.3. Từ preference alignment đến safe alignment có xét ràng buộc

RLHF và các biến thể cooperative reward optimization đã cho thấy hiệu quả trong việc căn chỉnh mô hình theo preference. Tuy nhiên, trong smart grid hoặc các hệ cyber-physical, preference không thể thay thế các quy tắc an toàn. Một quyết định có utility cao nhưng vi phạm giới hạn công suất hay cân bằng tải là quyết định không chấp nhận được.

Vì vậy, proposal này đề xuất mở rộng CoRLHF theo hướng `constraint-aware cooperative RLHF`, với hai ý chính:

- reward model học `utility/preference`
- constraint model hoặc safety head học `feasibility/safety`

Thay vì gom tất cả vào một scalar reward, cách tiếp cận này tách biệt tín hiệu kinh tế và tín hiệu an toàn. Trong proposal này, cơ chế tối ưu chính được chọn là `Lagrangian constrained policy optimization`, trong đó utility objective và safety constraint được tối ưu đồng thời thông qua một hệ số phạt thích nghi. Các phương án như safety budget control chỉ được xem là hướng mở rộng hoặc baseline so sánh, không phải lựa chọn cốt lõi của phương pháp.

Điểm mới học thuật nằm ở việc chuyển alignment từ `soft preference optimization` sang `safe cooperative decision alignment` phù hợp với các hệ nhiều ràng buộc cứng, đồng thời khóa rõ một lựa chọn tối ưu hóa đủ chặt để có thể kiểm chứng và phản biện.

### 5.4. Từ module rời rạc đến closed-loop architecture

Nhiều hệ thống hiện nay xử lý perception, planning hoặc alignment theo dạng pipeline một chiều. Hạn chế của cách này là chất lượng của vòng quyết định kế tiếp không được cải thiện từ phản hồi của vòng hiện tại.

Proposal này xem CAMAS như một `closed-loop cognitive architecture`, trong đó:

- Perception không chỉ là đầu vào của Coordination, mà còn được định hướng lại bởi thông tin bất định và policy prior từ Alignment
- Coordination không chỉ xuất hành động, mà còn xuất độ tin cậy điều phối và biểu diễn ngữ cảnh
- Alignment không chỉ là bước hậu kiểm, mà là một bộ cập nhật tác động ngược trở lại quá trình grounding và ra quyết định

Điểm then chốt là định nghĩa được `interface`, `feedback semantics` và `tần suất cập nhật`, từ đó chứng minh rằng closed-loop mang lại lợi ích ở cấp độ hệ thống. Trong proposal này, closed-loop được hình thức hóa theo ba quy tắc tối thiểu:

- `feedback bắt buộc`: Alignment phải trả về ít nhất `policy_update_signal`, `updated_constraint_model` và một `risk-aware prior` để Perception dùng ở vòng tiếp theo
- `kích hoạt phản hồi`: feedback được cập nhật theo episode ở giai đoạn đầu; với các trạng thái có risk cao hoặc vi phạm constraint, cơ chế `event-triggered re-grounding` được kích hoạt ngay
- `tác động phản hồi`: risk-aware prior làm thay đổi retrieval priority, conflict sensitivity và uncertainty threshold của Perception, từ đó ảnh hưởng trực tiếp tới grounded state của vòng sau

Với định nghĩa này, CAMAS không chỉ là pipeline có feedback tùy ý, mà là một kiến trúc có vòng cập nhật tối thiểu, có nghĩa vận hành và có thể kiểm chứng thực nghiệm.

## 6. Kiến trúc CAMAS đề xuất

### 6.1. Tổng quan

CAMAS gồm ba module chức năng chính:

1. `Perception`
2. `Coordination`
3. `Alignment`

Ba module này vận hành theo chu trình:

`Perception -> Coordination -> Alignment -> Perception`

Chu trình này diễn ra lặp theo episode hoặc theo event, tùy domain.

### 6.2. Module Perception

#### Đầu vào

- dữ liệu cảm biến
- alarm/log/trace
- tri thức nền
- execution history
- policy prior hoặc uncertainty cue từ Alignment nếu có

#### Thành phần chính

- semantic memory graph
- observability memory graph
- temporal retrieval
- conflict checking
- uncertainty estimation

#### Đầu ra chuẩn hóa

- `grounded_state`
- `evidence_set`
- `inconsistency_score`
- `uncertainty_score`

Module này chịu trách nhiệm biến dữ liệu hỗn hợp thành một trạng thái có căn cứ, có bằng chứng và có mức tin cậy định lượng được.

### 6.3. Module Coordination

#### Đầu vào

- grounded_state
- evidence_set
- uncertainty_score
- context constraints theo domain

#### Thành phần chính

- heterogeneous/temporal graph encoder
- LRMP
- master policy
- worker policies
- MD-MDP action-reward structure

#### Đầu ra chuẩn hóa

- `action_candidates`
- `policy_distribution`
- `context_embedding`
- `coordination_confidence`

Module này không chỉ trả lời "nên làm gì", mà còn cung cấp thông tin về mức độ chắc chắn của phương án điều phối và cấu trúc ngữ cảnh mà quyết định đang dựa vào.

### 6.4. Module Alignment

#### Đầu vào

- action_candidates hoặc policy output
- trajectory outcomes
- preference labels
- constraint satisfaction signals

#### Thành phần chính

- utility head
- safety/feasibility head
- cooperative reward refinement
- constrained policy optimization

#### Đầu ra chuẩn hóa

- `updated_reward_model`
- `updated_preference_model`
- `updated_constraint_model`
- `policy_update_signal`

### 6.5. Cơ chế phản hồi closed-loop

Alignment phản hồi ngược trở lại Perception thông qua một hoặc nhiều cơ chế:

- thay đổi prior cho retrieval
- ưu tiên re-grounding ở những tình huống có risk cao
- đánh dấu những trạng thái từng dẫn tới vi phạm constraint để tăng mức cảnh giác của perception
- điều chỉnh ngưỡng uncertainty hoặc conflict sensitivity

Từ đó, ở vòng quyết định sau, Perception không chỉ nhìn thế giới theo cùng một cách như trước, mà có thể tập trung hơn vào các tín hiệu đã được chứng minh là quan trọng cho an toàn và hiệu quả hệ thống.

Để tránh mơ hồ trong triển khai, proposal này giả định giao thức closed-loop chuẩn như sau:

1. `Perception` xây grounded state từ semantic memory, observability memory và prior của vòng trước.
2. `Coordination` sinh action candidates cùng context embedding và coordination confidence.
3. `Alignment` đánh giá utility, feasibility và risk của trajectory hiện tại, sau đó cập nhật reward/policy theo Lagrangian constrained optimization.
4. `Alignment` gửi lại `policy_update_signal`, `updated_constraint_model` và `risk-aware prior`.
5. Nếu phát hiện vi phạm constraint hoặc uncertainty vượt ngưỡng, `Perception` thực hiện `event-triggered re-grounding` trước vòng kế tiếp.

Giao thức này là phần tối thiểu phải giữ nguyên trong mọi domain để CAMAS còn được xem là cùng một kiến trúc.

## 7. Tiềm năng ứng dụng và giá trị thực tiễn

### 7.1. Giá trị ứng dụng tổng quát

CAMAS có tiềm năng ứng dụng trong các hệ vận hành thông minh nơi quyết định phải đồng thời đúng với trạng thái thực tế, thích ứng với bối cảnh biến động và tuân thủ ràng buộc an toàn. Đây là nhóm bài toán xuất hiện nhiều trong công nghiệp 4.0, hạ tầng năng lượng, nhà máy linh hoạt, bảo trì dự báo và các hệ thống hỗ trợ quyết định kỹ thuật số. Giá trị thực tiễn của CAMAS không chỉ nằm ở tăng độ chính xác của tác nhân, mà nằm ở việc tạo ra một kiến trúc quyết định có thể kiểm chứng, có giải thích bằng bằng chứng và có cơ chế kiểm soát rủi ro.

Về góc nhìn triển khai, CAMAS phù hợp trước hết như một nền tảng `decision support` hoặc `human-in-the-loop intelligence`, sau đó mới tiến dần sang các dạng tự động hóa cao hơn trong môi trường đã được mô phỏng và kiểm chứng đầy đủ. Cách tiếp cận này giúp giảm rủi ro triển khai, đồng thời tạo điều kiện để tích lũy dữ liệu phản hồi người dùng và dữ liệu vi phạm ràng buộc cho các vòng cải tiến tiếp theo.

### 7.2. Ứng dụng trong bảo trì công nghiệp

Trong bảo trì công nghiệp, CAMAS có thể được dùng để hỗ trợ chẩn đoán nguyên nhân sự cố, giải thích trạng thái thiết bị, đối chiếu log vận hành với tri thức nền và đề xuất hành động xử lý có căn cứ. `Dual-memory knowledge graph` giúp liên kết giữa hiểu biết kỹ thuật về thiết bị với bằng chứng mới nhất từ log, trace và sensor stream. Nhờ đó, kỹ sư vận hành không chỉ nhận được câu trả lời, mà còn nhận được bằng chứng nào đang ủng hộ kết luận đó và mức độ bất định của kết luận.

Giá trị vận hành ở domain này nằm ở ba điểm: giảm nguy cơ chẩn đoán sai do hallucination, rút ngắn thời gian truy vết nguyên nhân sự cố, và tạo ra một lớp tri thức vận hành hợp nhất có thể tái sử dụng cho bảo trì dự báo, đào tạo kỹ sư mới và chuẩn hóa quy trình xử lý. Mô hình triển khai phù hợp nhất ở giai đoạn đầu là `decision support` hoặc `human-supervised maintenance assistant`.

### 7.3. Ứng dụng trong sản xuất linh hoạt và scheduling

Trong FJSP hoặc các bài toán điều phối sản xuất động, CAMAS có thể hoạt động như một bộ gợi ý điều độ thông minh cho môi trường có nhiều máy, nhiều công đoạn và nhiều nhiễu động như máy hỏng, đơn hàng gấp hoặc thay đổi deadline. `Hierarchical coordination` cho phép hệ thống tách chiến lược điều độ ở tầng cao khỏi quyết định gán việc cụ thể ở tầng thấp, trong khi graph-based encoding và LRMP giúp phản ánh đúng cấu trúc phụ thuộc đang thay đổi của dây chuyền.

Giá trị thực tiễn ở domain này nằm ở khả năng giảm makespan, giảm tardiness và duy trì hiệu suất điều độ ổn định khi môi trường thay đổi. Với doanh nghiệp sản xuất, điều này đồng nghĩa với giảm thời gian chờ, tăng sử dụng máy và cải thiện khả năng phản ứng với biến động đơn hàng. Mô hình triển khai phù hợp là `human-in-the-loop scheduling assistant`, sau đó có thể tiến tới `autonomous-with-constraints` trong các phân xưởng đã có digital twin hoặc simulator đủ tin cậy.

### 7.4. Ứng dụng trong smart grid và hệ năng lượng thông minh

Trong smart grid, CAMAS có thể được dùng như một kiến trúc hỗ trợ điều phối đa tác nhân cho dispatch, demand response hoặc tối ưu vận hành dưới điều kiện phụ tải thay đổi và nguồn tái tạo biến động. Ở đây, `constraint-aware alignment` đóng vai trò đặc biệt quan trọng vì mục tiêu tối ưu kinh tế phải luôn bị chặn bởi các ràng buộc cứng như giới hạn đường dây, cân bằng công suất và safety margin.

Giá trị thực tiễn nằm ở khả năng giảm xác suất vi phạm constraint, tăng độ ổn định vận hành và cải thiện trade-off giữa safety với profit hoặc efficiency. Domain này phù hợp với mô hình triển khai `simulation-first`, sau đó là `operator-in-the-loop`, trước khi xem xét bất kỳ mức tự động hóa cao hơn nào trong môi trường thực.

## 8. Khả năng triển khai công nghệ lõi

### 8.1. Dual-memory knowledge graph như lớp tri thức vận hành

`Dual-memory knowledge graph` có thể được triển khai như lớp hợp nhất giữa dữ liệu tri thức nền và dữ liệu observability. Ở tầng dữ liệu, hệ thống nhận đầu vào từ sensor, log, SCADA/MES/CMMS hoặc các nguồn vận hành tương đương. Ở tầng tri thức, semantic memory lưu các quan hệ kỹ thuật ổn định, còn observability memory lưu các sự kiện và trạng thái động có đóng dấu thời gian. Ở tầng ứng dụng, lớp này phục vụ grounding, truy vết bằng chứng, giải thích quyết định và phát hiện mâu thuẫn giữa tri thức nền với vận hành thực tế.

Trong triển khai thực, công nghệ này phù hợp nhất để làm `knowledge layer` cho các tác nhân hỗ trợ kỹ sư, hệ thống chẩn đoán hoặc dashboard vận hành thông minh. Nó cũng có thể được dùng như lớp trung gian để giảm khoảng cách giữa dữ liệu vận hành thô và các mô hình quyết định ở tầng trên.

### 8.2. Hierarchical coordination như lớp ra quyết định thích ứng

`Hierarchical multi-agent coordination` có thể được triển khai như một bộ máy ra quyết định hoặc gợi ý ra quyết định cho các bài toán phân bổ tài nguyên, dispatch hoặc scheduling nhiều thực thể. Ở tầng mô hình, graph encoder và LRMP tạo ra biểu diễn ngữ cảnh động; ở tầng quyết định, master policy chọn chiến lược hoặc subgoal, còn worker policies chọn hành động tác nghiệp cụ thể. Cách thiết kế này giúp hệ thống vừa giữ được tính tổng quát ở tầng chiến lược, vừa phản ứng nhanh với thay đổi ở tầng thực thi.

Trong ứng dụng thực tế, công nghệ này phù hợp để làm `decision engine` phía sau các giao diện hỗ trợ điều độ hoặc tối ưu vận hành. Nó cũng có thể hoạt động như một `policy recommender` thay vì tác nhân tự động hoàn toàn, đặc biệt trong các môi trường có rủi ro cao hoặc cần phê duyệt của con người.

### 8.3. Constraint-aware RLHF như lớp căn chỉnh an toàn

`Constraint-aware cooperative RLHF` phù hợp để triển khai như một lớp cập nhật policy có kiểm soát an toàn. Ở tầng học, utility head học từ preference hoặc tín hiệu đánh giá của chuyên gia; safety head học từ vi phạm hoặc thỏa mãn constraint. Ở tầng tối ưu, policy chỉ được cập nhật trong không gian hành vi thỏa điều kiện feasibility hoặc safety budget. Điều này giúp hệ thống tránh kiểu cải thiện utility bằng cách đánh đổi an toàn một cách không kiểm soát.

Về triển khai, công nghệ này phù hợp nhất trong giai đoạn đầu với `simulation-first training` và `human-supervised adaptation`. Trong các môi trường như smart grid hoặc vận hành công nghiệp có rủi ro vật lý, đây nên là lớp kiểm soát và căn chỉnh chứ không phải lớp cho phép tự động hóa không giới hạn.

### 8.4. CAMAS như kiến trúc điều hành thông minh nhiều lớp

Khi tích hợp đầy đủ, CAMAS có thể được nhìn như một `multi-layer intelligent operations architecture`. Ở tầng dữ liệu và tri thức, hệ thống xây grounded state từ observability và tri thức nền. Ở tầng ra quyết định, hệ thống chọn hành động hoặc khuyến nghị điều phối phù hợp với ngữ cảnh. Ở tầng an toàn và căn chỉnh, hệ thống cập nhật policy và điều chỉnh cách perception/coordination hoạt động ở vòng tiếp theo.

Mô hình triển khai hợp lý nhất là đi theo ba mức:

- `decision support`: hệ thống đưa khuyến nghị kèm bằng chứng và độ bất định
- `human-in-the-loop`: con người phê duyệt hoặc điều chỉnh các quyết định quan trọng
- `autonomous-with-constraints`: tự động hóa cao hơn nhưng chỉ trong vùng hành vi đã được kiểm chứng bằng mô phỏng, log lịch sử và safety constraints

Thiết kế triển khai theo các mức này giúp proposal vừa giữ được tham vọng khoa học, vừa tránh bị phản biện là thiếu thực tế trong bối cảnh ứng dụng công nghiệp.

## 9. Bản đồ công bố và tách biệt novelty

### 9.1. Bài báo 1: Perception

#### Hướng tiêu đề

Đồ thị tri thức bộ nhớ kép có neo observability cho tác nhân giảm ảo giác trong bảo trì công nghiệp

#### Đóng góp chính

- mô hình dual-memory gồm semantic memory và observability memory
- cơ chế temporal retrieval
- cơ chế conflict checking giữa hai lớp bộ nhớ
- grounded output với uncertainty score

#### Domain neo

- bảo trì công nghiệp

#### Thông điệp học thuật

Tác nhân không nên chỉ truy xuất tri thức đúng về mặt khái niệm; tác nhân cần tri thức đúng với trạng thái vận hành hiện tại.

### 9.2. Bài báo 2: Coordination

#### Hướng tiêu đề

Điều phối đa tác nhân phân cấp thích ứng theo ngữ cảnh cho bài toán FJSP động

#### Đóng góp chính

- hierarchical MARL
- graph-based context encoding
- MD-MDP
- LRMP cho biểu diễn thích ứng

#### Domain neo

- FJSP/Scheduling

#### Thông điệp học thuật

Điều phối hiệu quả trong môi trường động đòi hỏi vừa có cấu trúc phân cấp, vừa có biểu diễn ngữ cảnh động.

### 9.3. Bài báo 3: Alignment

#### Hướng tiêu đề

Cooperative RLHF có xét ràng buộc cho điều khiển đa tác nhân an toàn trong smart grid

#### Đóng góp chính

- utility head và safety head
- preference learning kết hợp feasibility learning
- policy optimization có xét hard constraints

#### Domain neo

- smart grid

#### Thông điệp học thuật

Alignment trong cyber-physical systems không thể dừng ở preference; alignment phải đi cùng feasibility và safety.

### 9.4. Bài báo 4: Integration

#### Hướng tiêu đề

CAMAS: kiến trúc đa tác nhân nhận thức vòng lặp khép kín cho các hệ kỹ thuật phức tạp

#### Đóng góp chính

- định nghĩa interface rõ giữa ba module
- định nghĩa feedback loop và cơ chế cập nhật
- so sánh closed-loop với open-loop và pairwise integration
- đánh giá cross-domain

#### Domain neo

- maintenance
- FJSP
- smart grid

#### Thông điệp học thuật

Giá trị của CAMAS không nằm ở việc ghép ba kỹ thuật mạnh, mà nằm ở việc đóng vòng đúng cách để tạo lợi ích hệ thống.

## 10. Thiết kế thực nghiệm

### 10.1. Nguyên tắc chung

Mỗi bài báo phải có:

- một domain neo chính
- tối thiểu 3 baseline mạnh
- tối thiểu 3 ablation có ý nghĩa
- ít nhất một robustness test

Bài tích hợp phải có thêm:

- so sánh open-loop và closed-loop
- so sánh pairwise integration
- phân tích overhead và trade-off giữa hiệu năng với chi phí tính toán

Ngoài ra, các metric headline phải được định nghĩa theo cách vận hành được trong từng domain, tránh dùng các tên gọi hấp dẫn nhưng mơ hồ. Trong proposal này, bốn nhóm metric lõi được hiểu như sau:

- `hallucination rate`: tỷ lệ phát biểu, chẩn đoán hoặc đề xuất hành động không được hỗ trợ bởi evidence set hoặc mâu thuẫn với observability memory tại thời điểm đánh giá
- `evidence grounding score`: mức độ mà đầu ra của tác nhân có thể truy vết về tập bằng chứng hợp lệ trong semantic memory và observability memory
- `safety violation rate`: tỷ lệ trajectory hoặc hành động vi phạm ít nhất một hard constraint của domain
- `closed-loop gain`: độ chênh hiệu năng giữa full CAMAS và cấu hình open-loop hoặc pairwise integration, đo trên cùng điều kiện khởi tạo và cùng budget tính toán

Việc định nghĩa rõ các metric này là bắt buộc để tránh phản biện rằng proposal đang sử dụng các khái niệm hấp dẫn nhưng không đo lường được nhất quán.

### 10.2. Thực nghiệm cho Bài 1

#### Dữ liệu

- MAKG
- maintenance logs
- alarm traces
- sensor/event history

Trong domain này, một phát biểu hoặc đề xuất được xem là hallucination nếu rơi vào một trong ba trường hợp: không có bằng chứng truy vết được từ evidence set, mâu thuẫn với observability memory ở thời điểm tương ứng, hoặc dẫn tới một kết luận về trạng thái thiết bị trái với execution history đã xác thực. Cách định nghĩa này giúp `hallucination rate` trở thành metric vận hành, không chỉ là khái niệm ngôn ngữ chung chung.

#### Baseline

- semantic-only KG
- single-memory graph
- RAG không observability
- dual-memory không conflict checking

#### Metric

- hallucination rate
- factual consistency
- task success
- evidence grounding score

#### Ablation

- bỏ observability memory
- bỏ temporal validity
- bỏ conflict checking
- bỏ uncertainty estimation

#### Stress test

- stale logs
- missing sensor values
- conflicting maintenance records

### 10.3. Thực nghiệm cho Bài 2

#### Dữ liệu

- Barnes FJSP
- dynamic FJSP instances nếu có

#### Baseline

- heuristic dispatch rules
- PPO/DQN
- flat MARL
- hierarchical MARL không graph
- graph RL không LRMP

#### Metric

- makespan
- tardiness
- machine utilization
- robustness under perturbation
- convergence stability

#### Ablation

- bỏ hierarchy
- bỏ graph encoder
- bỏ MD-MDP
- bỏ LRMP
- bỏ temporal modeling

#### Stress test

- machine breakdown
- urgent order insertion
- processing delay

### 10.4. Thực nghiệm cho Bài 3

#### Dữ liệu

- IEEE 30 bus
- IEEE 118 bus
- IEEE 300 bus
- dữ liệu EVN nếu đủ điều kiện

Preference labels trong Paper 3 được xây theo chiến lược hai tầng để bảo đảm tính khả thi. Tầng thứ nhất là `simulated expert preference`, sinh từ tập luật chuyên gia, tiêu chí vận hành và xếp hạng trajectory theo utility-safety trade-off trong môi trường mô phỏng. Tầng thứ hai là `human validation subset`, trong đó một tập con trajectory được chuyên gia hoặc người vận hành đánh giá để kiểm tra độ phù hợp giữa preference mô phỏng và judgment của con người. Cách tổ chức này cho phép dùng RLHF trong bối cảnh cyber-physical mà không đòi hỏi một bộ dữ liệu human preference quá lớn ngay từ đầu.

#### Baseline

- RLHF chuẩn
- constrained RL
- safe RL
- CoRLHF không safety head

#### Metric

- safety violation rate
- constraint satisfaction rate
- profit/return
- robustness under disturbances

Trong domain smart grid, `safety violation` được xác định trực tiếp từ các điều kiện như quá tải đường dây, vi phạm cân bằng công suất, vượt giới hạn vận hành hoặc không thỏa safety margin. Nhờ vậy, safety head và utility head có thể được huấn luyện trên hai tín hiệu tách biệt nhưng nhất quán.

#### Ablation

- bỏ safety head
- bỏ cooperative optimization
- bỏ hard-constraint module
- chỉ dùng preference feedback

#### Stress test

- demand spike
- renewable fluctuation
- line congestion
- noisy preference annotations

### 10.5. Thực nghiệm cho Bài 4

#### Domain

- maintenance để đo grounding
- FJSP để đo coordination adaptation
- smart grid để đo safety-profit tradeoff

#### Baseline

- perception only
- perception + coordination
- coordination + alignment
- full CAMAS không feedback loop
- open-loop pipeline

#### Metric

- end-to-end task performance
- safety
- efficiency/profit
- robustness
- latency/compute overhead
- cross-domain generalization

Trong bài tích hợp, `cross-domain generalization` không phải headline claim chính mà chỉ là bằng chứng phụ cho tính bền vững của kiến trúc. Claim chính của bài này là `closed-loop gain` so với open-loop và pairwise integration về chất lượng quyết định có xét an toàn trong môi trường động.

#### Ablation

- tắt alignment-to-perception feedback
- tắt uncertainty propagation
- tắt conflict-aware re-grounding
- thay feedback theo event bằng feedback theo chu kỳ cố định

## 11. Lộ trình nghiên cứu và kế hoạch triển khai luận án

### 11.1. Bảng tóm tắt lộ trình luận án

| Giai đoạn | Trọng tâm nghiên cứu | Phương pháp chính | Dữ liệu/domain neo | Tiêu chí hoàn thành chính | Đầu ra |
|---|---|---|---|---|---|
| Giai đoạn 1 | Grounded Perception | Dual-memory KG, temporal retrieval, conflict checking | MAKG, maintenance logs | Định nghĩa được grounded state; hallucination rate có nghĩa vận hành; vượt baseline semantic-only/retrieval-only | Chương perception + bản thảo bài 1 |
| Giai đoạn 2 | Adaptive Coordination | Hierarchical MARL, graph encoder, MD-MDP, LRMP | Barnes FJSP, dynamic FJSP | Cải thiện makespan, tardiness, robustness; ablation tách vai trò hierarchy/graph/LRMP | Chương coordination + bản thảo bài 2 |
| Giai đoạn 3 | Safe Alignment | Dual-head reward model, simulated preference, Lagrangian constrained optimization | IEEE 30/118/300, EVN nếu phù hợp | Giảm safety violation; utility không sụp đổ; reward model học ổn định | Chương alignment + bản thảo bài 3 |
| Giai đoạn 4 | Closed-Loop CAMAS | Interface standardization, feedback protocol, full-system integration | Maintenance, FJSP, smart grid | Chứng minh closed-loop gain; kiểm chứng feedback semantics; tích hợp thành luận điểm thống nhất | Chương tích hợp + bản thảo bài 4 |

### 11.2. Nguyên tắc triển khai lộ trình

Lộ trình nghiên cứu của luận án tuân theo hai nguyên tắc. Thứ nhất, mỗi giai đoạn chỉ được chuyển sang giai đoạn kế tiếp khi đã đạt tiêu chí kiểm chứng tối thiểu ở giai đoạn hiện tại. Thứ hai, mọi kết quả trung gian đều phải phục vụ trực tiếp cho luận điểm tổng thể của luận án, không phát triển các nhánh nghiên cứu tách rời khỏi kiến trúc CAMAS. Nhờ đó, tiến độ nghiên cứu được kiểm soát tốt hơn và luận án giữ được sự thống nhất từ đầu đến cuối.

### Giai đoạn 1: Xây dựng Perception

Mục tiêu:

- hoàn thiện dual-memory knowledge graph
- định nghĩa grounded state và evidence set
- kiểm chứng khả năng giảm hallucination

Phương pháp thực hiện:

- xây semantic memory từ tri thức miền và cấu trúc hệ thống
- xây observability memory từ log, trace, sensor/event history
- thiết kế cơ chế temporal retrieval và conflict checking
- xây bộ quy tắc hoặc quy trình gán nhãn để xác định hallucination theo ngữ cảnh vận hành

Tiêu chí hoàn thành giai đoạn:

- grounded state được định nghĩa và kiểm chứng được
- metric hallucination rate có định nghĩa vận hành rõ
- mô hình perception chứng minh được cải thiện so với semantic-only hoặc retrieval-only baseline

Đầu ra khoa học và luận án:

- một chương/một cụm nội dung của luận án về grounded perception
- một bản thảo bài báo về grounded perception
- bộ pipeline dựng semantic memory và observability memory

### Giai đoạn 2: Xây dựng Coordination

Mục tiêu:

- xây framework điều phối phân cấp
- tích hợp graph encoder, MD-MDP và LRMP
- đánh giá trên FJSP động

Phương pháp thực hiện:

- mô hình hóa trạng thái FJSP động dưới dạng heterogeneous/temporal graph
- thiết kế master policy và worker policies cho cấu trúc phân cấp
- tích hợp MD-MDP để mô hình hóa reward và action đa chiều
- đưa LRMP vào tầng biểu diễn để tạo context-adaptive coordination

Tiêu chí hoàn thành giai đoạn:

- coordination sử dụng được grounded state như đầu vào có ý nghĩa
- các metric makespan, tardiness và robustness được cải thiện so với flat MARL và graph-free baselines
- vai trò của hierarchy, graph encoding và LRMP được tách bạch bằng ablation

Đầu ra khoa học và luận án:

- một chương/một cụm nội dung của luận án về adaptive coordination
- một bản thảo bài báo về adaptive coordination
- mô hình điều phối đủ độc lập để kiểm chứng riêng trước khi tích hợp

### Giai đoạn 3: Xây dựng Alignment

Mục tiêu:

- thiết kế reward model hai đầu
- xây cơ chế policy optimization có xét ràng buộc
- kiểm chứng trade-off giữa utility và safety

Phương pháp thực hiện:

- xây reward model hai đầu gồm utility head và safety head
- thiết kế chiến lược sinh preference labels hai tầng: simulated expert preference và human validation subset
- tối ưu policy bằng Lagrangian constrained policy optimization
- đánh giá trade-off giữa utility, safety và robustness dưới các nhiễu động hệ thống

Tiêu chí hoàn thành giai đoạn:

- preference labels và safety labels đủ nhất quán để huấn luyện reward model
- safety violation rate giảm rõ so với RLHF chuẩn và constrained RL baseline
- utility không sụp đổ khi tăng cường mức kiểm soát an toàn

Đầu ra khoa học và luận án:

- một chương/một cụm nội dung của luận án về safe alignment
- một bản thảo bài báo về safe alignment
- pipeline xây preference label, safety label và policy update under constraints

### Giai đoạn 4: Tích hợp CAMAS

Mục tiêu:

- chuẩn hóa interface giữa ba module
- xây feedback protocol
- chứng minh lợi ích closed-loop

Phương pháp thực hiện:

- chuẩn hóa interface giữa ba module theo grounded state, context embedding, constraint model và policy update signal
- định nghĩa giao thức closed-loop tối thiểu dùng chung cho các domain
- so sánh full CAMAS với open-loop và pairwise integration dưới cùng budget tính toán
- phân tích closed-loop gain, overhead và tính ổn định ở mức hệ thống

Tiêu chí hoàn thành giai đoạn:

- feedback semantics được kiểm chứng bằng thực nghiệm, không chỉ mô tả khái niệm
- full CAMAS cho closed-loop gain dương so với open-loop hoặc cấu hình tích hợp thiếu module
- kiến trúc tổng thể tạo ra một luận điểm thống nhất cho toàn bộ luận án

Đầu ra khoa học và luận án:

- chương tích hợp trung tâm của luận án tiến sĩ
- một bản thảo bài báo tổng hợp về CAMAS
- kết quả đối sánh open-loop, pairwise và full closed-loop

### Tính liên kết của toàn bộ luận án

Luận án này không phải tập hợp cơ học của bốn bài toán rời rạc. Logic tích lũy của luận án được xác định như sau:

- Giai đoạn 1 tạo `grounded state`, là điều kiện cần để hệ thống tránh quyết định trên trạng thái sai
- Giai đoạn 2 tạo `context-adaptive action generation`, là điều kiện cần để ra quyết định hiệu quả trong môi trường động
- Giai đoạn 3 tạo `safe policy update`, là điều kiện cần để quyết định tối ưu không vi phạm ràng buộc cứng
- Giai đoạn 4 chứng minh rằng ba điều kiện cần trên khi được đóng vòng sẽ trở thành một đóng góp kiến trúc hoàn chỉnh

Theo logic này, từng giai đoạn vừa là một kết quả học thuật độc lập, vừa là một bước bắt buộc trong cấu trúc chung của luận án tiến sĩ. Điều này giúp luận án giữ được hai yêu cầu cùng lúc: có chiều sâu ở từng lớp phương pháp và có một luận điểm trung tâm thống nhất ở cấp độ toàn bộ nghiên cứu.

## 12. Đóng góp khoa học kỳ vọng

Nếu thực hiện thành công, đề xuất này kỳ vọng tạo ra bốn lớp đóng góp:

### Đóng góp 1: Grounded perception

Chỉ ra rằng observability memory là một thành phần bắt buộc nếu muốn giảm hallucination của tác nhân trong môi trường vận hành thực.

### Đóng góp 2: Adaptive coordination

Chỉ ra rằng điều phối đa tác nhân hiệu quả trong môi trường scheduling động đòi hỏi cả cấu trúc phân cấp lẫn biểu diễn ngữ cảnh thay đổi theo trạng thái.

### Đóng góp 3: Safe alignment

Chỉ ra rằng alignment trong hệ kỹ thuật phức tạp phải tách utility và safety thay vì gộp vào một reward scalar đơn giản.

### Đóng góp 4: Architectural loop closure

Chỉ ra rằng vòng phản hồi giữa perception, coordination và alignment tạo ra lợi ích ở cấp độ hệ thống, từ đó cung cấp một cách nhìn mới về thiết kế tác nhân công nghiệp.

## 13. Giá trị học thuật và khả năng công bố

Đề xuất này phù hợp với nhóm tạp chí AI/Expert Systems như:

- Knowledge-Based Systems
- Expert Systems with Applications
- Information Sciences

Lý do là vì đề xuất vừa mang đóng góp phương pháp, vừa có đánh giá thực nghiệm trên nhiều domain, lại có khả năng kể câu chuyện rõ ràng từ module-level innovation đến architecture-level innovation.

Tuy nhiên, để tăng xác suất công bố, proposal cần tránh ba lỗi thường gặp:

- claim quá rộng ngay từ đầu
- để novelty giữa các bài chồng lên nhau
- viết các con số kỳ vọng như kết quả gần như chắc chắn

Do đó, trong bản đề xuất này, các giá trị như giảm hallucination, tăng safety hay tăng profit phải được diễn đạt là `target hypotheses`, không phải kết quả bảo đảm.

## 14. Rủi ro nghiên cứu và phương án giảm thiểu

### Rủi ro 1: Scope quá rộng

Ba domain và bốn bài báo là một kế hoạch tham vọng. Để giảm rủi ro, mỗi bài module chỉ neo vào một domain chính; phạm vi ba domain được giữ đầy đủ chủ yếu ở bài tích hợp.

### Rủi ro 2: Reviewer cho rằng đề xuất chỉ là ghép kỹ thuật có sẵn

Để phản biện điểm này, proposal phải nhấn mạnh:

- mỗi module có adaptation mới phù hợp với bài toán
- các interface giữa module là đóng góp thiết kế, không phải chi tiết kỹ thuật vụn
- closed-loop semantics là phần đóng góp kiến trúc mới

### Rủi ro 3: Metric chưa đủ thuyết phục

Proposal cần dùng metric đã được cộng đồng công nhận. Những metric tự định nghĩa như HHS chỉ nên giữ khi có mô tả toán học, trực giác rõ và thí nghiệm chứng minh tính hữu ích.

### Rủi ro 4: Dữ liệu thực không đủ sạch

Các domain như EVN hoặc maintenance logs có thể gặp vấn đề về chất lượng hoặc tính công bố. Phương án giảm thiểu là:

- dùng benchmark chuẩn làm xương sống thực nghiệm
- dùng dữ liệu thực như phần tăng giá trị ứng dụng nếu đủ điều kiện

## 15. Kết luận

CAMAS được đề xuất như một lộ trình nghiên cứu có cấu trúc, không phải một mô hình đơn lẻ. Điểm mạnh của đề xuất là biến ba vấn đề lớn của tác nhân AI trong hệ kỹ thuật phức tạp thành bốn đơn vị công bố có liên kết logic: grounded perception, adaptive coordination, safe alignment và closed-loop integration. Cách tổ chức này giúp proposal vừa tường minh hơn về mặt học thuật, vừa khả thi hơn về mặt công bố.

Nếu được triển khai đúng, CAMAS không chỉ đóng góp một số cải tiến thuật toán rời rạc, mà còn có thể đưa ra một khung thiết kế mới cho các tác nhân công nghiệp: tác nhân phải được grounding bởi observability, phải điều phối dựa trên biểu diễn ngữ cảnh động, phải được alignment dưới hard constraints, và quan trọng nhất là phải vận hành trong một vòng phản hồi khép kín có khả năng tự cải thiện qua thời gian.
