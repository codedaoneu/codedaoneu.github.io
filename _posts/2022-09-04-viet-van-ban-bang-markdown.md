---
layout: post
title: "Soạn thảo văn bản bằng ngôn ngữ Markdown"
author: "codedaoneu"
tags: tutorial
---

Việc vừa học, vừa thực hành là việc vô cùng cần thiết trong việc tìm hiểu một vấn đề. Ngoài việc được trải nghiệm thực tế với các vấn đề đang gặp, có còn giúp chúng ta nhận dạng được các vấn đề mà chỉ có bắt tay vào làm mới có thể nhận ra. Việc lặp lại chu trình thực hành -> tìm ra vấn đề -> giải quyết vấn đề cho đến khi hoàn thành vấn đề lớn giúp ta học được tính kiên nhẫn, rèn luyện khả năng tìm tòi của bản thân, và nâng cao kỷ luật làm việc.

Trong quá trình lập blog này, vấn đề đầu tiên mà tôi gặp phải là việc sử dụng ngôn ngữ Markdown để thực hiện việc định dạng các phần của bài viết, chèn ảnh, link, video, hoặc các đoạn code. Hiểu đơn giản thì Markdown là một ngôn ngữ ký hiệu, sử dụng các ký tự đặc biệt để định dạng chữ viết, sau đó trình thông dịch sẽ chuyển các định dạng này thành các ngôn ngữ như html... và hiển thị lên trang web như chúng ta nhìn thấy. Sau đây là một số vấn đề và ví dụ thực hành cụ thể.

## Tạo các thẻ H1, H2 cho văn bản.

Sử dụng các dấu # để tạo các thẻ  H tương ứng.  Số lượng dấu # sẽ tương ứng với loại thẻ đó. Ví dụ #H tương ứng với thẻ H1. nếu ta gõ # Đây là thẻ H1, thì kết quả hiển thị sẽ là:

> # Đây là thẻ H1

Tương tự cho các loại thẻ khác. **## Đây là thẻ H2** cho kết quả hiển thị là một thẻ H2.

> ## Đây là thẻ H2
> ### Đây là thẻ H3
> #### Đây là thẻ H4
> ##### Đây là thẻ H5
> ###### Đây là thẻ H6

Trong ví dụ trên và kế tiếp dưới đây đây, các kết quả được đưa vào trong một khối (blockquote). Bằng việc đặt dấu ">" ở đầu câu và đưa nội dung văn bản vào bên trong khối.

## Tô đậm, in nghiêng, gạch ngang đoạn văn bản
Để tô đậm, dùng cú pháp `**Đoạn văn bản**` với hai dấu ** ở đầu và cuối đoạn văn bản cần in đậm.

Kết quả:

> **Đoạn văn bản**

In nghiêng, dùng cú pháp `*Đoạn văn bản*` với một dấu * ở đầu và cuối đoạn văn bản cần in nghiêng.

Kết quả:

> *Đoạn văn bản*

Gạch ngang, dùng cú pháp `~~Đoạn văn bản~~` với hai ký tự ~~ ở đầu và cuối văn bản cần gạch ngang.

Kết quả:

> ~~Đoạn văn bản~~

Kết hợp, có một đoạn văn bản vừa in nghiêng, vừa tô đậm. Sử dụng cú pháp `***Đoạn văn bản***`, kết hợp cả ba định dạng trên bằng cú pháp `~~***Đoạn văn bản***~~`

Kết quả:

> ***Đoạn văn bản***
>
> ~~***Đoạn văn bản***~~

## Định dạng một khối code

Có thể định dạng các ngôn ngữ lập trình khác nhau bằng cú pháp sau:

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

Hoặc một đoạn ngôn ngữ python được định dạng bằng markdown như sau ([\t] ký hiệu cho tab):

> \```python
> 
> def query_generator(schema_name, table_name, *argv):
>
>[\t]query = "SELECT * FROM {}.{} WHERE 1=1 ".format(schema_name, table_name)
> 
>[\t]for arg in argv:
>
>[\t][\t]cond = "and {} ".format(arg)
>
>[\t][\t]query = query + cond
>
>[\t]return query
>
> \```

Kết quả:

```python
def query_generator(schema_name, table_name, *argv):
    query = "SELECT * FROM {}.{} WHERE 1=1 ".format(schema_name, table_name)
    for arg in argv:
        cond = "and {} ".format(arg)
        query = query + cond
    return query
```
## Tạo list

Để tạo một danh sách không có thứ tự (Các đầu mục chính ngang hàng với nhau), sử dụng các ký tự dấu hoa thị (*) ở ngay đầu dòng của các đầu mục. Với các đầu mục con, ấn Tab vào và tiếp tục sử dụng *. Ngoài *, ta còn có thể sử dụng các ký tự khác có cùng tác dụng như -, +

Ví dụ:

```markdown
Danh sách của tôi

* Đầu mục thứ nhất

* Đầu mục thứ hai

    * Đầu mục con thứ nhất của đầu mục thứ hai
    * Đầu mục con thứ hai của đầu mục thứ hai
        * Đầu mục con thứ nhất của đầu mục con thứ hai của đầu mục thứ hai
```

Kết quả:

>Danh sách của tôi
>
>* Đầu mục thứ nhất
>
>* Đầu mục thứ hai
>
>    * Đầu mục con thứ nhất của đầu mục thứ hai.
>    * Đầu mục con thứ hai của đầu mục thứ hai.
>        * Đầu mục con thứ nhất của đầu mục con thứ hai của đầu mục thứ hai.
>* Đầu mục thứ ba

## Tạo một list có thứ tự

Sử dụng số thay cho ký tự *, -, + để tạo một danh sách có thứ tự.

```markdown
Danh sách của tôi

1. Đầu mục thứ nhất

2. Đầu mục thứ hai

    1. Đầu mục con thứ nhất của đầu mục thứ hai.
    2. Đầu mục con thứ hai của đầu mục thứ hai.
        1. Đầu mục con thứ nhất của đầu mục con thứ hai của đầu mục thứ hai.
3. Đầu mục thứ ba
```
Kết quả:

> Danh sách của tôi
>
>1. Đầu mục thứ nhất
>
>2. Đầu mục thứ hai
>
>    1. Đầu mục con thứ nhất của đầu mục thứ hai.
>    2. Đầu mục con thứ hai của đầu mục thứ hai.
>        1. Đầu mục con thứ nhất của đầu mục con thứ hai của đầu mục thứ hai.
>3. Đầu mục thứ ba

## Chèn liên kết

Chèn một đường link vào văn bản bằng cú pháp `<link>`. Ví dụ

>```markdown
><https://github.com/codedaoneu/codedaoneu.github.io>
>```

Kết quả:

<https://github.com/codedaoneu/codedaoneu.github.io>

Chèn một link được liên kết với một đoạn văn bản.

>```markdown
>[link](https://github.com/codedaoneu/codedaoneu.github.io>)
>```

Kết quả:

[link](https://github.com/codedaoneu/codedaoneu.github.io>)

## Chèn ảnh

Gần giống với cú pháp chèn link, thêm dấu `!` ở phía trước ngoặc vuông.

```markdown
![Minion](https://octodex.github.com/images/minion.png)
```

Kết quả:

![Minion](https://octodex.github.com/images/minion.png)

