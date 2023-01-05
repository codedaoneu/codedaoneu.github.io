---
layout: post
title: "Bài 4: Triển khai mô hình"
author: "codedaoneu"
tags: econometrics
---

## Sử dụng MLFlow để theo dõi hiệu quả training mô hình

MLFlow là một nền tảng mã nguồn mở để quản lý vòng đời học máy từ đầu đến cuối. Nó giải quyết bốn chức năng chính:

* Theo dõi các thí nghiệm để ghi lại và so sánh các thông số và kết quả.
* Đóng gói bộ code ở dạng có thể tái sử dụng, có thể tái tạo code, môi trường chạy code cho nhiều người cùng sử dụng.
* Quản lý và triển khai các mô hình từ nhiều thư viện ML.
* Quản lý toàn bộ vòng đời của Mô hình MLflow, bao gồm lập phiên bản cho các lần training mô hình, ghi chép lại các nâng cấp cải tiến của mô hình.

Xuất phát từ nhu cầu theo dõi hiệu quả của việc training mô hình với các thay đổi theo thời gian, ta có thể sử dụng MLFlow để ghi chép lại các chỉ số hiệu quả, từ đó dễ đánh giá cho các lần chạy tiếp theo

Ví dụ với mô hình OLS dự báo giá nhà, ta sẽ so sánh giữa việc training mô hình OLS có hệ số chặn và mô hình OLS không có hệ số chặn. Như vậy, tham số cần theo dõi ở việc thực hiện training mô hình là hệ số chặn. Ta quy ước như sau, nếu ta truyền tham số 0 vào việc training mô hình thì mô hình là không có hệ số chặn, nếu truyền 1 vào khi training mô hình thì mô hình có hệ số chặn.

Trước hết, cần import thư viện cần thiết cho việc truyền tham số:

``` python
import sys
```

giả sử file thực thi chương trình python có tên là ols_model.py, khi tiến hành chạy chương trình, ta có thể truyền tham số như sau:

```python ols_model.py 0```

tham số 0 ở cuối cùng chính là quy ước của chúng ta bên trên, 0 thì mô hình là không có hệ số chặn, nếu truyền 1 thì việc training mô hình là mô hình OLS có hệ số chặn.

Đây là kiến thức cơ bản khi khởi chạy một file python, sau đây chúng ta sẽ đi từng bước để có thể training mô hình.

Bước 1: Import các thư viện cần thiết:

``` python
import sys

import mlflow
import pandas as pd
import numpy as np

from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn import metrics
```

Bước 2: Đọc dữ liệu:

``` python
    try:
        data = pd.read_csv('data/house_prices/train.csv')
    except Exception as E:
        print("Unable to read file data, detail: {0}".format(E))
```

Đọc dữ liệu trong cấu trúc try: except để kiểm soát việc đọc dữ liệu, nếu có lỗi đọc dữ liệu thì chương trình sẽ dừng lại và in ra dòng lệnh lỗi, việc này giúp ta có thể kiểm soát chương trình tốt hơn cũng như dễ tìm lỗi khi chạy chương trình.

Bước 3: Biến đổi dữ liệu (chuẩn bị dữ liệu training)

```python
    model_data = data[["SalePrice", "LotArea", "WoodDeckSF", "OpenPorchSF",
                       "1stFlrSF", "GrLivArea", "MSSubClass", "MSZoning", "Neighborhood", "BedroomAbvGr"]]

    model_data_all = pd.get_dummies(model_data
                                    , prefix=["MSSubClass", "MSZoning", "Neighborhood", "BedroomAbvGr"]
                                    , columns=["MSSubClass", "MSZoning", "Neighborhood", "BedroomAbvGr"]
                                    , drop_first=False
                                    )
    Y = model_data_all["SalePrice"]
    X = model_data_all.loc[:, model_data_all.columns != "SalePrice"]
```

Lựa chọn các biến cần thiết và tạo các biến giả dựa trên dữ liệu có sẵn, sau đó ta tách riêng biến phụ thuộc và các biến độc lập để chuẩn bị cho việc training

Bước 4: Chia tập train, test

``` python
X_train, X_test, Y_train, Y_test = train_test_split(X, Y,                                                   
test_size=0.2
,random_state=40
)
```

Chia dữ liệu thành hai tập train test để kiểm thử mô hình với dữ liệu ngoài không được training.

Bước 5: Đọc các tham số được truyền vào mô hình

``` python
    try:
        if int(sys.argv[1]) == 1:
            intercept = True
        elif int(sys.argv[1]) == 0:
            intercept = False
        else:
            raise "wrong intercept input (intercept must be 0 or 1)"
    except Exception as e:
        print("Unable to read or missing intercept argument: {0}".format(e))

```

Tương tự như trên, ta đặt việc đọc tham số trong cấu trúc try: except để kiểm soát việc nhập tham số vào mô hình.

Bước 6: Khởi chạy MLFlow và tiến hành training mô hình

``` python
    with mlflow.start_run():
        reg = LinearRegression(fit_intercept=intercept)
        reg.fit(X_train, Y_train)
        Y_pred = reg.predict(X_test)

        n = X_test.shape[0]
        p = X_test.shape[1]

        r2 = metrics.r2_score(Y_test, Y_pred)
        r2_adjusted = 1 - (1 - r2) * (n - 1) / (n - p - 1)

        resid = np.array(Y_test) - Y_pred

        mlflow.log_param("intercept", intercept)
        mlflow.log_metric("r2_score", r2)
        mlflow.log_metric("r2_adjusted", r2_adjusted)
        mlflow.log_metric("resid_mean", round(resid.mean(), 2))
        mlflow.log_metric("resid_std", round(resid.std(), 2))
```

        mlflow.log_metric("resid_std", round(resid.std(), 2))
Sau khi training mô hình xong, ta ghi chép lại các chỉ số hiệu quả của mô hình bao gồm các chỉ số r2_score, r2_adjusted, resid_mean, resid_std. Các chỉ số này được ghi chép lại bằng hàm log_metric. Với tham số truyền vào mô hình, ta dùng hàm log_param để lưu lại. Sau khi training và đo lường chỉ số hiệu quả với tập dữ liệu test, kết quả hiển thị trên MLFlow như sau:

![Ví dụ](https://github.com/codedaoneu/codedaoneu.github.io/blob/master/images/2022-12-27-mlflow-example.png?raw=true)

Với việc sử dụng MLFlow để training mô hình, ta có thể so sánh một cách trực quan việc training nhiều lần mô hình, hoặc có thể so sánh hiệu quả training mô hình sử dụng nhiều loại mô hình khác nhau, cũng như điều chỉnh tham số để cho kết quả tốt nhất.
