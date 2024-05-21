---
layout: post
title: "Working with string"
author: "codedaoneu"
tags: tutorial python
---

## Chuỗi ký tự

Có nhiều cách để nhập một chuỗi ký tự trong python:

String có thể nằm giữa 2 dấu nháy đơn:

Ví dụ:

```python 
'text block'
```

String có thể nằm giữa hai dấu nháy kép:

```python 
"text block"
```

### Escape Characters

Escape Characters được sử dụng để biểu thị các ký tự đặc biệt:
1. \n: Xuống dòng (newline).
2. \t: Tab.
3. \\': Dấu nháy đơn.
4. \\": Dấu nháy kép.
5. \\: Dấu gạch chéo ngược.

Khi sử dụng các Escape Characters, ta có thể hiển thị các ký tự đặc biệt mà không gây ra lỗi khi xử lý chuỗi ký tự trong python. Ví dụ, sử dụng ký tự `\` đứng trước ký tự đặc biệt mà ta muốn đưa vào chuỗi string:

```python
'alice\'s dog'
```

### Raw String

Ta có thể thêm ký tự `r` trước chuỗi ký tự cần in để in ra màn hình chuỗi ký tự nguyên bản của chuỗi. Chuỗi nguyên bản hoàn toàn bỏ qua các escape characters và in ra màn hình bất cứ ký tự `\` nào có chứa trong văn bản.

### Multiline Strings with Triple Quotes

Ta có thể sử dụng 3 lần dấu nháy đơn để có thể viết chuỗi string trên nhiều dòng.

### Multiline Comments

Ta có thể sử dụng 3 dấu nháy kép để biểu thị comment trên nhiều dòng, tương tự như việc sử dụng `#` để biểu diễn comment trên một dòng.

## Indexing and Slicing Strings

Tương tự như list, string trong python cũng sử dụng index vá slices. Ta có thể hình dung một chuỗi ký tự như một list trong đó mỗi phần tử là một ký tự trong chuỗi và mỗi ký tự có một index tương ứng.

## The in and not in Operators with Strings

Toán tử `in` và `not in` có thể sử dụng trong strings tương tự như với list values. Ví dụ:

```python
'Hello' in 'Hello World'
```

Kiểm tra một chuỗi ký tự có chứa ký tự Hello không.

## Useful String Methods

### The upper(), lower(), isupper(), and islower() String Methods

`upper(), lower()` chuyển đổi chuỗi cũ thành một chuỗi mới theo điều kiện viết hoa hoặc viết thường toàn bộ. Bởi vì kết quả của hai hàm trên đều trả về một chuỗi string nên ta hoàn toàn có thể sử dụng bộ hàm này một cách nối tiếp nhau.

`isupper(), and islower()` giúp kiểm tra trong chuỗi có ít nhất một ký tự và tất cả các ký tự được viết hoa hoặc viết thường.

### The isX String Methods

Song song với các hàm `isupper(), and islower()`, Python cũng cung cấp một số hàm khác để kiểm tra chuỗi ký tự

•	 `isalpha()` returns True if the string consists only of letters and is not blank.

•	 `isalnum()` returns True if the string consists only of letters and numbers
and is not blank.

•	 `isdecimal()` returns True if the string consists only of numeric characters
and is not blank.

•	 `isspace()` returns True if the string consists only of spaces, tabs, and newlines and is not blank.

•	 `istitle()` returns True if the string consists only of words that begin with
an uppercase letter followed by only lowercase letters.

### The startswith() and endswith() String Methods

```startswith(), endswith() ``` sử dụng để kiểm tra một chuỗi ký tự bắt đầu và kết thúc bằng một chuỗi ký tự được xác định trước hay không.

### join() and split()

`join()` giúp ta nối một list các chuỗi string lại với nhau. Nó hoạt động bằng cách lặp qua từng phần tử trong list và trả về một chuỗi string sau khi kết nối chúng lại. Chúng ta cũng có thể chèn vào giữa các phần tử một ký tự xác định nào đó. Ví dụ:

```python
'ABC'.join(['My', 'name', 'is', 'Simon'])
```

`split()` cho phép ta tách một chuỗi ký tự bằng một ký tự được xác định trước. Nếu như không truyền vào ký tự nào, hàm sẽ mặc định dùng space để split chuỗi.

Ví dụ:

```python
'MyABCnameABCisABCSimon'.split('ABC')
```

Chúng ta hoàn toàn có thể sử dụng các ký tự escape để đưa vào và split hoặc join các chuỗi văn bản lại với nhau.

### Justifying Text with rjust(), ljust(), and center()

`rjust(), ljust()` cho phép thêm vào ký tự ở đầu hoặc cuối một đoạn string.
Đối số đầu tiên là số lượng ký tự được sử dụng để thêm vào sao cho tổng độ dài của chuỗi bằng với số lượng được nhập. Đối số thứ 2 chính là ký tự được sử dụng, nếu không điền đối số thứ 2, ký tự mặc định được sử dụng là space.

`center()` giúp đặt chuỗi string vào chính giữa thay vì trái hoặc phải.

`strip(), rstrip(), and lstrip()` giúp lược bỏ dấu cách hoặc các ký tự bọc bên ngoài chuỗi string được truyền vào. Một sự lựa chọn khác là điền vào các ký tự ta muốn bỏ ra ngoài chuỗi, đối số được truyền vào chính là các ký tự cần lược bỏ. Thứ tự truyền vào của các ký tự không quan trọng khi thực hiện.
Ví dụ:

```python
spam = 'SpamSpamBaconSpamEggsSpamSpam'
spam.strip('Sam')
```

#### string.format_map(z)

Trả về giá trị của một key trong một dictionary. Ví dụ:

```python
# input stored in variable a. 
a = {'x':'John', 'y':'Wick'} 
  
# Use of format_map() function 
print("{x}'s last name is {y}".format_map(a))
```

### Copying and Pasting Strings with the pyperclip Module

Thư viện pyperclip giúp ta có thể, một cách nhanh chóng copy một đoạn string vào clipboard của máy tính và/hoặc paste một đoạn văn bản đã được copy từ trước vào python. Ví dụ:

```python
import pyperclip


pyperclip.copy('Hello world!')
pyperclip.paste()
```



Tất cả string method có thể được tìm và tra cứu tại:

https://docs.python.org/3/library/stdtypes.html#string-methods

