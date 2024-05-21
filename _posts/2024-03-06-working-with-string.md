---
layout: post
title: "Các phương pháp đánh giá mô hình phân lớp"
author: "codedaoneu"
tags: tutorial python
---

## 1. Các phương pháp chính.

- Accuracy
- Confusion matrix
- True/False Positive/Negative
- Receiver Operating Characteristic curve
- Area Under the Curve
- Precision và Recall

## Accuracy

Chính là tỷ lệ số điểm được dự đoán đúng trên tổng số điểm dữ liệu được dự đoán trong tập test.

## Confusion matrix

Là một ma trận thể hiện số điểm được dự đoán đúng và sai của từng phân lớp.

```
 Total: 10 | Predicted | Predicted | Predicted |   
           |    as: 0  |    as: 1  |    as: 2  |   
-----------|-----------|-----------|-----------|---
 True: 0   |     2     |     1     |     1     | 4 
-----------|-----------|-----------|-----------|---
 True: 1   |     1     |     2     |     0     | 3 
-----------|-----------|-----------|-----------|---
 True: 2   |     0     |     1     |     2     | 3 
-----------|-----------|-----------|-----------|---
```

Tổng các phần tử trong ma trận chính là tổng số điểm dữ liệu trong tập dữ liệu test.

Tổng số phần tử trên đường chéo của ma trận là tổng số điểm dữ liệu được dự đoán
chính xác.

Ý nghĩa: Phuương pháp đánh giá này giúp biết được tỷ lệ dự đoán đúng
của từng phân lớp và mức độ hiệu quả nói chung của mô hình.

## True/False Positive/Negative

```
                  |      Predicted      |      Predicted      |
                  |     as Positive     |     as Negative     |
------------------|---------------------|---------------------|
 Actual: Positive | True Positive (TP)  | False Negative (FN) |
------------------|---------------------|---------------------|
 Actual: Negative | False Positive (FP) | True Negative (TN)  |
------------------|---------------------|---------------------|
```

Phương pháp này thường được sử dụng trong mô hình phân loại chỉ có 2 lớp.
Phương pháp này giúp đánh giá hiện trạng dự đoán kết quả của từng nhóm dự đoán
, từ đó có thể lựa chọn mô hình để tăng khả năng dự đoán của một nhóm nhất định.

### Receiver Operating Characteristic curve (ROC)

Trong một số bài toán, chúng ta có thể sử dụng ngưỡng nhất định nào đó để
tăng hay giảm False Negative Rate hoặc False Positive Rate.

Đường cong ROC biểu diễn tất cả các cặp xác suất TPR và FPR trong dữ liệu tương
ứng với tất cả các ngưỡng  có thể được lựa chọn. Việc lựa chọn ngưỡng
có thể đảm bảo việc lựa chọn nhóm dự đoán quan trọng hơn đối với mô hình.

Đường còn ROC càng tốt khi nó có tiệm cận với trục TPR dốc đứng và tiệm cận
với đường FPR nằm ngang, điều này thể hiện là với bất kỳ ngưỡng được lựa chọn
nào, chúng ta đều có tỷ lệ dự đoán đúng cao, tỷ lệ dự đoán sai thấp.

Một cách đánh giá khác của đường ROC là diện tích bên dưới của nó càng tiệm cận 1 thì càng tốt.

## Precision và Recall

``` 
                  |     Predicted      |     Predicted      |
                  |    as Positive     |    as Negative     |
------------------|--------------------|--------------------|
 Actual: Positive | TPR = TP/(TP + FN) | FNR = FN/(TP + FN) |
------------------|--------------------|--------------------|
 Actual: Negative | FPR = FP/(FP + TN) | TNR = TN/(FP + TN) |
------------------|--------------------|--------------------|
```

Được sử dụng để đánh gái bài toán phân loại mà dữ liệu của các lớp là chênh
lệch nhau rất nhiều. 

- Precision = TP/(TP + FP)
- Recall = TP(TP + FN) = TPR

Precision cao chứng tỏ mô hình dự đoán càng chính xác các điểm dữ liệu.
Recall cao chứng tỏ tỷ lệ bỏ sót các điểm thực sự là positive thấp.

Khi Precision = 1 tức là mọi điểm tìm được đều là điểm Positive, tuy nhiên
mô hình không đảm bảo tìm được mọi điểm positive.

Khi Recall = 1 tức là mọi điểm positive đều được tìm thấy, nhưng không đảm
bảo có lẫn các điểm negative không.

Một mô hình tốt khi có cả 2 điểm trên càng cao.

### F1-score

Bằng trung bình harmonic của precision và recall.

F1-score = 1/Precision + 1/Recall

Điểm R1-Score có giá trị nằm trong khoảng `(0;1]`. Điểm F1 càng cao thì một mô hình càng được phân lớp tốt, khi đó cả precision và recall đầu bằng 1. Nếu cần phải đánh giá các mô hình khác nhau có chỉ số precision và recall khác nhau thì điểm R1 là một thước đo ổn định cho cả hai chỉ số.


