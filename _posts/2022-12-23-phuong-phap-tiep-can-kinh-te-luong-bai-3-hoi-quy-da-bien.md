---
layout: post
title: "Bài 3: Hồi quy đa biến"
author: "codedaoneu"
tags: econometrics
---

## Hồi quy đa biến

### Lựa chọn các biến đưa vào mô hình

```python
data = pd.read_csv('data/house_prices/train.csv')

data.info()
```

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 1460 entries, 0 to 1459
Data columns (total 81 columns):
 #   Column         Non-Null Count  Dtype  
---  ------         --------------  -----  
 0   Id             1460 non-null   int64  
 1   MSSubClass     1460 non-null   int64  
 2   MSZoning       1460 non-null   object 
 3   LotFrontage    1201 non-null   float64
 4   LotArea        1460 non-null   int64  
 5   Street         1460 non-null   object 
 6   Alley          91 non-null     object 
 7   LotShape       1460 non-null   object 
 8   LandContour    1460 non-null   object 
 9   Utilities      1460 non-null   object 
 10  LotConfig      1460 non-null   object 
 11  LandSlope      1460 non-null   object 
 12  Neighborhood   1460 non-null   object 
 13  Condition1     1460 non-null   object 
 14  Condition2     1460 non-null   object 
 15  BldgType       1460 non-null   object 
 16  HouseStyle     1460 non-null   object 
 17  OverallQual    1460 non-null   int64  
 18  OverallCond    1460 non-null   int64  
 19  YearBuilt      1460 non-null   int64  
 20  YearRemodAdd   1460 non-null   int64  
 21  RoofStyle      1460 non-null   object 
 22  RoofMatl       1460 non-null   object 
 23  Exterior1st    1460 non-null   object 
 24  Exterior2nd    1460 non-null   object 
 25  MasVnrType     1452 non-null   object 
 26  MasVnrArea     1452 non-null   float64
 27  ExterQual      1460 non-null   object 
 28  ExterCond      1460 non-null   object 
 29  Foundation     1460 non-null   object 
 30  BsmtQual       1423 non-null   object 
 31  BsmtCond       1423 non-null   object 
 32  BsmtExposure   1422 non-null   object 
 33  BsmtFinType1   1423 non-null   object 
 34  BsmtFinSF1     1460 non-null   int64  
 35  BsmtFinType2   1422 non-null   object 
 36  BsmtFinSF2     1460 non-null   int64  
 37  BsmtUnfSF      1460 non-null   int64  
 38  TotalBsmtSF    1460 non-null   int64  
 39  Heating        1460 non-null   object 
 40  HeatingQC      1460 non-null   object 
 41  CentralAir     1460 non-null   object 
 42  Electrical     1459 non-null   object 
 43  1stFlrSF       1460 non-null   int64  
 44  2ndFlrSF       1460 non-null   int64  
 45  LowQualFinSF   1460 non-null   int64  
 46  GrLivArea      1460 non-null   int64  
 47  BsmtFullBath   1460 non-null   int64  
 48  BsmtHalfBath   1460 non-null   int64  
 49  FullBath       1460 non-null   int64  
 50  HalfBath       1460 non-null   int64  
 51  BedroomAbvGr   1460 non-null   int64  
 52  KitchenAbvGr   1460 non-null   int64  
 53  KitchenQual    1460 non-null   object 
 54  TotRmsAbvGrd   1460 non-null   int64  
 55  Functional     1460 non-null   object 
 56  Fireplaces     1460 non-null   int64  
 57  FireplaceQu    770 non-null    object 
 58  GarageType     1379 non-null   object 
 59  GarageYrBlt    1379 non-null   float64
 60  GarageFinish   1379 non-null   object 
 61  GarageCars     1460 non-null   int64  
 62  GarageArea     1460 non-null   int64  
 63  GarageQual     1379 non-null   object 
 64  GarageCond     1379 non-null   object 
 65  PavedDrive     1460 non-null   object 
 66  WoodDeckSF     1460 non-null   int64  
 67  OpenPorchSF    1460 non-null   int64  
 68  EnclosedPorch  1460 non-null   int64  
 69  3SsnPorch      1460 non-null   int64  
 70  ScreenPorch    1460 non-null   int64  
 71  PoolArea       1460 non-null   int64  
 72  PoolQC         7 non-null      object 
 73  Fence          281 non-null    object 
 74  MiscFeature    54 non-null     object 
 75  MiscVal        1460 non-null   int64  
 76  MoSold         1460 non-null   int64  
 77  YrSold         1460 non-null   int64  
 78  SaleType       1460 non-null   object 
 79  SaleCondition  1460 non-null   object 
 80  SalePrice      1460 non-null   int64  
dtypes: float64(3), int64(35), object(43)
memory usage: 924.0+ KB
```

Nếu tính cả biến độc lập, thì có 80 biến được cung cấp bởi bộ dữ liệu định giá nhà ở. Để đơn giản, ta sẽ lựa chọn một số biến để tiến hành phân tích giá nhà. Các biến được lựa chọn là các biến sau:

Các biến độc lập định lượng đưa vào mô hình:
1. LotArea
2. WoodDeckSF
3. OpenPorchSF
4. 1stFlrSF
5. GrLivArea

Các biến định tính đưa vào mô hình:

1. MSSubClass
2. MSZoning
3. Neighborhood
4. Bedroom

### Xử lý dữ liệu biến định tính:

Biến định tính là loại biến thường gặp trong thực tế, nó mang thông tin về đặc điểm của một đối tượng nào đó. Ví dụ như giới tính thì có hai lựa chọn là Nam hoặc Nữ, hay như khu vực dân cư thì có thể phân ra thành khu vực trung tâm, hoặc khu vực ngoại ô. Rõ ràng là với giá nhà, thì khu vực cũng là một yếu tố quan trọng ảnh hưởng đến mức giá, vì vậy, chúng ta cần tìm cách để đưa các biến này vào mô hình để xử lý cùng với các biến định lượng khác.

Có hai loại biến định tính thường gặp, đó là biến định tính ngang hàng và biến định tính thứ bậc. Biến định tính ngang hàng khi mỗi phạm trù của biến định tính đó đều có ý nghĩa tương đương nhau, ví dụ như giới tính nam, nữ. Khu vực ngoại ô, trung tâm. Biến định tính có thứ bậc khi các phạm trù của nó có thể sắp xếp được. Ví dụ như đánh giá về ngôi nhà, thì ta có thể cho điểm dựa trên thang điểm, 5 là rất tốt cho đến 1 là rất tệ... Tuy các thông tin này ở dạng số, nhưng khi đưa trực tiếp các giá trị này vào mô hình thì sẽ dẫn đến sự không chính xác. Ví dụ như việc đánh giá về ngôi nhà theo thang điểm 5. 1 điểm là rất tệ, 2 điểm là tệ... Điều này có ý nghĩa rằng một ngôi nhà khi được đánh giá ở thang điểm 2, thì giá nhà sẽ tăng beta đơn vị so với ngôi nhà được đánh giá ở thang điểm 1. Trên thực tế thì khoảng cách của các mốc 1 -> 2 và 2 -> 3, 
3 -> 4... là rất lớn và không giống nhau.

Để phù hợp với loại đối tượng là các biến định tính, ta sử dụng khái niệm biến giả để làm việc. Ví dụ với đối tượng là giới tính, ta sử dụng hai biến giả với các thuộc tính sau:

NAM: = 1 nếu đối tượng là nam, bằng 0 với đối tượng là nữ.
NU: = 1 nếu đối tượng là nữ, bằng 0 với đối tượng là nam

Cách diễn giải biến định tính bên trên là phù hợp với thực tế, tuy nhiên gặp một vấn đề như sau:

Ở mọi quan sát, tổng giá trị NAM + NU = 1. Ta gặp hiện tượng đa cộng tuyến hoàn hảo giữa hai biến định tính vừa tạo. Để khắc phục hiện tượng trên, ta rút gọn đi một biến giả như sau:

GT: = 1 nếu đối tượng là NAM, = 0 nếu đối tượng là NU.

Mở rộng ra với biến định tính có nhiều phạm trù, ta sử dụng n-1 biến giả tương ứng với n-1 phạm trù có trong biến định tính.

Để tạo biến giả, ta thực hiện như sau:

```python
model_data = data[["SalePrice", "LotArea", "WoodDeckSF", "OpenPorchSF"
                    , "1stFlrSF", "GrLivArea", "MSSubClass", "MSZoning" 
                    , "Neighborhood", "BedroomAbvGr" ]]

model_data = pd.get_dummies(model_data
                            , prefix=["MSSubClass", "MSZoning", "Neighborhood", "BedroomAbvGr"]
                            , columns=["MSSubClass", "MSZoning", "Neighborhood", "BedroomAbvGr"]
                            , drop_first=False # True: Bỏ bớt định nghĩa đầu tiên của mỗi biến
                           )             
```

### Đưa dữ liệu vào mô hình

```python
# Xử lý dữ liệu đầu vào cho mô hình:
Y = model_data["SalePrice"]
X = model_data.loc[:, model_data.columns != "SalePrice"]
```

Tương tự như mô hình hồi quy đơn biến, ta sẽ sử dụng mô hình hồi quy không có hệ số chặn để training dữ liệu

```python
mod = sm.OLS(Y, X)
res = mod.fit()

print(res.summary())
```

Kết quả:

```
                                 OLS Regression Results                                
=======================================================================================
Dep. Variable:              SalePrice   R-squared (uncentered):                   0.967
Model:                            OLS   Adj. R-squared (uncentered):              0.965
Method:                 Least Squares   F-statistic:                              754.1
Date:                Sat, 24 Dec 2022   Prob (F-statistic):                        0.00
Time:                        13:38:00   Log-Likelihood:                         -17393.
No. Observations:                1460   AIC:                                  3.489e+04
Df Residuals:                    1406   BIC:                                  3.518e+04
Df Model:                          54                                                  
Covariance Type:            nonrobust                                                  
========================================================================================
                           coef    std err          t      P>|t|      [0.025      0.975]
----------------------------------------------------------------------------------------
LotArea                  0.3352      0.113      2.964      0.003       0.113       0.557
WoodDeckSF              37.8398      8.442      4.482      0.000      21.279      54.400
OpenPorchSF             41.9913     16.566      2.535      0.011       9.495      74.487
1stFlrSF                18.1581      6.725      2.700      0.007       4.966      31.351
GrLivArea               78.8298      5.876     13.416      0.000      67.303      90.356
MSSubClass_30        -2.296e+04   6066.904     -3.784      0.000   -3.49e+04   -1.11e+04
MSSubClass_40        -4679.8604    1.9e+04     -0.247      0.805   -4.19e+04    3.26e+04
MSSubClass_45        -1.383e+04   1.14e+04     -1.214      0.225   -3.62e+04    8512.291
MSSubClass_50        -2.413e+04   5402.419     -4.466      0.000   -3.47e+04   -1.35e+04
MSSubClass_60        -9725.4495   6043.228     -1.609      0.108   -2.16e+04    2129.264
MSSubClass_70         -2.41e+04   7628.928     -3.160      0.002   -3.91e+04   -9139.629
MSSubClass_75        -2.572e+04   1.19e+04     -2.158      0.031   -4.91e+04   -2340.265
MSSubClass_80        -2486.4143   5310.360     -0.468      0.640   -1.29e+04    7930.667
MSSubClass_85         8161.8295   8555.443      0.954      0.340   -8620.978    2.49e+04
MSSubClass_90        -3.783e+04   6151.515     -6.149      0.000   -4.99e+04   -2.58e+04
MSSubClass_120       -3.087e+04   5677.486     -5.438      0.000    -4.2e+04   -1.97e+04
MSSubClass_160       -5.398e+04   8448.902     -6.389      0.000   -7.06e+04   -3.74e+04
MSSubClass_180       -1.638e+04   1.52e+04     -1.076      0.282   -4.62e+04    1.35e+04
MSSubClass_190        -3.28e+04   8163.432     -4.018      0.000   -4.88e+04   -1.68e+04
MSZoning_FV           6.129e+04   1.49e+04      4.115      0.000    3.21e+04    9.05e+04
MSZoning_RH           5.499e+04   1.52e+04      3.618      0.000    2.52e+04    8.48e+04
MSZoning_RL           6.589e+04   1.14e+04      5.777      0.000    4.35e+04    8.83e+04
MSZoning_RM           7.026e+04   1.13e+04      6.201      0.000     4.8e+04    9.25e+04
Neighborhood_Blueste  -184.8903   2.85e+04     -0.006      0.995   -5.61e+04    5.57e+04
Neighborhood_BrDale  -9639.4105   1.49e+04     -0.648      0.517   -3.88e+04    1.95e+04
Neighborhood_BrkSide -3.085e+04   1.12e+04     -2.765      0.006   -5.27e+04   -8959.168
Neighborhood_ClearCr -1.618e+04   1.17e+04     -1.385      0.166   -3.91e+04    6737.365
Neighborhood_CollgCr -1454.0115   9477.212     -0.153      0.878      -2e+04    1.71e+04
Neighborhood_Crawfor  2917.4448   1.07e+04      0.272      0.786   -1.81e+04     2.4e+04
Neighborhood_Edwards  -4.62e+04   9912.186     -4.661      0.000   -6.56e+04   -2.68e+04
Neighborhood_Gilbert -9210.3699   1.01e+04     -0.910      0.363   -2.91e+04    1.06e+04
Neighborhood_IDOTRR  -3.454e+04   1.19e+04     -2.904      0.004   -5.79e+04   -1.12e+04
Neighborhood_MeadowV -3.544e+04   1.49e+04     -2.382      0.017   -6.46e+04   -6257.040
Neighborhood_Mitchel -2.404e+04   1.05e+04     -2.290      0.022   -4.46e+04   -3445.321
Neighborhood_NAmes    -3.55e+04   9441.568     -3.760      0.000    -5.4e+04    -1.7e+04
Neighborhood_NPkVill  7251.4613   1.54e+04      0.471      0.637   -2.29e+04    3.74e+04
Neighborhood_NWAmes  -2.971e+04   1.01e+04     -2.939      0.003   -4.95e+04   -9881.358
Neighborhood_NoRidge  5.073e+04    1.1e+04      4.610      0.000    2.91e+04    7.23e+04
Neighborhood_NridgHt  7.792e+04   9705.485      8.029      0.000    5.89e+04     9.7e+04
Neighborhood_OldTown -4.971e+04    1.1e+04     -4.511      0.000   -7.13e+04   -2.81e+04
Neighborhood_SWISU   -4.557e+04   1.25e+04     -3.647      0.000   -7.01e+04   -2.11e+04
Neighborhood_Sawyer  -3.741e+04   9983.021     -3.747      0.000    -5.7e+04   -1.78e+04
Neighborhood_SawyerW -1.479e+04   1.02e+04     -1.454      0.146   -3.47e+04    5163.485
Neighborhood_Somerst  3.332e+04   1.22e+04      2.722      0.007    9307.127    5.73e+04
Neighborhood_StoneBr  7.971e+04   1.12e+04      7.138      0.000    5.78e+04    1.02e+05
Neighborhood_Timber   9745.7796    1.1e+04      0.885      0.377   -1.19e+04    3.14e+04
Neighborhood_Veenker  2.508e+04   1.39e+04      1.800      0.072   -2252.879    5.24e+04
BedroomAbvGr_1        1.365e+04   1.31e+04      1.043      0.297    -1.2e+04    3.93e+04
BedroomAbvGr_2       -1365.0682    1.2e+04     -0.114      0.909   -2.49e+04    2.22e+04
BedroomAbvGr_3       -1.141e+04   1.21e+04     -0.944      0.346   -3.51e+04    1.23e+04
BedroomAbvGr_4       -1.474e+04   1.26e+04     -1.174      0.241   -3.94e+04    9886.869
BedroomAbvGr_5       -5.168e+04   1.51e+04     -3.426      0.001   -8.13e+04   -2.21e+04
BedroomAbvGr_6       -3.705e+04   1.91e+04     -1.942      0.052   -7.45e+04     376.240
BedroomAbvGr_8       -7.866e+04   4.21e+04     -1.867      0.062   -1.61e+05    4006.998
==============================================================================
Omnibus:                      379.195   Durbin-Watson:                   1.960
Prob(Omnibus):                  0.000   Jarque-Bera (JB):            23989.995
Skew:                          -0.181   Prob(JB):                         0.00
Kurtosis:                      22.855   Cond. No.                     7.55e+05
==============================================================================

Notes:
[1] R² is computed without centering (uncentered) since the model does not contain a constant.
[2] Standard Errors assume that the covariance matrix of the errors is correctly specified.
[3] The condition number is large, 7.55e+05. This might indicate that there are
strong multicollinearity or other numerical problems.
```

### Giải thích kết quả hồi quy:

Vấn đề biến định tính:

Vì mô hình sử dụng là mô hình không có hệ số chặn nên ta sẽ vẫn lấy đầy đủ tất cả các giá trị của biến mà không cần loại bỏ. Biến định tính trong trường hợp này sẽ tác động đến hệ số chặn của mô hình (có thể đọc lại sách giáo trình để tìm hiểu kỹ hơn). 

Kết quả hồi quy:

R-squared (uncentered): 0.967

Hệ số R bình phương đã tăng lên đáng kể, tuy nhiên việc tăng lên của hệ số R bình phương có thể do tăng số lượng biến trong mô hình, nên chỉ số này không phải là một thước đo tốt để đánh giá mô hình có nhiều biến.

Mức ý nghĩa:

* Tất cả các biến định lượng đều có ý nghĩa với mô hình ở mức ý nghĩa trên 1%.
* Một số giá trị biến giả của biến định tính không có ý nghĩa với mô hình.

Hệ số hồi quy:

* Ngoài biến MSZoning mang ý nghĩa tích cực, góp phần làm tăng giá trị của ngôi nhà, còn lại hầu hết các giá trị của các biến giả khác đều góp phần làm giảm giá trị của ngôi nhà. Hiện tượng thú vị như sau: Các căn hộ có 1 phòng ngủ có giá bán cao hơn các căn hộ không phải là một phòng ngủ với giá trị khoảng 13650$ với các yếu tố khác không đổi. Điều này có thể do thị hiếu và nhu cầu của các khách hàng đối với căn hộ 1 phòng ngủ là cao hơn so với các loại căn hộ khác.

* Neighborhood cũng phân hóa một cách rõ rệt, điều này có ý nghĩa là một số vùng đất cụ thể có mức giá cao hơn trung bình, còn một số vùng đất khác thì lại có giá bán thấp hơn trung bình.
    * Tích cực:
        + Neighborhood_Somerst
        + Neighborhood_StoneBr
        + Neighborhood_Timber 
        + Neighborhood_Veenker
    * Tiêu cực:
        * Neighborhood_OldTown
        * Neighborhood_SWISU  
        * Neighborhood_Sawyer 
        * Neighborhood_SawyerW

Trên đây, tôi đã tiến hành việc hồi quy mô hình với phương pháp OLS và giải thích một số kết quả thu được. Để tối ưu mô hình và phục vụ việc dự báo giá nhà, tôi sẽ tiếp tục thực hiện trong bài viết sau. Việc xử lý kết quả, tối ưu mô hình là vô cùng quan trọng cũng như có nhiều phương pháp để thực hiện. Qua việc hồi quy, chúng ta đã có một số hình dung về bộ dữ liệu, và các kết quả được liên hệ đến bài toán thực tế, cũng như thực tế đã được phần nào phản ánh thông qua kết quả hồi quy trên.