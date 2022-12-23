---
layout: post
title: "Bài 2: Hồi quy đơn biến"
author: "codedaoneu"
tags: econometrics
---

## Hồi quy đơn biến

### Giới thiệu bộ dữ liệu giá nhà và bài toán dự báo giá nhà

Là một bài toán trên <kaggle.com> . Được xem như là sân chơi quốc tế dành cho cộng đồng trí tuệ nhân tạo, khám phá và xây dựng các mô hình AI. 

Link cuộc thi: <https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques>

Bộ dữ liệu và mô tả: <https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/data>

### Hồi quy đơn biến

Ở đây tôi lấy Python làm công cụ do mức độ phổ biến và được các công ty chấp nhận, áp dụng rộng rãi. Trong trường học, chúng ta cũng đã được áp dụng với một số công cụ phân tích thống kê như Eviews, SPSS,... Ta cũng hoàn toàn có thể sử dụng các công cụ này để thực hiện các phép tính và ước lượng mô hình hồi quy.

Theo cách tiếp cận của KTL và áp dụng mô hình hồi quy đơn biến, trong bộ dữ liệu, tôi chọn biến độc lập X là biến **LotArea** dựa theo quan niệm cơ bản về giá đất, đó là miếng đất càng to thì giá càng cao. Biến phụ thuộc Y là biến **SalePrice**.

Hơi khác một chút so với phương pháp luận của KTL, nhưng tôi đã trình bày ở trên, chúng ta đã có dữ liệu trước, rồi mới đi tìm mô hình thích hợp để giải thích và dự báo.

#### 1. Tổng quan bộ dữ liệu:

Gọi biến độc lập **LotArea** là biến X, biến phụ thuộc **SalePrice** là biến Y, thực hiện việc đọc bộ dữ liệu:

```python
data = pd.read_csv('data/house_prices/train.csv')
train_data = pd.DataFrame(data[['SalePrice'
                                , 'LotArea']]).reset_index()
del train_data['index']
train_data = train_data.rename(columns={'SalePrice': 'Y'
                                        , 'LotArea': 'X'})

print(train_data.info())
```

Kết quả:

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 1460 entries, 0 to 1459
Data columns (total 2 columns):
 #   Column  Non-Null Count  Dtype
---  ------  --------------  -----
 0   Y       1460 non-null   int64
 1   X       1460 non-null   int64
dtypes: int64(2)
memory usage: 22.9 KB
None
```

Bộ dữ liệu có 1460 quan sát. Dữ liệu không chứa giá trị null.

Biểu diễn tương quan của biến độc lập và biến phụ thuộc:

```python
plt.figure(figsize=(10,8))

plt.scatter(train_data["X"], train_data["Y"], marker='o', alpha=0.3 , color = 'g', label=True)
plt.xlabel("X")
plt.ylabel("Y")
plt.grid(True)

plt.show()
```

Kết quả:

```
<ẢNh>
```

Nhận xét: Hầu hết các căn nhà được định giá trong tập dữ liệu đều có diện tích từ xấp xỉ 0 đến 50000 đơn vị diện tích. Mức giá cũng phân bố trong khoảng chủ yếu từ 100000 đến 400000 đơn vị tiền tệ. Xu hướng phân bố của dữ liệu khá co cụm theo trục X và trải rộng theo trục Y, điều này có ý nghĩa là với cùng một diện tích, các ngôi nhà có thể có các mức định giá rất khá nhau, điều này cho biết rằng việc định giá nhà cửa còn nhiều yếu tố bên ngoài khác ngoài mô hình. Ngoài ra cũng có một số điểm ngoại lệ, đó là 2 điểm cao góc trên bên trái, diện tích của hai căn nhà này cũng không quá khác biệt so với các ngôi nhà khác nhưng được định giá đặc biệt cao, hay như điểm bên phải xa nhất, tuy có diện tích rất lớn nhưng mức giá được định tương đối thấp so với các bất động sản có diện tích nhỏ.


#### Xây dựng mô hình và hàm hồi quy

Xác định loại mô hình:

Ta sẽ cần xác định mô hình hồi quy có hệ số chặn hay không. Trên thực tế, nếu bất động sản có diện tích = 0 thì mức giá cũng sẽ = 0, vì vậy có thể thấy mô hình không có hệ số chặn phù hợp với thực tế hơn.

Sử dụng phương pháp OLS với thư viện statsmodel hỗ trợ, training mô hình theo phương pháp OLS không có hệ số chặn.

```python
# Chuẩn bị dữ liệu
X = train_data['X'].values.reshape(-1,1)
y = train_data['Y'].values.reshape(-1,1)

mod = sm.OLS(y, X)
res = mod.fit()

print(res.summary())
```

Kết quả: 

```
                                 OLS Regression Results                                
=======================================================================================
Dep. Variable:                      y   R-squared (uncentered):                   0.544
Model:                            OLS   Adj. R-squared (uncentered):              0.543
Method:                 Least Squares   F-statistic:                              1737.
Date:                Fri, 23 Dec 2022   Prob (F-statistic):                   9.42e-251
Time:                        22:13:42   Log-Likelihood:                         -19302.
No. Observations:                1460   AIC:                                  3.861e+04
Df Residuals:                    1459   BIC:                                  3.861e+04
Df Model:                           1                                                  
Covariance Type:            nonrobust                                                  
==============================================================================
                 coef    std err          t      P>|t|      [0.025      0.975]
------------------------------------------------------------------------------
x1            10.0484      0.241     41.683      0.000       9.576      10.521
==============================================================================
Omnibus:                     1902.440   Durbin-Watson:                   1.383
Prob(Omnibus):                  0.000   Jarque-Bera (JB):           622467.528
Skew:                          -6.735   Prob(JB):                         0.00
Kurtosis:                     103.254   Cond. No.                         1.00
==============================================================================

Notes:
[1] R² is computed without centering (uncentered) since the model does not contain a constant.
[2] Standard Errors assume that the covariance matrix of the errors is correctly specified.
```

Diễn giải kết quả ước lượng:

X1 = 10.0484 có ý nghĩa, khi diện tích của nhà ở tăng lên 1 đơn vị diện tích thì giá nhà sẽ tăng lên 10 đơn vị tiền tệ. Trên thực tế, đây chính là giá trung bình của 1 met vuông nhà.

P>|t| = 0.000

Hệ số P_value cho thấy với mọi mức ý nghĩa lớn hơn P_value thì giả thiết H0: Biến X không có ý nghĩa trong mô hình hồi quy đều được bác bỏ. Điều này ngụ ý rằng biến X là có ý nghĩa trong mô hình với mọi mức ý nghĩa (P_value ~ 0).

R-squared (uncentered): = 0.544

Hệ số R-squared (uncentered) được hiệu chỉnh lại để phù hợp với mô hình hồi quy không có hệ số chặn. Hệ số này có ý nghĩa biến X giải thích được 54.4% sự thay đổi của biến phụ thuộc. Hay diện tích của nhà ở sẽ có thể giải thích được 54.4% sự thay đổi của giá nhà. Điều này khẳng định lại nhận định ban đầu là có nhiều yếu tố khác ảnh hưởng đến giá nhà ngoài diện tích của căn nhà đó.

Bài tiếp theo, chúng ta sẽ bổ sung các biến khác trong mô hình bằng cách bổ sung thêm các biến độc lập vào mô hình hồi quy đa biến.






