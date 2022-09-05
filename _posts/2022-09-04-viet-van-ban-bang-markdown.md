---
layout: post
title: "Soạn thảo văn bản bằng ngôn ngữ Markdown"
author: "codedaoneu"
tags: tutorial
---

Nhằm truyền tải nội dung bài viết lên blog cá nhân, mục đích chủ đạo của tôi bao gồm, viết các bài viết hướng dẫn, các bài viết học thuật liên quan đến các chủ đề về data. Các bài viết phân tích khác. Hoặc đơn giản là các ghi chú như một bài nhật ký.

Trong quá trình lập blog này, vấn đề đầu tiên mà tôi gặp phải là việc sử dụng ngôn ngữ Markdown để thực hiện việc định dạng các phần của bài viết, chèn ảnh, link, video, hoặc các đoạn code. Hiểu đơn giản thì Markdown là một ngôn ngữ ký hiệu, sử dụng các ký tự đặc biệt để định dạng chữ viết, sau đó trình thông dịch sẽ chuyển các định dạng này thành các ngôn ngữ như html... và hiển thị lên trang web như chúng ta nhìn thấy. Sau đây là một số ví dụ thực hành cụ thể.

## Tạo các thẻ H1, H2 cho văn bản.

Sử dụng các dấu # để tạo các thẻ  H tương ứng.  Số lượng dấu # sẽ tương ứng với loại thẻ đó. Ví dụ #H tương ứng với thẻ H1. nếu ta gõ # Đây là thẻ H1, thì kết quả hiển thị sẽ là:

# Đây là thẻ H1

Tương tự cho các loại thẻ khác. **## Đây là thẻ H2** cho kết quả hiển thị là một thẻ H2.

> ## Đây là thẻ H2
> ### Đây là thẻ H3
> #### Đây là thẻ H4
> ##### Đây là thẻ H5
> ###### Đây là thẻ H6

Trong ví dụ trên và kế tiếp dưới đây đây, tôi đưa các kết quả của mình vào trong một khối (blockquote). Bằng việc đặt dấu ">" ở đầu câu và đưa nội dung văn bản vào bên trong khối.

## Tô đậm, in nghiêng, gạch ngang đoạn văn bản
Để tô đậm, ta dùng cú pháp `**Đoạn văn bản**` với hai dấu ** ở đầu và cuối đoạn văn bản cần in đậm.

Kết quả:

> **Đoạn văn bản**

In nghiêng, ta dùng cú pháp `*Đoạn văn bản*` với một dấu * ở đầu và cuối đoạn văn bản cần in nghiêng.

Kết quả:

> *Đoạn văn bản*

Gạch ngang, ta dùng cú pháp `~~Đoạn văn bản~~` với hai ký tự ~~ ở đầu và cuối văn bản cần gạch ngang.

Kết quả:

> ~~Đoạn văn bản~~

Kết hợp, ta có một đoạn văn bản vừa in nghiêng, vừa tô đậm. Sử dụng cú pháp `***Đoạn văn bản***`, kết hợp cả ba định dạng trên bằng cú pháp `~~***Đoạn văn bản***~~`

Kết quả:

> ***Đoạn văn bản***
>
> ~~***Đoạn văn bản***~~

## Định dạng một khối code

Ta có thể định dạng các ngôn ngữ lập trình khác nhau bằng cú pháp sau:

>\```Tên ngôn ngữ
>
>Khối code
>
>\```

Ví dụ:

>\```markdown
>
>Khối code bằng ngôn ngữ markdown
>
>```

Kết quả:

```markdown
Khối code bằng ngôn ngữ markdown
```

Hoặc một đoạn ngôn ngữ python được định dạng bằng markdown như sau:

```python
def query_generator(schema_name, table_name, *argv):
    query = "SELECT * FROM {}.{} WHERE 1=1 ".format(schema_name, table_name)
    for arg in argv:
        cond = "and {} ".format(arg)
        query = query + cond
    return query
```
