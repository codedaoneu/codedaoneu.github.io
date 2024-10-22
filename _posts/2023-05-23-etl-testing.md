---
layout: post
title: "ETL Testing"
author: "codedaoneu"
tags: tutorial
---

Sau khi chuyển dữ liêu đến một nơi lưu trữ và theo một cấu trúc khác, đặc biệt là một nơi
mang nhiều logic như data warehouse hay datamart, việc kiểm tra lại dữ liệu
là một điều hết sức quan trọng và cần thiết. Bài viết này tôi muốn giới thiệu
một số tiêu chuẩn để kiểm định dữ liệu sau quá trình ETL. Bài viết có tham khảo
một số nguồn tư liệu, tôi sẽ để trích dẫn dưới cuối bài.

## ETL Testing

ETL testing là một quá trình được thiết kế để đảm bảo việc ETL dữ liệu từ source
vào các nơi chứa dữ liệu như warehouse, mart một cách chính xác.
Trong quá trình ETL, người ta thường đưa vào đó nhiều logic business, clean data
hoặc chuyển đổi giữa nhiều cơ sở dữ liệu khác nhau, việc testing dữ liệu sẽ
đảm bảo tính chính xác theo các quy tắc mà người tổ chức dữ liệu và người thực
hiện ETL đã thống nhất từ trước để tránh các lỗi phát sinh trong quá trình
thực hiện. Việc testing ETL còn đảm bảo sự ổn định trong quá trình vận hành
dữ liệu khi các case về dữ liệu đã được định nghĩa sẵn và có thể tham chiếu đến
mỗi khi có lỗi phát sinh. Ngoài ra, khi rule business ở source thay đổi có thể
dẫn đến sai lệch trong dữ liệu, việc có một bộ rule được định nghĩa trước là điều
cần thiết để đánh giá lại mức độ ảnh huởng và có phương án xử lý thích hợp.

### ETL Testing
ETL Testing là việc kiểm tra dữ liệu sau quá trình ETL.
ETL Testing là việc cần thiết phải làm để so sánh mức độ chính xác của dữ liệu được tổ chức vào warehouse so với ở source. ETL Testing được thực hiện khi diễn ra bước transform dữ liệu so với source và load vào trong warehouse.
Do trong quá trình ETL cần phải áp dụng nhiều logic và trải qua nhiều bước khác nhau, nên điều quan trọng là tất cả những bước trên đều phải giữ gìn sự chính xác của dữ liệu từ input là source đến output là warehouse.
Ngoài ra, cần kiểm tra việc thực hiện áp dụng các logic được nghiệp vụ cài đặt trong quá trình ETL xem có chính xác so với kỳ vọng chưa.
- Sự khác biệt của việc test dữ liệu ETL so với test phần mềm.
Thay vì test các tính năng, sự vận hành của phần mềm. Tesing quá trình ETL không trọng tâm vào việc test tool ETL mà trọng tâm test vào dữ liệu mà nó trả ra trong cả quá trình ETL.
Phương pháp tiếp cận ở đây được gọi là data centric tesing approach.
- Một số thách thức trong quá trình testing dữ liệu ETL:
 Khối lượng dữ liệu ETL là rất lớn, có thể lên đến hàng triệu bản ghi. Việc test dữ liệu cần phải cover được tất cả khối lượng dữ liệu này.
 Sự không đồng nhất về database giữa source và warehouse, dẫn đến các lỗi phát sinh trong quá trình chuyển đổi. 
 Thường xuyên phải áp dụng các logic phức tạp lên dữ liệu trong quá trình ETL (complex query)
 Rất phụ thuộc vào các kịch bản dữ liệu có sẵn và sự sẵn có của dữ liệu thật trong quá trình test dữ liệu.

### Template file test data thống nhất:

| **Group Test** | **Case dữ liệu cần test** | **Dữ liệu test đầu vào** | **Kết quả kỳ vọng** | **Status** | **Kết quả thực tế** | **Assignee** | **Note** | **** | **** |
|:--------------:|:-------------------------:|:------------------------:|:-------------------:|:----------:|:-------------------:|:------------:|:--------:|:----:|:----:|
| Cấu trúc bảng  |                           |                          |                     |            |                     |              |          |      |      |
| Cấu trúc bảng  |                           |                          |                     |            |                     |              |          |      |      |
| Cấu trúc bảng  |                           |                          |                     |            |                     |              |          |      |      |
| Cấu trúc bảng  |                           |                          |                     |            |                     |              |          |      |      |
| Cấu trúc bảng  |                           |                          |                     |            |                     |              |          |      |      |
| Data testing   |                           |                          |                     |            |                     |              |          |      |      |
| Data testing   |                           |                          |                     |            |                     |              |          |      |      |
| Data testing   |                           |                          |                     |            |                     |              |          |      |      |
|                |                           |                          |                     |            |                     |              |          |      |      |


| **Type of Bugs**           | **Mô tả**                                                                        |
|:--------------------------:|:--------------------------------------------------------------------------------:|
| User interface bugs        | Lỗi tương tác với người dùng, với database, chủ yếu là lỗi chính tả, lỗi font... |
| Input and Output bugs      | Lỗi dữ liệu không chính xác giữa input và output                                 |
| Calculation and logic bugs | Lỗi logic hoặc tính toán không đúng so với kỳ vọng                               |
| Load Condition bugs        | Dữ liệu vào trong warehouse không đúng so với kỳ vọng                            |
| System interrupts bugs     | Hệ thống bị treo hoặc lâu hơn so với kỳ vọng                                     |
| Design bugs                | Cấu trúc dữ liệu không đúng so với tài liệu thiết kế                             

### Mô hình Test dữ liệu ETL đề xuất:

| **ETL Testing Categories** | **Group Testing** | **Case**          | **Base data**                      | **Detail**                                                             | **Type of Bug** |
|:--------------------------:|:-----------------:|:-----------------:|:----------------------------------:|:----------------------------------------------------------------------:|:---------------:|
| Metadata Testing           | Cấu trúc bảng     | Column Name check | Data model File (data design file) | Kiểm tra các bảng đích của quá trình ETL so với thiết kế đã thống nhất | Design bugs     |

| **Metadata Testing**        | **Cấu trúc bảng** | **Table Name check**                                 | **Data model File (data design file)** | **Kiểm tra các bảng đích của quá trình ETL so với thiết kế đã thống nhất**                                                                                                            | **Design bugs**            |
|:---------------------------:|:-----------------:|:----------------------------------------------------:|:--------------------------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------------------------:|
| Metadata Testing            |                   | Schema Name check                                    | Data model File (data design file)     | Kiểm tra các bảng đích của quá trình ETL so với thiết kế đã thống nhất                                                                                                                | Design bugs                |
| Metadata Testing            | Cấu trúc bảng     | Data Type Check                                      | Data model File (data design file)     | Kiểm tra kiểu dữ liệu của đối tượng là bảng, cột so với file thiết kế                                                                                                                 | Design bugs                |
| Metadata Testing            | Cấu trúc bảng     | Data Length Check                                    | Data model File (data design file)     | Kiểm tra length của dữ liệu trong cột so với length định nghĩa trong file thiết kế                                                                                                    | Design bugs                |
| Metadata Testing            | Cấu trúc bảng     | Data Index Check                                     | Data model File (data design file)     | Kiểm tra index của dữ liệu trong bảng so với file thiết kế                                                                                                                            | Design bugs                |
| Metadata Testing            | Cấu trúc bảng     | Constraint Check                                     | Data model File (data design file)     | Kiểm tra các ràng buộc của bảng, cột, dữ liệu trong cột so với file thiết kế                                                                                                          | Design bugs                |
| Metadata Testing            | Cấu trúc bảng     | Constraint Check - Null value                        | Target table                           | Kiểm tra các trường được định nghĩa là not null                                                                                                                                       | Design bugs                |
| Metadata Testing            | Cấu trúc bảng     | Constraint Check - tham chiếu khóa chính, khóa ngoại | Target table                           | Kiểm tra các khóa ngoại trong bảng đã được tham chiếu đến khóa chính của đúng bảng hay chưa                                                                                           | Design bugs                |
| Metadata Testing            | Cấu trúc bảng     | Metadata Check Across Environments                   | Data model File (data design file)     | Check chéo với môi trường ở source, lake xem có đảm bảo về mặt lưu trữ không, tránh hiện tượng tràn dữ liệu                                                                           | Design bugs                |
| Data Completeness Testing   | Cấu trúc bảng     | Record Count Validation                              | Source                                 | So sánh số lượng bản ghi ở source được etl vào warehouse                                                                                                                              | Load Condition bugs        |
| Data Completeness Testing   | Data testing      | Column Data Profile Validation                       | Source                                 | Checksum các cột dữ liệu trong warehouse và source, so sánh tổng các chỉ tiêu                                                                                                         | Load Condition bugs        |
| Data Completeness Testing   | Data testing      | Compare Entire Source and Target Data                | Source                                 | So sánh value các trường mô tả ở source và warehouse xem có khớp không                                                                                                                | Input and Output bugs      |
| Data Quality Testing        | Data testing      | Duplicate Data Checks                                | Target table                           | Kiểm tra logic duplicate dữ liệu trong bảng đích                                                                                                                                      | Calculation and logic bugs |
| Data Quality Testing        |                   | Data Integrity Checks                                | Target table                           | Kiểm tra các ràng buộc như null, fk tham chiếu pk, và các ràng buộc khác trong warehouse                                                                                              | Calculation and logic bugs |
| Data Quality Testing        | Data testing      | Data Validation Rules                                | Target table                           | Kiểm tra các logic được định nghĩa chi tiết trong từng trường dữ liệu                                                                                                                 | Calculation and logic bugs |
| Data Quality Testing        | Data testing      | Spelling mistakes                                    | Target table                           | Kiểm tra Loỗi chính tả, lỗi font nếu có trong dữ liệu ở bảng đích                                                                                                                     | User interface bugs        |
| Data Transformation Testing | Data testing      | Transformation testing using the White Box approach  | Target table                           | Kiểm tra số lượng change detect được trong ngày bất kỳ thực hiện ETL tại các thao tác insert/update/delete                                                                            | Load Condition bugs        |
| Data Transformation Testing | Data testing      | Transformation testing using the Black Box approach  | Target table                           | Kiểm tra chi tiết các event change trong ngày ETL bất kỳ. Các thông tin được insert/update/delete                                                                                     | Load Condition bugs        |
| Incremental ETL Testing     | Data testing      | Slowly Changing Dimension Checks                     |                                        | Kiểm tra các thay đổi thông tin ở source và ghi nhận của các bảng dim trong warehosue theo các phương pháp SCD                                                                        | Load Condition bugs        |
| ETL Integration Testing     | Data testing      | End-to-End Data Testing                              | Target table                           | Kiểm tra logic của các bản ghi trong bảng dim theo phương pháp SCD. Valid, end_date, eff_date, uniquie                                                                                | Input and Output bugs      |
| ETL Performance Testing     | Data testing      | End-to-End Data Testing                              | Source - Target                        | Kiểm tra một tập dữ liệu ở source và so sánh với dữ liệu cuối cùng được ghi nhận ở warehouse xem có giống nhau không. Có thể kiểm tra một tập dữ liệu hoặc tốt hơn là toàn bộ dữ liệu | System interrupts bugs     |

Riêng phần Reference Data Testing, Incremental ETL Testing đã trùng với các phần test logic trước nên không đưa vào danh mục cần check.
- Các bước thực hiện test dữ liệu
 
 | **STT** | **Stages**                                    | **Detail**                                                                                                                                         | **Output**                                                                                  |
|:-------:|:---------------------------------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------:|:-------------------------------------------------------------------------------------------:|
| 1       | Làm rõ yêu cầu về mặt business của dữ liệu    | Thường thì trong file thiết kế đã định nghĩa rõ dữ liệu và logic cần thiết                                                                         | Design files                                                                                |
| 2       | Kiểm tra dữ liệu ở source                     | Kiểm tra các logic của dữ liệu trong source để phân biệt các lỗi mắc phải do quá trình ETL và các lỗi mắc phải do dữ liệu ở source chưa chính xác. | Source desc (hoặc kiểm tra trong lake)                                                      |
| 3       | Thiết kế test case                            | - Thiết kế các kịch bản dữ liệu                                                                                                                    | File test case chi tiết                                                                     |
| 4       | Báo cáo tổng quan dữ liệu ETL                 | - Tạo các query cần thiết                                                                                                                          | Kiểm tra các logic tổng quan và performance của hệ thống ETL                                |
| 5       | Test dữ liệu                                  | - Định nghĩa các rule transform dữ liệu                                                                                                            | File kết quả test dữ liệu                                                                   |
| 6       | Báo cáo kết quả test và tạo yêu cầu chỉnh sửa | Đánh giá tổng quan dữ liệu ETL và luồng ETL dữ liệu đã tạo                                                                                         | jira nếu có lỗi. Chu trình được lặp lại đến bước 5 ở bước test dữ liệu sau khi dev fix xong |

### Link tham khảo:

https://www.guru99.com/utlimate-guide-etl-datawarehouse-testing.html 
https://www.datagaps.com/data-testing-concepts/etl-testing/ 
https://www.datagaps.com/data-testing-concepts/etl-testing/ 
https://hevodata.com/learn/etl-testing/