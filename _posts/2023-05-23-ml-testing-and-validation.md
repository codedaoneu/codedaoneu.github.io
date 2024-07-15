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

