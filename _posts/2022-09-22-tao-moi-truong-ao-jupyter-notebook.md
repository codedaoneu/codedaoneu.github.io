---
layout: post
title: "Tạo môi trường ảo và khởi chạy trên Jupyter Notebook"
author: "codedaoneu"
tags: begin
---

# Tạo môi trường ảo và khởi chạy trên Jupyter Notebook

Trong quá trình phát triển một cách song song các dự án khác nhau, việc tạo các môi trường độc lập để phát triển và thử nghiệm một cách đồng thời là việc hết sức cấp thiết. 

## Tại sao lại là môi trường ảo?

Python, cũng giống các ngôn ngữ khác, đều có cách tải và quản lý các thư viện theo cách riêng. Mặc đinh, Python quản lý các gói cài đặt của mình trong một thư mục gốc - được gọi là môi trường **base**, hay môi trường **thật** trên máy local của bạn theo cơ chế đường dẫn mặc định. Tức là khi không có cấu hình bổ sung gì thêm, thì khi cài đặt và gọi một thư viện bất kỳ, thì gói thư viện đó sẽ được cài đặt vào đúng đường dẫn mặc định của python, và khi gọi thư viện đó ra để sử dụng thì đường dẫn mà nó tự động đọc cũng chính là đường dẫn mặc định khi gói thư viện đó được cài.
Ví dụ với gói numpy.

```python
import numpy as np
print(np.__file__)

'/usr/local/lib/python3.9/site-packages/numpy/__init__.py'
```

Đây là đường dẫn mặc định mà python đã sử dụng để cài gói thư viện vào máy local của bạn, đây cũng chính là đường dẫn **base** mà khi import thư viện để sử dụng, python sẽ gọi vào để lấy gói cần thiết.

Một ví dụ kinh điển là khi phát triển đồng thời hai dự án sử dụng chung một thư viện, ví dụ là tensoflow. Một dự án đang được phát triển sử dụng phiên bản 1.5, dự án còn lại sử dụng tensoflow 2. Vấn đề xuất hiện ở đây là Python không thể dựa vào phiên bản để quản lý đường dẫn được. Như vậy, khi cài đặt đồng thời hai gói tensoflow thì sẽ dẫn đến tình trạng trùng đường dẫn, dẫn đến việc không thể phát triển đồng thời nhiều dự án khác nhau.

Mục đích chính của việc tạo các môi trường ảo là để cô lập môi trường phát triển của từng dự án riêng lẻ. Khi đó môi trường phát triển của các dự án không còn phụ thuộc vào nhau và có thể phát triển một cách độc lập. Việc này cũng khiến cho môi trường ảo cũng không phụ thuộc vào môi trường cài đặt mặc định của Python trên máy local. Thậm chí, ta có thể phát triển các dự án khác nhau sử dụng nhiều version Python khác nhau để phù hợp với từng tổ chức, và yêu cầu của từng dự án.

## Khởi tạo môi trường ảo.

Có nhiều cách để khởi tạo môi trường ảo, ở đây tôi giới thiệu và sử dụng cách thông dụng nhất, đó là sử dụng gói thư viện **virtualenv**.

### Cài đặt virtualenv:

Kiểm tra virtualenv đã được cài trên máy của bạn hay chưa.

```
which virtualenv
```

Nếu không trả ra kết quả thì ta cần tiến hành cài đặt virtualenv.

Tại môi trường mặc định của máy local. sử dụng lệnh sau.

```
pip install virtualenv
```

Lưu ý, bản chất của việc cài đặt thư viện là sự download các gói có sẵn từ internet về máy của bạn, nên việc kết nối internet cho máy tính là điều hiển nhiên và cần thiết.

### Khởi tạo môi trường ảo:

```
virtualenv <project>
```

Lệnh này sẽ khởi tạo một folder có tên là project trên máy local, đây cũng chính là folder dùng để quản lý các thư viện, các gói cài đặt trong dự án của bạn.

### Khởi chạy môi trường ảo:

Để bắt đầu sử dụng môi trường ảo, ta cần activate môi trường đã khởi tạo trước.
Với thư mục có tên là project, sử dụng lệnh sau:

```
source project/bin/activate
```

Giờ đây môi trường ảo đã được khởi chạy, ta có thể cài đặt các gói thư viện vào môi trường ảo này, các gói này sẽ chỉ được sử dụng cho các dự án nằm trong môi trường ảo này mà không liên quan đến môi trường mặc định của máy hoặc các môi trường ảo khác.

### Tắt môi trường ảo:

Tại thư mục bạn sử dụng để kích hoạt môi trường ảo bên trên, dùng lệnh:

```
deactivate
```

Môi trường ảo bạn vừa khởi chạy đã được tắt, hiện tại ta không thể tiếp tục bổ sung thêm thông tin vào môi trường ảo được nữa. Hiểu đơn giản, ta đã ngừng làm việc với môi trường ảo này sau khi deactivate nó.

## Tích hợp môi trường ảo vào Jupyter Notebook.

Ở đây, ta cần hiểu khái niệm kernel của Jupyter Notebook là gì.

> *"Kernels are programming language specific processes that run independently and interact with the Jupyter Applications and their user interfaces. ipykernel is the reference Jupyter kernel built on top of IPython, providing a powerful environment for interactive computing in Python."*

<https://docs.jupyter.org/en/latest/projects/kernels.html>

Kernel là nơi thực thi mỗi câu lệnh trong mỗi cell của Jupyter Notebook. Do vậy, ta hoàn toàn có thể setup môi trường trong kernel để code chạy đúng theo môi trường mà ta đã chuẩn bị, hoặc tạo ra nhiều kernel khác nhau để thực thi code.

### Cài đặt ipykernel:

Để tạo ra nhiều kenel khác nhau trên môi trường chạy code, đầu tiên bạn phải cài gói ipykernel. Sử dụng lệnh sau:

```
pip install ipykernel
```

### Khởi tạo kernel cho môi trường ảo vừa tạo:

Sử dụng lệnh sau để khởi tạo kernel mới cho Jupyter. Với project chính là môi trường ảo ta vừa khởi tạo và khởi chạy bên trên.

```
python -m ipykernel install --user --name=project
```

Lúc này, khi khởi chạy Jupyter Notebook ngay trên môi trường ảo, ta có các lựa chọn sau:

![link](https://github.com/codedaoneu/codedaoneu.github.io/blob/96c925968317697b819e875f4b756018ed6b7484/images/ipython%20kernel.png)

Ta chỉ việc chuyển qua lựa chọn kernel vừa tạo, code trong Jupyter sẽ được thực thi đúng trên môi trường ảo mà ta đã tạo cho từng dự án riêng lẻ.

