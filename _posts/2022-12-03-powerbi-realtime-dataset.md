---
layout: post
title: "Tạo dataset realtime với PowerBI"
author: "codedaoneu"
tags: powerbi
---

# Real-time Streaming với PowerBI

PowerBI cùng với phương thức truyền dữ liệu thời gian thực (real-time) của mình là một tính năng vô cùng hữu ích để giải quyết các nhu cầu về việc xem báo cáo thời gian thực. Hơn thế nữa, PowerBI cũng hỗ trợ việc phân tích ngay trên bộ dữ liệu được truyền tải real-time này.

## PowerBI report & PowerBI Dashboard

Thông thường, khi tiếp cận powerbi, ban đầu chúng ta sẽ tiếp cận theo flow chuẩn như sau:

1. Kết nối với dữ liệu ở source, thường là các relational database, đó có thể được quy định là datawarehouse của công ty, hoặc là các datamart... tùy theo mô hình tổ chức của từng công ty. Tuy nhiên các mô hình datawarehouse này thường là dữ liệu được tổ chức và được làm mới định kỳ (batch), thông thường là daily, còn với các dữ liệu tổng hợp ở mức độ cao thì đó có thể là tuần, tháng, quý....
2. Đẩy dữ liệu vào PowerBI để tạo thành PowerBI dataset. 
3. Thực hiện việc định nghĩa và nối các quan hệ trong PowerBI model.
4. Tạo các báo cáo, Dashboard dựa trên bộ dữ liệu đã chuẩn bị sau đó publish nó lên các workspace để các end-user có thể sử dụng.

Đặc điểm của dataset khi ta tiếp cận theo hướng này là dataset sau khi được publish lên Powerbi Web service thì dữ liệu sẽ được làm mới định kỳ hàng ngày, chúng ta cũng có thể làm mới nó thường xuyên hơn bằng việc setup thời gian làm mới dữ liệu, hoặc người dùng cũng có thể tự làm mới dữ liệu trong dataset một cách thủ công. Cơ chế của việc làm mới này như sau:

PowerBI sẽ gửi một truy vấn dữ liệu đến source dữ liệu thông qua một gateway, điều này cho phép dữ liệu được truyền tải và lưu tại bộ nhớ của dataset PowerBI. Sau đó, dữ liệu sẽ được làm mới trên các report, dashboard.

Để dữ liệu được làm mới thường xuyên hơn, ta sẽ phải gửi truy vấn đến source một cách thường xuyên hơn. Điều này sẽ làm phát sinh rất nhiều vấn đề, và nói chung, nó không phải thực sự là dữ liệu real-time.

Để khắc phục vấn đề này, PowerBI đưa ra một giải pháp hoàn toàn khác với một cơ chế tiếp cận cũng hoàn toàn khác với các bước đã được nêu ở bên trên.

## Cơ chế real-time sử dụng API.

Có 3 phương thức truyền tải dữ liệu real-time với PowerBI.

+ Push Dataset
+ Streaming Dataset
+ PubNub streaming Dataset

Cả ba phương thức này đều dùng API để truyền tải dữ liệu realtime lên PowerBI. Điểm khác biệt chính ở đây là khả năng lưu trữ dữ liệu của từng phương thức. Push Dataset sẽ lưu dữ liệu tại một database riêng được tạo ra tự động trên PowerBI Web Service và có khả năng lưu trữ nhất định. Trong khi 2 phương thức tiếp theo chỉ lưu dữ liệu tại một bộ nhớ đệm và sẽ tự động xóa trong vòng 1h.
Các phương thức này đều có các hạn chế và giới hạn nhất định, để tìm hiểu rõ hơn, chúng ta có thể xem các thông số quy định về API trên trang chủ của microsoft.

Ta sẽ tìm hiểu kỹ hơn phương thức thứ nhất - Push Dataset

Dữ liệu sẽ được đẩy lên PowerBI service. Sau khi dữ liệu được tạo, PowerBI service sẽ tự động tạo ra một database để lưu trữ tất cả dữ liệu được đẩy lên. Bởi vì đây thực sự là một database được tạo ra, nên nó sẽ có khả năng tiếp tục lưu trữ dữ liệu. Chúng ta sẽ có thể sử dụng chính dữ liệu này để tạo ra các visual, báo cáo, dashboard. Ngoài ra, dataset này cũng có thể được tiếp cận như phương thức cơ bản như đã đề cập ở phần đầu tiên, chúng ta có thể xem nó như một source dữ liệu và kết nối & kết hợp với các nguồn dữ liệu khác để tạo ra một báo cáo cực kỳ mạnh mẽ. Đó là các Báo cáo phân tích theo thời gian thực.

## Các bước tạo một real-time report với PowerBI

Cách tiếp cận và các bước thực hiện như sau:

1. Tạo một streaming dataset.
2. Bật chức năng lưu dữ liệu lịch sử của streaming dataset
3. Tạo một công cụ để đẩy dữ liệu lên dataset đã được tạo
4. Có thể kết hợp dữ liệu của dataset được tạo này với cơ sở dữ liệu có sẵn để tạo thành powerbi real-time model.
5. Tạo Dashboard, Report dựa trên dataset đã được tạo.

### Bước 1: Tạo một streaming dataset

Trong workspace, chọn tạo mới **Streaming Dataset** -> Chọn tiếp **API**

![ảnh 1](https://github.com/codedaoneu/codedaoneu.github.io/blob/master/images/2022-12-03-powerbi-realtime-dataset_01.png?raw=true)

Thực hiện tiếp các thao tác đặt tên, và định nghĩa các trường dữ liệu cho bộ dataset.

![ảnh 2](https://github.com/codedaoneu/codedaoneu.github.io/blob/master/images/2022-12-03-powerbi-realtime-dataset_02.png?raw=true)

Tiếp tục bật chức năng lưu dữ liệu lịch sử. Việc này sẽ giúp lưu lại dữ liệu trong database của PowerBI service, chúng ta có thể sử dụng dữ liệu ở đây như một source dữ liệu độc lập để xây dựng các báo cáo khác nhau.

![ảnh 3](https://github.com/codedaoneu/codedaoneu.github.io/blob/master/images/2022-12-03-powerbi-realtime-dataset_03.png?raw=true)

Ấn tạo dataset.

### Bước 3: Tạo một công cụ để đẩy dữ liệu theo thời gian thực nên dataset.

Đến bước này, chúng ta cần sự hỗ trợ của đội ngũ developer trong team để có thể đẩy dữ liệu liên tục lên API của PowerBI. Khi mới tạo API, database được tạo và đó là một dataset rỗng, dữ liệu sẽ được đẩy liên tục lên API và sẽ được lưu lại trong database. Việc này tùy thuộc vào công nghệ mà team bạn đang sử dụng, nói chung thì vấn đề này không phải là việc quá phức tạp về mặt kỹ thuật, tuy nhiên việc đưa dữ liệu gì lên là điều cần phải định nghĩa hết sức kỹ lưỡng trước khi triển khai một dataset thực tế.

### Bước 4: Tạo một báo cáo kết hợp với nguồn dữ liệu khác

Tạo một report mới, trong đó lấy dữ liệu từ API đã được tạo. Lưu ý là ta phải đăng nhập vào tài khoản có quyền truy cập vào API vừa được tạo. 

![ảnh 4](https://github.com/codedaoneu/codedaoneu.github.io/blob/master/images/2022-12-03-powerbi-realtime-dataset_04.jpg?raw=true)

Đưa thêm dữ liệu từ các nguồn dữ liệu khác để tạo thành dataset, tiếp tục nối quan hệ giữa các bảng trong source dữ liệu để tạo thành model hoàn chỉnh

![ảnh 5](https://github.com/codedaoneu/codedaoneu.github.io/blob/master/images/2022-12-03-powerbi-realtime-dataset_05.png?raw=true)

Thực hiện tính toán bằng các hàm dax với dữ liệu đã được đưa vào model hoàn chỉnh sau đó publish báo cáo hoàn chỉnh lên PowerBI Service và tạo các Dashboard với các visual đã được tạo, hoặc chúng ta có thể trực tiếp tạo các biểu đồ cho bộ dữ liệu real-time trên Dashboard

![ảnh 6](https://github.com/codedaoneu/codedaoneu.github.io/blob/master/images/2022-12-03-powerbi-realtime-dataset_06.png?raw=true)

### Lời kết:

Như vậy chúng ta đã hoàn thành việc tạo một bộ dữ liệu thời gian thực với một phương pháp tiếp cận hoàn toàn khác với cách xây dựng báo cáo trước đây. Việc này mở rộng phạm vi sử dụng và các bài toán có thể giải quyết với PowerBI theo một cách mới và rộng hơn trước rất nhiều. Việc tính toán real-time mang lại sức mạnh to lớn trong việc theo dõi hàng ngày, hàng giờ và nhận biết vấn đề nhanh chóng. Tuy nhiên, khi triển khai thực tế, các vấn đề về giới hạn kỹ thuật của PowerBI là không hề ít, đòi hỏi người thực hiện phải hiểu rõ được yêu cầu của bài toán, chọn giải pháp xử lý hợp lý trước khi đi vào triển khai thực tế. Ví dụ về việc đưa dữ liệu để đẩy lên API của PowerBI, nếu chúng ta đưa dữ liệu lên một cách quá chi tiết, điều này dẫn đến một khối lượng dữ liệu khổng lồ sẽ được tải lên và việc tính toán, tuy đa năng hơn, nhưng sẽ rất nhanh sẽ gặp giới hạn về mặt kỹ thuật với thông số số lượng dòng tối đa được lưu trữ trong PowerBI Service. Điều này cần cả người làm giải pháp và người triển khai thực tế phải đánh giá được cả về phương pháp tiếp cận, đề bài, tính khả thi và các tính huống thực tế có thể gặp phải để triển khai thành công báo cáo PowerBI theo phương thức tiếp cận này.

