---
layout: post
title: "Bài 1: Phương pháp tiếp cận Kinh tế lượng"
author: "codedaoneu"
tags: econometrics
---

Trong những năm gần đây, sự phát triển của các mô hình máy học, mô hình AI đã trở nên mạnh mẽ ở cả Việt Nam và trên thế giới. Các mô hình này ngày càng có tính ứng dụng cao cũng như ngày càng hoàn thiện hơn do sự phát triển của năng lực tính toán của máy tính, và sự nghiên cứu không ngừng nghỉ của cộng đồng và các chuyên gia. Tuy nhiên, với các bài toán kinh tế nói riêng, thì Kinh tế lượng, một cách tiếp cận có vẻ cổ điển vẫn có vai trò vô cùng quan trọng và vẫn đang tiếp tục đóng góp vai trò của mình trong ngành khoa học về kinh tế nói riêng. Loạt bài viết sau mong muốn sẽ đóng góp vào kho tài liệu chung của cộng đồng về cách tiếp cận của kinh tế lượng với các vấn đề kinh tế, khái niệm, các mô hình và sự khác biệt của Kinh tế lượng với các bài toán được giải quyết theo hướng tiếp cận Máy học, AI...

Loạt bài viết có các nội dung sau:

Bài 1: Các khái niệm về Kinh tế lượng, cách tiếp cận, và phương pháp luận.

Bài 2: Hồi quy đơn biến.

Bài 3: Hồi quy đa biến.

Bài 4: Kiểm định và lựa chọn mô hình.

....

Loạt bài viết sẽ được tiếp tục phát triển trong đó trọng tâm vào các lớp mô hình phân tích dữ liệu chuỗi thời gian, loại dữ liệu đang trở nên rất phổ biến hiện nay và các ứng dụng của nó.

Loạt bài viết tham khảo rất lớn từ Giáo trình Kinh tế lượng và kết hợp với một số tài liệu khác để làm sáng tỏ thêm vấn đề và ví dụ thực tế. Vì vậy, đây cũng có thể xem như tư liệu cô đọng lại kiến thức của Kinh tế lượng đã được học và các vấn đề băn khoăn trong việc làm việc với dữ liệu thực tế của mình. Trong quá trình biên soạn, ngoài kiến thức chính thống, tôi cũng có để lại các nhận định cá nhân của mình và cũng như không thể tránh khỏi sai sót, rất mong được sự góp ý từ phía các bạn đọc.

## Các khái niệm Kinh tế lượng

Dùng từ Các khái niệm về Kinh tế lượng, bởi vì chưa thực sự có một định nghĩa thống nhất, được mọi người cùng chấp nhận để định nghĩa về bộ môn này.

Một số các khái niệm phổ biến như:

- Kinh tế lượng bao gồm việc áp dụng thống kê toán cho các số liệu kinh tế để củng cố về mặt thực nghiệm cho các mô hình kinh tế do các nhà kinh tế đề xuất và tìm ra lời giải bằng số.

- Là sự phân tích về lượng các vấn đề kinh tế hiện thời dựa trên việc vận dụng đồng thời lý thuyết và thực tế được thực hiện bằng các phương pháp suy đoán thích hợp.

- Là một môn khoa học xã hội trong đó kết hợp các công cụ của lý thuyết kinh tế, toán học và suy diễn thống kế để phân tích các vấn đề kinh tế.

- Là một bộ phận của khoa học kinh tế, trong đó sử dụng các mô hình xác suất để giải thích các lý thuyết kinh tế được đề xuất.

Dựa trên một số định nghĩa trên, ta có thể đúc kết lại được, việc nghiên cứu kinh tế lượng không chỉ là các công cụ giúp đo lường, mà còn là cách mà nó đóng góp cho ngành khoa học kinh tế nói chung. Nó giúp chúng ta lượng hóa, đo lường, kiểm chứng các mô hình kinh tế sẵn có và mới bằng một bộ công cụ của mình đó là các mô hình xác suất, được kết hợp của toán học, xác suất và suy diễn thống kê. Tuy nhiên, Kinh tế lượng được thiết kế để phát huy vai trò của mình trong khoa học kinh tế, trong khi các bài toán ML, AI sau này tuy cũng dựa trên các mô hình xác suất, nhưng đã mở rộng phạm vi ứng dụng của mình ra rất nhiều lĩnh vực khác nhau như xử lý ngôn ngữ, ảnh, các công cụ có trí thông minh nhân tạo.....

Để hiểu và vận dụng tốt được Kinh tế lượng, chúng ta cần có hiểu biết nhất định về các mô hình kinh tế, nó sẽ đóng vai trò quan trọng trong phương pháp luận của (Kinh tế lượng)KTL, cũng như giúp vận dụng vào thực tế một cách tốt nhất.

## Phương pháp luận của Kinh tế lượng

Phương pháp luận của KTL bao gồm 7 bước, vì đã có nhiều tài liệu đề cập nên tôi chỉ nêu vắn tắt như sau:
1. Nêu ra các giải thuyết.
2. Thiết lập mô hình.
3. Thu thập số liệu.
4. Ước lượng tham số.
5. Phân tích kết quả.
6. Dự báo.
7. Ra quyết định.

So với cách tiếp cận này, bằng kinh nghiệm của mình với dữ liệu tại các doanh nghiệp, tôi thấy một số điểm khác biệt như sau:

### Dữ liệu có trước, mô hình có sau

Trong một doanh nghiệp, dữ liệu thường được sinh ra trước bởi các hệ thống của mình, dữ liệu sau đó được lưu lại và tiến hành phân tích. Tức là việc sử dụng các giả thuyết và mô hình để lựa chọn dữ liệu sẽ dựa trên một bể dữ liệu có sẵn trong doanh nghiệp chứ không phải là thiết lập mô hình trước rồi mới đi thu thập số liệu.

### Nêu ra các giả thuyết

Với các vấn đề kinh tế vĩ mô, lĩnh vực đã được con người nghiên cứu trong hàng trăm năm, thì việc đưa ra các giả thuyết là khá dễ dàng, ví dụ nó giúp giải thích quy luật hoặc dự báo khi có một thay đổi trong nền kinh tế vĩ mô...
Tuy nhiên, mỗi doanh nghiệp lại có một vấn đề khác nhau, vấn đề này thường rất khó xác định cũng như kinh nghiệm của một doanh nghiệp cũng không thể áp dụng cho các doanh nghiệp khác, vì vậy việc đưa ra các giả thuyết là hết sức khó khăn. Cách tiếp cận thường thấy của các doanh nghiệp đó là tiếp cận dựa trên vấn đề, mỗi khi lãnh đạo doanh nghiệp hoặc các phòng ban, thông qua quá trình hoạt động hoặc quan sát số liệu, nhận ra một vấn đề nào đó thì mới bắt tay vào sử dụng các phương pháp khác nhau để tìm hiểu cũng như cố gắng giải thích và tìm ra phương pháp. Sẽ có các công cụ và mô hình giúp doanh nghiệp nhận ra các vấn đề này nhưng nhìn chung chúng đều mang tinh đặc trưng cho từng doanh nghiệp cụ thể, vì vậy hướng tiếp cận theo cách nêu ra các giả thuyết sẽ được điều chỉnh lại để phù hợp với tình hình thực tế hơn là các vấn đề khuôn mẫu.

### Dự báo

Một lớp bài toán quan trọng trong doanh nghiệp ngày nay là dự báo một vấn đề, ví dụ như dự báo về doanh thu công ty. Cách làm phổ biến hiện tại là dựa vào kinh nghiệm và "bốc thuốc" một con số. Cách làm này đôi khi tỏ ra rất hiệu quả và không cần các mô hình kinh tế phức tạp. Tuy nhiên đối với các đánh giá khó hơn, thì niềm tin của lãnh đạo vào các con số của mô hình dường như chưa đủ lớn vì các sai lệch dự báo. Điều này có thể do cách tiếp cận, xây dựng mô hình chưa thực sự hiệu quả và cần điều chỉnh thêm. Hoặc do các cú sốc không lường trước của các yếu tố bên ngoài, do đó cần sự nhanh nhạy trong việc ra quyết định dựa trên kinh nghiệm và các thông tin bên ngoài khác mà chưa xem xét đánh giá tác động dựa trên các mô hình, đây cũng là điều cần tối ưu trong tương lai.

### Phạm vi của bài toán.

Như đã nói bên trên, các lớp bài toán Kinh tế lượng cần sự hỗ trợ của các lý thuyết và mô hình kinh tế làm nền tảng và để kiểm chứng. Trong khi bài toán của các doanh nghiệp hiện tại không chỉ là các bài toán mẫu mà còn là vô vàn vấn đề của doanh nghiệp trên con đường phát triển. Khi không có sự hỗ trợ của các lý thuyết và mô hình cần thiết, KTL dường như bị thiếu căn cứ để có thể giải thích một cách tường minh các quan hệ dữ liệu trong doanh nghiệp. Hiện tại, các bài toán học máy, AI chủ yếu phục vụ cho các yêu cầu về dự đoán, dự báo, việc giải thích các dữ liệu trong doanh nghiệp để có thể hiểu hơn đang ít có chỗ đứng hơn vì các ứng dụng của AI, máy học đang trở nên thiết thực hơn bao giờ hết. Tuy nhiên việc hiểu dữ liệu của doanh nghiệp, nhận diện được các mối quan hệ thực tế, hay chỉ là mối quan hệ về mặt thống kê cũng là hết sức quan trọng để người lãnh đạo có thể ra quyết định một cách chính xác và hiệu quả hơn.

### Vấn đề về dữ liệu.

Dữ liệu trong doanh nghiệp, do lịch sử phát triển qua nhiều giai đoạn với nhiều người phát triển khác nhau đã trở nên lỗi thời hoặc thậm trí lỗi qua thời gian. Việc hiểu được dữ liệu trong doanh nghiệp là một thách thức và yêu cầu về thời gian cho việc này chiếm một chi phí rất lớn của người làm dữ liệu, điều này yêu cầu người làm dữ liệu phải thực sự hiểu dữ liệu của doanh nghiệp, hay rộng hơn là hiểu về doanh nghiệp, cấu trúc, quy trình kinh doanh, quy trình phát sinh dữ liệu trong doanh nghiệp như thế nào để kịp thời điều chỉnh sai sót cũng như phân tích một cách chính xác dữ liệu sẵn có trong doanh nghiệp, hoặc có thể tư vấn để tạo ra các dữ liệu mới phục vụ cho các bài toán phân tích của mình.

## Phân loại dữ liệu

Phân loại theo kiểu dữ liệu:
1. Dữ liệu chéo: Là dữ liệu về một hay nhiều tính chất của nhiều chủ thể khác nhau.
2. Dữ liệu chuỗi thời gian: Là dữ liệu về trạng thái của một chủ thể qua nhiều mốc thời gian khác nhau.
3. Số liệu hỗn hợp: kết hợp hai kiểu dữ liệu trên.

Phân loại theo tính chất dữ liệu:
1. Dữ liệu định tính: Các thuộc tính đặc trưng của đối tượng.
2. Dữ liệu định lượng: Được thể hiện bằng các con số, có thể thực hiện các phép tính lên loại dữ liệu này.

Phân loại theo nguồn phát sinh dữ liệu:
1. Dữ liệu sơ cấp (dữ liệu thô): Dữ liệu chưa qua xử lý
2. Dữ liệu thứ cấp: Dữ liệu đã được tổng hợp, phát sinh trên dữ liệu so cấp.

Phân loại theo nguồn gôc số liệu:
1. Dữ liệu thực nghiệm: Được tạo ra bằng cách kiểm soát một cách nhân tạo các yếu tố chi phối lên dữ liệu đó. Ví dụ, người ta kiểm soát chất lượng của một giống cây bằng cách sử dụng chế độ nước, phân bón khác nhau và lưu lại kết quả để đánh giá.
2. Dữ liệu phi thực nghiệm: Khi không thể kiểm soát được các yếu tố chi phối lên dữ liệu, đây được gọi là dữ liệu phi thực nghiệm. Ví dụ như ta không thể kiểm soát được tỷ lệ lạm phát bằng việc thử nghiệm tăng cung tiền ở nhiều quy mô khác nhau. Điều này là phi lý và không thể diễn ra trên thực tế.

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








