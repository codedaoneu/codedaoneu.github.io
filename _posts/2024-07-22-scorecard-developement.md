---
layout: post
title: "Scorecard Development"
author: "codedaoneu"
tags: scorecard
---

Cũng như các model khác, việc triển khai một model, trên thực tế bao gồm nhiều bước khác nhau. Việc triển khai model không nhất thiết chỉ là xây dựng model, nó còn rất nhiều bước khác nhau để đảm bảo yêu cầu cao nhất, đó là đưa được model đi vào sử dụng thực tế. Hay nói cách khác, kết quả của model cần phải có tính chính xác và có thể sử dụng được. Ngoài ra, bên ngoài phạm vi bài viết này, còn là việc model cần được đặt trên một môi trường thực tế phù hợp, và có thể tích hợp với một hệ thống application thực tế khác.

## Explore Data

Công việc cần làm trước khi bắt đầu xây dựng một datamodel là bắt đầu với việc khám phá dữ liệu mẫu. Bắt đầu với một số các chỉ số thống kê đơn giản như phân phối của các giá trị, trung bình/trung vị, dữ liệu thiếu, khoảng giá trị của dữ liệu cho mỗi biến. 
