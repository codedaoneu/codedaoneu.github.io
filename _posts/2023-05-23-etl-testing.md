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

