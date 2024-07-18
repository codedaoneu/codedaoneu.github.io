---
layout: post
title: "ML Testing and Validation"
author: "codedaoneu"
tags: tutorial
---


## ML Testing là gì?

Không giống như các phương pháp kiểm định phần mềm thông thường và truyền thống, công việc chỉ bao gồm kiểm tra tính chính xác của mã nguồn cũng như kết quả của bộ mã. Phương pháp ML cho phép học dữ liệu, xác định các phương pháp và tự đưa ra quyết định. Đây là một mô hình tự học, có độ phức tạp và mức độ tương đối cao. Nếu một phần mềm truyền thống trả ra lỗi, thường thì các lỗi đó đến từ logic của bộ mã. Tuy nhiên, nếu một ML model trả ra dữ liệu không hợp lý, nó có thể đến từ nhiều nguyên nhân khác nhau:
- Tính thiên kiến khi training data.
- Lỗi dữ liệu quá khớp (overfitting).
- Tính không lường trước được của các biến trong bộ dữ liệu.

## Tầm quan trọng của ML Testing:

### Duy trì tính chính xác của model

ML model được training bởi dữ liệu lịch sử, và độ chính xác của nó phụ thuộc vào chất lượng của dữ liệu đó. ML model testing giúp nhận dạng các lỗi giữa biến được dự báo và giá trị thực tế trả ra. Đây chính là tính chính xác của model.

### Bảo vệ khỏi sự thiên kiến (bias)

Bias trong ML model có thể trả ra các kết quả không công bằng trong dữ liệu kết quả. Thorough testing có thể làm bộc lộ sự thiên kiến này, dẫn đến các dev có thể xác định được vấn đề và tạo ra các model mang tính công bằng cao hơn.

### Đáp ứng sự thay đổi của dữ liệu

Đảm bảo model vẫn hiệu quả với các dữ liệu mới, duy trì sức mạnh dự báo theo thời gian.

### Nâng cao độ tin cậy

Duy trì sức mạnh dự báo của model. Đảm bảo hiệu suất được nâng cao và giảm các rủi ro dự báo sai không lường trước được.

## Các loại ML Testing

### Unit Testing for Components

Giống như các phương pháp kiểm thử truyền thống khác, unit test tập trung vào từng bước riêng lẻ của quá trình training và deploy ML model, ví dụ như các bước:
- Prepare data
- Data cleaning
- Feature extraction
- Model architecture
- Hyperparam turning
- Deploy model

Mỗi bước cần đảm bảo sự chính xác riêng, việc define các test case ở mỗi bước là việc làm cần thiết và hiệu quả để kiểm thử ML model.

### Data Testing và preprocessing

Chất lượng data giữ một vai trò quan trọng trong việc training model. Việc kiểm tra data bao gồm các công việc như đảm bảo tính chính xác, tính thống nhất và toàn vẹn của dữ liệu được đưa vào model. Kiểm định data sẽ bao gồm trong các bước:
- Data transformation
- Data normalisation
- Data cleaning
- Data loading and limitation.

### Cross-Validation

Là một phương pháp kỹ thuật mạnh mẽ để định lượng hóa mức độ hiệu quả của model. Mức độ hiệu quả này được định lượng bằng cách không cho phép độ chính xác của model phụ thuộc vào dữ liệu đầu vào, nói cách khác, chúng ta hoàn toàn có thể kỳ vọng mức độ chính xác với dữ liệu thực tế ở mức tương tự như mức độ hiệu quả sau khi model được đánh giá bằng phương pháp này.

### Performance Metrics Testing

Lựa chọn phương pháp tiếp cận để đánh giá mức độ hiệu quả của model là phương pháp bắt buộc và được tính toán trước tiên. Metric có thể là accuracy, recall, F1_score... mang ý nghĩa khác nhau đối với từng model. VỚi từng model khác nhau, để đánh giá hiệu quả, trước hết ta cần phải định nghĩa ra một bộ metric hiệu quả để có thể đánh giá model này.

### Robustness and Adversarial Testing

Phương pháp này đo lượng mức độ xử lý hiệu quả của model khi nhận một đầu vào không như mong đợi và một cuộc tấn công bất thường. Phương pháp này nhằm đánh giá hành vi của model khi thay đổi một biến đầu vào trở nên bất thường, và gây nhầm lẫn đối với model và người dùng. Mức độ mạnh mẽ của model giống như việc đưa ra các dự báo hợp lý hơn khi nhận các điều kiện đầu vào thách thức hoặc bất thường.

### A/B Testing for Deployment

Triển khai cùng lúc nhiều mô hình khác nhau và đánh giá hiệu quả của từng mô hình so với dữ liệu thực tế để tìm ra mô hình hiệu quả nhất. Đánh giá trên nhiều mô hình khác nhau để đảm bảo có ít nhất một mô hình perform hiệu quả với dữ liệu thực tế, và đảm bảo các kết quả không có sự bất thường xảy ra.

### Bias Testing

Đánh giá sự thiên kiến. Đảm bảo model trả ra kết quả công bằng với mọi dữ liệu được đưa vào mô hình.

## Một số Metrics đo lường ML Models

- Accuracy
- Precision
- Sensitivity
- Specificity
- Area Under the ROC Curve (AUC-ROC)
- Mean Absolute Error (MAE)
- Root Mean Squared Error (RMSE)

## Tổng kêt

Trên đây là một số loại hình và phương pháp để kiểm thử ML model, mỗi phương pháp sẽ xử lý một loạt các vấn đề khác nhau mà model có thể gặp phải. Ngoài ra, theo thời gian thì model có thể suy giảm độ chính xác, hoặc thậm chí trở nên không hiệu quả do dữ liệu thay đổi theo thời gian, vì vậy việc maintain model thường xuyên là việc làm hết sức quan trọng nhằm duy trì và cập nhật kịp thời, đảm bảo độ chính xác, tin cậy theo thời gian. Để hỗ trợ cho công việc, ta có thể sử dụng một số framework sau:
- TensorFlow
- PyTorch
- Scikit-learn
- Fairlearn

Ngoài ra, chúng ta cũng cần quan tâm đến các vấn đề khác như:
- Data Privacy and Security
- Fairness and Bias
- Transparency and Explainability
- Accountability and Liability
- Human-Centric Design
- Consent and Data Usage
- Long-Term Effects
- Collaborative Oversight

Các vấn đề trên giúp việc kiểm thử model trở nên an toàn và thực tế hơn trong điều kiện làm việc của một công ty, hoặc các team khác nhau.

Link tham khảo:

- https://www.testingxperts.com/blog/ml-testing
- https://deepchecks.com/how-to-test-machine-learning-models/
- https://censius.ai/blogs/model-testing-types-methods-and-best-practices
- https://research.aimultiple.com/ml-model-testing/
- https://www.markovml.com/blog/model-testing
- https://www.design-reuse.com/articles/55045/exploring-machine-learning-testing-and-its-tools-and-frameworks.html
- https://www.sciencedirect.com/science/article/pii/S0920410517308094


