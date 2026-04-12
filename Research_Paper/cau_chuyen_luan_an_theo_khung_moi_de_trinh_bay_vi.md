# Câu Chuyện Luận Án Theo Khung Mới

## 1. Mục tiêu của tài liệu này

Tài liệu này không viết theo kiểu proposal học thuật khô cứng.  
Nó được viết theo kiểu `câu chuyện nghiên cứu`, để bạn có thể:

- tự hiểu luận án một cách tự nhiên
- trình bày với giáo viên hướng dẫn dễ hơn
- giải thích cho hội đồng hoặc người ngoài ngành AI vẫn nắm được
- kể được vì sao 4 paper đi với nhau thành một luận án

Nếu phải nói ngắn gọn, luận án này kể một câu chuyện rất đơn giản:

`Một hệ AI muốn được tin để ra quyết định trong môi trường vận hành phức tạp thì trước hết phải biết trạng thái thật của hệ là gì, sau đó phải biết khi nào nên hành động hay chưa nên hành động, tiếp theo phải biết khi nào cần phối hợp lại toàn hệ, và cuối cùng phải biết khi nào mức tự động hóa đang vượt quá mức rủi ro chấp nhận được.`

Đó chính là logic của 4 paper.

## 2. Hãy bắt đầu từ một hình ảnh rất đời thường

Hãy tưởng tượng bạn là người phụ trách vận hành của một nhà máy thông minh.

Bạn có:

- nhiều máy móc
- nhiều đơn hàng
- nhiều cảm biến
- nhiều cảnh báo
- nhiều lịch bảo trì
- nhiều ràng buộc an toàn

Mỗi ngày, hệ thống phải quyết định rất nhiều thứ:

- máy nào đang có dấu hiệu hỏng thật, máy nào chỉ báo động giả?
- nên tiếp tục chạy máy hay dừng để kiểm tra?
- nếu một máy có nguy cơ lỗi, có nên đổi lịch sản xuất không?
- nếu vừa muốn giữ tiến độ đơn hàng vừa phải đảm bảo an toàn, nên ưu tiên điều gì?
- khi nào hệ nên tự động quyết, và khi nào nên gọi con người vào?

Bây giờ hãy nhìn vấn đề sâu hơn.

Phần lớn các hệ AI hiện nay thường chỉ giỏi một phần:

- có hệ giỏi dự đoán lỗi
- có hệ giỏi điều độ
- có hệ giỏi tối ưu policy
- có hệ giỏi cảnh báo rủi ro

Nhưng khi ghép lại, chúng chưa chắc tạo thành một hệ thống đáng tin.

Tại sao?

Vì chúng thường thiếu 4 khả năng rất quan trọng:

1. `không biết trạng thái thật của hệ rõ đến đâu`
2. `không biết khi nào chưa nên ra quyết định`
3. `không biết khi nào cần phối hợp lại toàn hệ`
4. `không biết tổng mức rủi ro của tự động hóa đang tăng đến đâu`

Luận án này ra đời để giải quyết đúng 4 câu hỏi đó.

## 3. Một câu mô tả toàn bộ luận án

Nếu phải giới thiệu luận án này chỉ bằng một câu, bạn có thể nói:

`Luận án nghiên cứu cách xây dựng một hệ AI có thể ra quyết định đáng tin cậy trong môi trường vận hành phức tạp, bằng cách đi từ hiểu trạng thái thật của hệ, đến ra quyết định dưới bất định, đến phối hợp lại khi có biến động, và cuối cùng là quản trị mức tự động hóa bằng ngân sách rủi ro.`

## 4. Vì sao đây là một luận án PhD, chứ không chỉ là 4 bài ghép lại

Một luận án PhD tốt không phải là 4 bài báo đứng cạnh nhau.  
Một luận án PhD tốt là 4 câu trả lời cho 4 phần của cùng một câu hỏi lớn.

Ở đây, câu hỏi lớn là:

`AI nên hành động như thế nào trong một hệ vận hành phức tạp khi nó không quan sát được toàn bộ thế giới, môi trường thay đổi liên tục, và nó vẫn phải an toàn?`

Từ câu hỏi lớn đó, 4 paper xuất hiện rất tự nhiên:

- `Paper 1`: nếu không biết trạng thái thật của hệ, thì không thể quyết đúng
- `Paper 2`: nếu trạng thái còn chưa chắc, thì phải biết khi nào nên quyết, khi nào chưa
- `Paper 3`: nếu môi trường đổi và nhiều quyết định liên quan nhau, thì phải biết khi nào cần phối hợp lại
- `Paper 4`: nếu hệ ngày càng tự động, thì phải quản lý tổng mức rủi ro của quyền tự động đó

Bạn có thể hình dung luận án như một người lái xe thông minh:

1. trước tiên phải nhìn đúng tình huống trên đường
2. nếu nhìn chưa chắc thì không được bẻ lái bừa
3. nếu có chướng ngại vật mới xuất hiện thì phải phối hợp lại toàn bộ hành vi
4. nếu rủi ro quá cao thì phải giảm quyền tự động, chậm lại hoặc nhường cho người lái

Đó là toàn bộ câu chuyện.

## 5. Câu chuyện của Paper 1: “Hệ có thật sự biết trạng thái của thế giới không?”

### 5.1. Ví dụ trực quan

Hãy tưởng tượng một máy trong nhà máy phát cảnh báo nhiệt độ cao.

Một hệ AI đơn giản có thể nhìn thấy cảnh báo đó và nói:

- “Máy đang quá nhiệt, cần dừng ngay.”

Nghe có vẻ hợp lý.

Nhưng thực tế có thể là:

- cảm biến đang bị lỗi
- cảnh báo này đã xuất hiện từ ca trước, giờ đã xử lý rồi
- một cảm biến khác lại cho thấy hệ đang ổn định
- log vận hành cho thấy máy vừa được kiểm tra và đang chạy bình thường

Vậy câu hỏi là:

`AI có thật sự biết trạng thái vận hành hiện tại của máy không, hay chỉ đang phản ứng với một vài tín hiệu rời rạc?`

### 5.2. Vấn đề cốt lõi

Rất nhiều hệ AI hiện nay ra quyết định từ dữ liệu quan sát nhưng không trả lời được:

- dữ liệu này có đầy đủ không?
- có bị nhiễu không?
- có bị trễ không?
- có nguồn nào đang mâu thuẫn nhau không?

Cho nên chúng dễ “tưởng là biết”, nhưng thực ra chỉ đang đoán.

### 5.3. Paper 1 muốn làm gì

Paper 1 không chỉ muốn dự đoán nhãn như:

- bình thường
- bất thường
- lỗi

Mà muốn đi xa hơn:

- ước lượng một `belief state`, tức là trạng thái vận hành mà hệ tin là đúng nhất hiện tại
- đồng thời cho biết `mức độ chắc chắn`
- và chỉ ra `bằng chứng nào ủng hộ`, `bằng chứng nào mâu thuẫn`

### 5.4. Cách giải thích dễ hiểu

Paper 1 giống như biến AI từ một người “trả lời rất nhanh” thành một người “biết tự kiểm tra xem mình có chắc hay không”.

### 5.5. Câu chốt của Paper 1

`Trước khi để AI quyết định, ta phải buộc nó xây dựng một trạng thái vận hành đáng tin cậy, thay vì chỉ phản ứng với vài tín hiệu bề mặt.`

## 6. Câu chuyện của Paper 2: “Khi chưa chắc, có nên hành động ngay không?”

### 6.1. Ví dụ trực quan

Giả sử hệ thống vừa phát hiện một tín hiệu bất thường ở một máy.

Có 5 cách phản ứng:

1. dừng máy ngay
2. tiếp tục chạy
3. chờ thêm 1 phút để quan sát thêm
4. yêu cầu cảm biến khác kiểm tra lại
5. gửi cảnh báo cho kỹ sư con người

Rõ ràng, không phải lúc nào “quyết ngay” cũng là tốt nhất.

Nếu dừng máy quá sớm:

- mất năng suất
- gián đoạn sản xuất

Nếu không dừng khi đáng lẽ phải dừng:

- có thể gây hỏng nặng hơn
- tăng rủi ro an toàn

Vậy câu hỏi thật ở đây là:

`Khi AI chưa chắc về trạng thái hiện tại, nó nên hành động, trì hoãn, quan sát thêm hay gọi con người?`

### 6.2. Vấn đề cốt lõi

Hầu hết hệ AI hiện nay được thiết kế như thể:

- lúc nào cũng phải đưa ra một action

Nhưng trong thực tế, một hệ đáng tin thường phải có thêm năng lực:

- biết “chưa đủ chắc để quyết”

Đây là điểm rất quan trọng nhưng thường bị bỏ qua.

### 6.3. Paper 2 muốn làm gì

Paper 2 mở rộng không gian hành động.  
AI không chỉ chọn:

- action A
- action B

Mà còn có thể chọn:

- `defer`: tạm hoãn quyết định
- `observe more`: thu thêm quan sát
- `escalate`: gọi con người
- `fallback`: chuyển sang chế độ bảo thủ

### 6.4. Cách giải thích dễ hiểu

Nếu Paper 1 dạy AI biết “mình đang thấy gì”, thì Paper 2 dạy AI biết:

- “khi nào mình chưa đủ chắc để làm ngay”

Đây là một bước tiến rất quan trọng về độ tin cậy.

### 6.5. Câu chốt của Paper 2

`Một hệ AI đáng tin không chỉ biết hành động đúng, mà còn phải biết khi nào chưa nên hành động.`

## 7. Câu chuyện của Paper 3: “Khi có biến động, toàn hệ nên phối hợp lại ra sao?”

### 7.1. Ví dụ trực quan

Hãy tưởng tượng trong nhà máy:

- một máy có nguy cơ hỏng trong 2 giờ tới
- nhưng hiện đang giữ một công đoạn quan trọng
- nếu dừng máy để bảo trì ngay thì đơn hàng trễ
- nếu không dừng thì có thể hỏng nặng giữa ca

Lúc này không còn là bài toán của một máy nữa.

Toàn hệ phải trả lời:

- có nên đổi lịch sản xuất?
- có nên chuyển việc sang máy khác?
- có nên bảo trì sớm?
- có nên chấp nhận chậm một phần đơn hàng để tránh rủi ro lớn?

### 7.2. Vấn đề cốt lõi

Trong thực tế, bảo trì, điều độ và phân bổ tài nguyên không tách rời nhau.  
Nhưng nhiều hệ AI vẫn xử lý chúng như các bài toán riêng.

Hệ quả là:

- từng phần có vẻ hợp lý
- nhưng toàn hệ lại tối ưu kém

### 7.3. Paper 3 muốn làm gì

Paper 3 nghiên cứu `joint coordination`.

Ý tưởng là:

- không phải lúc nào cũng cần tái phối hợp toàn hệ
- chỉ khi có một sự kiện đủ quan trọng thì mới kích hoạt tái phối hợp

Ví dụ các trigger:

- risk spike
- uncertainty spike
- throughput giảm mạnh
- dự báo cửa sổ hỏng hóc sắp tới

### 7.4. Cách giải thích dễ hiểu

Paper 3 giống như một người điều phối trung tâm biết rằng:

- không thể cứ 5 phút lại đảo hết kế hoạch
- nhưng khi có tín hiệu đủ nghiêm trọng thì phải lập tức phối hợp lại bảo trì, lịch sản xuất và tài nguyên

### 7.5. Câu chốt của Paper 3

`Một hệ vận hành đáng tin không chỉ ra quyết định cục bộ tốt, mà còn phải biết khi nào cần tái phối hợp toàn hệ do biến động mới xuất hiện.`

## 8. Câu chuyện của Paper 4: “Khi nào nên tin AI tiếp tục tự động, và khi nào phải giảm quyền tự động?”

### 8.1. Ví dụ trực quan

Hãy tưởng tượng một hệ AI trong nhà máy đang hoạt động khá tốt trong nhiều giờ.

Nhưng dần dần:

- dữ liệu cảm biến trở nên nhiễu hơn
- nhiều cảnh báo mâu thuẫn nhau hơn
- lịch sản xuất căng hơn
- nguy cơ vi phạm an toàn tăng dần

Nếu nhìn từng quyết định riêng lẻ, có thể chưa có cái nào quá nguy hiểm.  
Nhưng nếu nhìn cả quá trình, tổng mức rủi ro đang tăng lên.

Lúc này câu hỏi không còn là:

- quyết định tiếp theo có hợp lý không?

Mà là:

- hệ có nên tiếp tục được trao quyền tự động ở mức hiện tại không?

### 8.2. Vấn đề cốt lõi

Rất nhiều hệ AI chỉ kiểm tra safety ở từng bước riêng lẻ.  
Nhưng trong thực tế, điều quan trọng hơn là:

- rủi ro tích lũy theo thời gian
- mức căng thẳng tích tụ trong hệ
- mức độ mà AI còn xứng đáng được “tin để tự động”

### 8.3. Paper 4 muốn làm gì

Paper 4 đưa vào khái niệm `risk budget`.

Bạn có thể hiểu đơn giản như sau:

- hệ có một “ngân sách rủi ro”
- mỗi quyết định dưới bất định sẽ tiêu hao một phần ngân sách này
- khi ngân sách còn thấp, AI phải bớt tự động lại

Ví dụ:

- tăng quan sát
- chuyển sang chế độ bảo thủ
- giảm quyền tự động
- yêu cầu can thiệp của con người

### 8.4. Cách giải thích dễ hiểu

Giống như lái xe đường dài:

- lúc đường trống, thời tiết tốt, tài xế khỏe, có thể lái nhanh và tự tin
- khi trời tối, mưa lớn, buồn ngủ, đường xấu, rủi ro tích tụ
- lúc đó, quyết định đúng không phải là “cứ lái tiếp như cũ”
- mà là phải giảm tốc, nghỉ, hoặc đổi người lái

Paper 4 chính là tư duy đó, nhưng cho AI.

### 8.5. Câu chốt của Paper 4

`Một hệ AI đáng tin không chỉ cần quyết định tốt, mà còn phải biết khi nào mức tự động hóa của chính nó cần bị giới hạn bởi ngân sách rủi ro.`

## 9. Tóm tắt rất ngắn logic 4 paper

Bạn có thể trình bày 4 paper bằng một chuỗi rất dễ nhớ:

### Paper 1

`Biết thế giới đang ở trạng thái nào`

### Paper 2

`Biết khi nào nên quyết, khi nào chưa nên quyết`

### Paper 3

`Biết khi nào phải phối hợp lại cả hệ`

### Paper 4

`Biết khi nào phải giảm quyền tự động của chính mình`

Đây là cách trình bày rất dễ hiểu và rất logic.

## 10. Vì sao luận án này không chỉ áp dụng cho nhà máy

Đây là câu hỏi rất hay khi trình bày.

Bạn có thể trả lời theo cách rất dễ hiểu:

`Luận án được kiểm chứng sâu trong bối cảnh vận hành công nghiệp, nhưng các cơ chế cốt lõi của nó không chỉ thuộc về nhà máy. Chúng thuộc về một lớp bài toán rộng hơn: ra quyết định đáng tin cậy trong môi trường quan sát không đầy đủ, biến động động và có ràng buộc an toàn.`

## 10.1. Ví dụ sang logistics

Trong logistics:

- trạng thái xe, hàng và tuyến đường có thể không được quan sát đầy đủ
- hệ không phải lúc nào cũng nên dispatch ngay
- khi có tắc đường, trễ hàng, hỏng xe, phải phối hợp lại
- khi rủi ro giao hàng trễ tăng cao, mức tự động hóa cần giảm

Tức là cùng một logic.

## 10.2. Ví dụ sang cloud / data center operations

Trong cloud operations:

- metrics và logs có thể mâu thuẫn
- hệ không phải lúc nào cũng nên scale hoặc migrate ngay
- khi có workload spike hay node failure, phải phối hợp lại
- khi nguy cơ SLO violation tăng cao, phải siết quyền tự động hoặc gọi operator

Cũng là cùng một logic.

## 10.3. Ví dụ sang robotics

Trong robotics:

- robot không quan sát đủ môi trường
- nếu chưa chắc thì không nên hành động ngay
- khi xuất hiện chướng ngại hoặc robot khác gặp sự cố, phải phối hợp lại
- khi tổng rủi ro va chạm tăng cao, phải giảm mức tự động

Lại vẫn là cùng một logic.

## 10.4. Cách nói đúng khi trình bày

Bạn không nên nói:

- “Luận án này áp dụng ngay cho mọi domain.”

Bạn nên nói:

- “Luận án này được kiểm chứng sâu trong industrial operations, nhưng được thiết kế ở mức mechanism đủ tổng quát để có thể mở rộng sang các domain vận hành khác như logistics, cloud operations hoặc robotics, nếu được đặc tả lại phù hợp với state, trigger và risk model của từng miền.”

Cách nói này vừa mạnh, vừa không overclaim.

## 11. Cách trình bày rất ngắn trước hội đồng

Nếu bạn chỉ có 2 đến 3 phút, bạn có thể kể như sau:

`Luận án của tôi nghiên cứu cách để AI ra quyết định đáng tin cậy trong các hệ vận hành phức tạp. Tôi đi từ một vấn đề rất cơ bản: AI thường hành động khi nó chưa thực sự biết trạng thái của hệ rõ đến đâu. Vì vậy, paper đầu tiên của tôi tập trung vào việc ước lượng trạng thái vận hành đáng tin cậy dưới dữ liệu thiếu, nhiễu và mâu thuẫn. Khi đã có trạng thái, vấn đề tiếp theo là khi chưa chắc thì có nên hành động ngay hay không. Paper thứ hai nghiên cứu action gating, decision deferral và escalation. Nhưng trong hệ vận hành thực, các quyết định không tồn tại riêng lẻ. Một biến động ở thiết bị có thể kéo theo đổi lịch sản xuất và tái phân bổ tài nguyên. Paper thứ ba nghiên cứu event-triggered joint coordination. Cuối cùng, khi hệ ngày càng tự động, câu hỏi quan trọng là mức tự động hóa có còn nằm trong giới hạn rủi ro chấp nhận được không. Paper thứ tư nghiên cứu cơ chế risk budget để quản trị closed-loop autonomy. Bốn paper này tạo thành một chuỗi logic hoàn chỉnh cho reliable AI in complex operational systems.` 

## 12. Cách trình bày dài hơn trước giáo sư hướng dẫn

Nếu bạn có 5 đến 10 phút, bạn có thể kể theo nhịp:

1. nêu nỗi đau thực tế
2. nêu lỗi của các hệ hiện tại
3. đi qua 4 paper như 4 lớp giải quyết
4. kết thúc bằng ý tưởng transfer sang domain khác

Một cách kể dễ hiểu:

`Tôi xem AI vận hành giống như một người điều hành thông minh. Trước hết người đó phải hiểu trạng thái thật của hệ. Nếu chưa hiểu đủ, người đó không được phép quyết bừa. Nếu môi trường thay đổi, người đó phải biết lúc nào cần phối hợp lại toàn bộ hệ. Và nếu rủi ro tích lũy quá cao, người đó phải giảm quyền tự quyết của chính mình. Luận án của tôi chính là formalize bốn năng lực đó cho AI trong các hệ vận hành phức tạp.`

## 13. Điều quan trọng nhất khi bạn tự giải thích luận án

Đừng mở đầu bằng:

- graph
- RL
- memory
- MARL
- optimization
- safety

Hãy mở đầu bằng:

- một hệ AI trong vận hành thực có thể sai ở đâu
- tại sao sai
- và tại sao phải giải theo 4 lớp

Khi người nghe đã hiểu câu chuyện, lúc đó mới nói đến kỹ thuật.

## 14. Kết luận

Toàn bộ luận án này có thể được hiểu như một câu chuyện rất dễ nhớ:

`Muốn để AI được tin trong môi trường vận hành phức tạp, ta phải dạy nó bốn điều: hiểu trạng thái thật của hệ, biết khi nào chưa nên hành động, biết khi nào cần phối hợp lại, và biết khi nào phải tự giảm quyền tự động vì rủi ro đang tăng.`

Nếu bạn kể được đúng câu chuyện này, thì:

- người nghe sẽ dễ hiểu
- giáo sư sẽ dễ thấy logic
- hội đồng sẽ dễ thấy đây là một luận án thống nhất
- và bạn cũng sẽ dễ giữ được hướng nghiên cứu của mình mà không bị lạc vào các chi tiết kỹ thuật rời rạc

Nói ngắn gọn nhất:

- `Paper 1`: hiểu trạng thái
- `Paper 2`: quyết hay chưa quyết
- `Paper 3`: khi nào phải phối hợp lại
- `Paper 4`: khi nào phải giảm quyền tự động

Đó là một câu chuyện đủ rõ, đủ mạch lạc và đủ mạnh để trình bày.
