---
layout: post
title: "Model Drift"
author: "codedaoneu"
tags: machine learning
---


Model Drift là hiện tượng khả năng dự đoán của model gốc suy giảm theo thời gian do có sự thay đổi về các yếu tố tác động dẫn đến các yếu tố trong model không dự đoán đúng được các thay đổi mới trong điều kiện dữ liệu thực tế. Bản thân model không thay đổi, tuy nhiên các yếu tố xung quanh model thay đổi dẫn đến khả năng dự báo của một model trong điều kiện thực tế giảm đi. Điều này cũng giống như một người đã được training rất kỹ trong chuyên môn của mình, nhưng sự nhạy bén lại giảm đi đáng kể trong các vấn đề thực tế khác ngoài xã hội.

## Nguyên nhân

Về phương diện kỹ thuật, có hai nguyên nhân chính dẫn đến model drift đó là data drift và concept drift.

- Data drift là các thay đổi trong nội tại data trên môi trường production. Các thay đổi này là các suy biến tự nhiên theo thời gian của các yếu tố được đặt làm attribute của model, ví dụ như thói quen của khách hàng thay đổi theo thời gian, sự biến đổi trong hành vi khách hàng... Điều này có thể biểu diễn bằng sự thay đổi của phân phối dữ liệu trong việc training và dữ liệu trên production.

- Concept drift là các thay đổi trong bản chất mối quan hệ của biến được dự báo và các biến độc lập trong mô hình. Ví dụ như sự thay đổi của hành vi khách hàng khi tuổi của khách hàng ngày một tăng lên. Hoặc có một sự kiện đặc biệt khiến các mối quan hệ của biến độc lập và phụ thuộc thay đổi như covid19 khiến hành vi, thói quen mua sắm cơ bản thay đổi trong và sau khi covid19 kết thúc. 

Về các nguyên nhân thực tế, có thể kể ra một số nguyên nhân sau:

### Thay đổi trong hành vi khách hàng

Sự thay đổi đến từ nhiều nguyên nhân khác nhau ví dụ như công nghệ thay đổi, văn hóa, các mối quan hệ trong xã hội của khách hàng. Các thay đổi này dẫn đến các hành vi không dự báo được trước bởi các model cũ. Ví dụ như với cùng một điều kiện, thì một bạn sinh viên sẽ có phản ứng khác với chính bạn sinh viên đó đã đi làm được một vài năm. Nếu áp dụng các model dự báo cũ cho bạn sinh viên thời đi học, thì kết quả dự đoán chắc chắn sẽ không hiệu quả.

### Yếu tố mùa vụ

Yếu tố mùa vụ có trong nhiều sự kiện, thói quen khác nhau của người dùng. Ví dụ như khách hàng có nhu cầu mua sắm nhiều hơn trước các dịp nghỉ lễ lớn, mùa hè, mùa đông, khách hàng đều có các hành vi khác nhau. Ngoài ra, các chủ thể kinh tế đều có ảnh hưởng qua lại lẫn nhau, vì vậy xét về các yếu tố nói chung, yếu tố mùa vụ là yếu tố quan trọng trong các model dự báo.

### Sự thay đổi của thiết bị/ phương pháp đo đạc

Suy rộng hơn, là sự thay đổi về bản chất mối quan hệ trong business với một trường dữ liệu nhất định. Ví dụ cùng một trường dữ liệu là giới tính, việc ghi nhân bằng tay/form giấy sẽ hoàn toàn khác so với ghi nhận bằng eKYC. Hay cùng một trường thông tin như status của khách hàng, nhưng nâng cấp hệ thống ghi nhận logic khác so với logic cũ, dẫn đến bản chất trong các mối quan hệ xung quanh biến đó thay đổi so với trước.

### Sự kiện đột xuất

Các sự kiện đột xuất có ảnh hưởng ngắn hạn, dài hạn đến các biến dữ liệu. Ví dụ như việc ngân hàng tăng lãi suất sẽ luôn có tác động ngắn, dài hạn khác nhau đến nền kinh tế. Hoặc các sự kiện cực đoan như đại dịch covid19 cũng gây ra ảnh hưởng rất nhiều đến các mối quan hệ trong nền kinh tế.

### Nguồn dữ liệu, quy trình thu thập dữ liệu thay đổi

Ví dụ như cùng một form khảo sát trong dân số, việc quy trình thu thập thông tin thay đổi, hoặc ở các vùng khác nhau sẽ dẫn đến các thay đổi khác nhau trong dữ liệu thu thập được.

### Chất lượng dữ liệu thay đổi

Đặc biệt là các dữ liệu có sự can thiệp bởi con người, mỗi người khác nhau thường sẽ mắc các lỗi khác nhau dẫn đến các dữ liệu đầu vào không đồng nhất về chất lượng ở các giai đoạn khác nhau. Ngoài ra còn nhiều nguyên khác không thể tính đến khiến cho chất lượng dữ liệu có thay đổi theo thời gian.

## Biểu hiện và các phương pháp nhận biết

### Prediction drift

Khi nói đến Data drift, ta đang nói đến các thay đổi trong phân phối của các biến đầu vào. Khi nói đến Prediction drift, ta đang nói đến các thay đổi trong chính biến được dự báo. Ví dụ, một model dự báo giá cho sản phẩm gần đây thường cho kết quả dự báo (có phân phối) thấp hơn kết quả training, validate model. 

Prediction drift không chỉ bao hàm việc suy giảm độ chính xác của model, nó còn bao hàm cả việc model có độ chính xác cao hơn so với khi training khi áp dụng trong dữ liệu thực tế. Prediction drift, cùng với data drift đều đưa ra các tín hiệu tin cậy cho sự thay đổi của model trong môi trường thực tế.

Trong một số trường hợp, người ta còn nói data drift hoặc dataset shift như là một trong các trường hợp của input và output của model bị thay đổi.

### Training-serving skew

Điều này chỉ ra việc model không hoạt động hiệu quả trong điều kiện thực tế vì sự sai khác của dữ liệu thực tế so với dữ liệu training. Sự sai khác này khác với data drift ở chỗ nó là sự sai khác thực tế, và ngay lập tức nếu như so với dữ liệu training. Model, trên thực tế sẽ không thể hoạt động nếu thiếu các tính toán các biến quan trọng. Vì vậy, trong trường hợp dữ liệu đầu vào có phân phối, định dạng khác với dữ liệu training, thì là một điểm đáng lưu ý để xem xét để đảm bảo kết quả của model là chính xác.

### Data quality

Chất lượng dữ liệu là một vấn đề quan trọng trong quá trình training và serving trên môi trường thực tế, nếu dữ liệu mới có quá nhiều null value, về cơ bản thì ý nghĩa của bộ dữ liệu đã thực sự có những thay đổi mà khi training ta không lường trước hết được. Việc kiểm tra lại giá trị null là cần thiết để đánh giá model drift.

Ngoài ra, việc xuất hiện dữ liệu mới cũng là dấu hiệu đáng chú ý, ví dụ công ty mở rộng kinh doanh ra tỉnh thành mới, model dự báo cho các dữ liệu ở tính mới này cũng cần hết sức lưu ý vì có thể không chính xác, hoặc ít nhất chúng ta nên monitor rất kỹ kết quả dự báo để tránh các rủi ro xảy ra.

### Outlier detection

Để tìm ra các thay đổi về dữ liệu, ta có thể dựa vào các điểm bất thường trong dữ liệu. Nếu các điểm dị thường này có phân phối khác nhau giữa dữ liệu cũ và mới, thì dường như tính chất của dữ liệu có thể đã thay đổi. Các điểm dị thường thường là các trường hợp cực đoan của logic business, nếu các điểm cực đoan này có biểu hiện khác đi, chứng tỏ business có thể đã thay đổi từ bên trong.

## Các phương pháp phát hiện Model Drift

### Thống kê mô tả

Sử dụng các chỉ số thống kê mô tả cơ bản để xác định các thay đổi trong dữ liệu. Ví dụ như mean, median, std, skewness, kurtosis, mode. Xem xét các chỉ số này có thể cho ta thấy mức độ thay đổi trong tổng thể dữ liệu. Một sự dịch chuyển về tổng thể sẽ dẫn đến thay đổi các chỉ số. 

Một chỉ tiêu quan trọng trong phần này là phân phối của bộ dữ liệu, phân phối cho biết tần suất theo một giá trị nhất đinh, nếu phân phối của dữ liệu thay đổi, chứng tỏ đã có sự chuyển dịch trong dữ liệu.

### Kiểm định thống kê

Sử dụng các kiểm định như T-test, F-test, Chi-square test, Kolmogorov Smirnov để kiểm định sự thay đổi thực tế trong dữ liệu.

### Rule-based checks

Sử dụng các rule thực tế được đúc kết bằng kinh nghiệm làm việc, hoặc các ngưỡng chung để giới hạn, nếu dữ liệu vượt qua các ngưỡng này thì ta có thể kết luận có hiện tượng drift diễn ra. Ví dụ tỷ lệ dư nợ của khách hàng vượt ngưỡng thì cần phải xem xét ngay lại bộ dữ liệu để đảm bảo phòng ngừa rủi ro.

## Các phương pháp xử lý

Có nhiều phương pháp xử lý hiện tượng model drift này, các phương pháp giúp cập nhật dữ liệu, model, hoặc thực hiện các phân tích đánh giá ảnh hưởng.

### Phân tích các thay đổi

Trước khi thực hiện chỉnh sửa model, chúng ta cần hiểu bản chất của sự thay đổi trong dữ liệu. Tìm hiểu được bản chất, nguyên nhân, ta sẽ có các thay đổi tương ứng. Ví dụ nếu drift do chất lượng dữ liệu, thì cần khắc phục ngay từ khâu nhập liệu...

### Retraining model

#### Turning lại bộ tham số

Thay đổi các hyper param trong model ví dụ như ngưỡng nhận biết các cluster...

#### Turning lại bộ feature đầu vào

Thay đổi bộ feature đầu vào phù hợp với các thay đổi mới, cập nhật thêm các logic mới. Ví dụ như có một trường dữ liệu mang tính chất phân loại cao được thêm vào logic của hệ thống.

#### Thay đổi model đầu vào

Có thể thử nghiệm các loại model khác nhau để khắc phục các nhược điểm cố hữu của từng model, việc thay đổi model cần được sắp xếp hợp lý với việc thay đổi features để đảm bảo đưa ra lựa chọn phù hợp tối ưu nhất.

#### Thêm dữ liệu mới vào trong quá trình training

Khi việc thay đổi dữ liệu là tự nhiên, thì thêm dữ liệu mới vào việc training là việc cần thiết để model nhận ra sự thay đổi trong hành vi khách hàng.

### Tần suất Retrain Model

Một vấn đề tiếp theo cần quan tâm là tần suất retrain model như thế nào là hợp lý?

Câu trả lời là không có một quy định, quy tắc cụ thể nào cả. Tùy từng bài toán mà ta có cách xử lý khác nhau.

Retrain model tại một thời điểm cố định nếu ta biết trước chính xác thời điểm dữ liệu có sự thay đổi lớn. VD: tại các trường đại học, đầu mỗi năm học đều có số lượng lớn sinh viên nhập học và ra trường thì ta nên retrain lại model tại thời điểm đó.
Retrain model khi thu thập được đủ một lượng dữ liệu nhất định
Retrain model khi các metrics mà ta theo dõi (như đề cập trong mục 2) thay đổi vượt quá một ngưỡng nào đó.
Đối với cách thứ 2&3, cần phải có một hạ tầng độc để giám sát và đưa ra cảnh báo khi sự thay đổi đạt đến mức quy định. Việc chọn ngưỡng cho các metrics cũng cần phải xem xét cẩn thận. Ngưỡng quá thấp sẽ làm cho tần suất retrain model thường xuyên hơn, dẫn đến tốn kém chi phí tính toán (đặc biệt quan trong trường trường hợp sử dụng tài nguyên trên cloud). Ngưỡng quá cao làm cho model không thay đổi kịp với sự thay đổi của môi trường, dẫn đến không tối ưu hóa lợi nhuận, …

Đặc biệt trong trường hợp model cần thay đổi realtime mỗi khi có bất cứ dữ liệu mới (VD model dự đoán giao dịch ngân hàng an toàn hay không an toàn) thì nên sử dụng phương pháp học tăng dần, Incremental Learning / Online Learning. Phương pháp này khác các cách Retrain Model đã đề cập ở chỗ model được retrain (cập nhật) chỉ sử dụng dữ liệu mới, không phải retrain trên toàn bộ dữ liệu.

### Chạy Retrain Model tự động

Cách cấu hình để Retrain Model tự động liên quan đến tần suất retrain model của bạn.

Nếu model được retrained định kỳ, chúng ta có thể sử dụng Kubernetes CronJobs hoặc Jenkins để lập lịch cho model chạy retrain.

Nếu model đươc retrained dựa vào trigger khi các metrics thay đổi đến ngưỡng được phát hiện, chúng ta có thể sử dụng Kubernetes Jobs hoặc Jenkins để làm việc này.

Cuối cùng, nếu model cần retrain realtime, sử dụng phương pháp Online Learning. River là thư viện lý tưởng cho việc này. Tên cũ của nó là Creme.
