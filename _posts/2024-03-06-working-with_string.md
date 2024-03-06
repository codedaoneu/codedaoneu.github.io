---
layout: post
title: "Working with string"
author: "codedaoneu"
tags: tutorial, python
---

# Kiểu dữ liệu, toán tử và các phương thức trong Python

Link tham khảo: https://pythongeeks.org/python-sequences-types-examples/

| Thuộc tính/ Kiểu dữ liệu | sequences | immutable | ordered | bags | True/False |
|--------------------------|-----------|-----------|---------|------|------------|
| Booleans                 | x         | x         | x       | x    | v          |
| Numbers/Complex          | x         | v         |         |      | x          |
| Strings                  | v         | v         | x       | x    | x          |
| Bytes                    | v         | v         |         |      | x          |
| byte arrays              | v         |           |         |      | x          |
| Lists                    | v         | x         | v       | x    | x          |
| Tuples                   | v         | v         | v       | x    | x          |
| Sets                     | x         | x         | x       | v    | x          |
| Frozenset                | x         | v         | x       | v    | x          |
| Dictionaries             | x         | x         | x       | v    | x          |
| Range()                  | v         | x         | v       | v    | x          |

## Thuộc tính sequences

### Các toán tử với đối tượng có thuộc tính sequences trong python


- Phép `+` dùng để join 2 chuỗi có cùng kiểu dữ liệu có thuộc tính sequences. Ví dụ:

```python
A = [1,2,3,4]
B = [5,6,7,8]

A + B
```
- Phép `*` dùng để lặp lại và join một chuỗi một số lượng lần nhất định.

- Phép `in` hoặc `not in` dùng để kiểm tra một phần tử có mặt trong một sequences hay không.

- Phép `[:]` dùng để lấy ra một phần của một sequences theo một khoảng cho trước.

### Sequence Functions and Methods

| STT | Tên function/ method | Chức năng                                                                 |
|-----|----------------------|---------------------------------------------------------------------------|
| 1   | len(sequence)        | Trả về độ dài của sequence                                                |
| 2   | index(index)         | Trả về index của phần tử đầu tiên chứa giá trị yêu cầu trong một sequence |
| 3   | min(sequence)        | Trả về giá trị nhỏ nhất của sequence                                      |
| 4   | max(sequence)        | Trả về giá trị lớn nhất của sequence                                      |
| 5   | count()              | Trả về số lần xuất hiện của một phần tử trong một sequence                |
| 6   | append(value)        | Thêm một phần tử vào cuối cùng của một sequence                           |
| 7   | clear()              | Xóa hết dữ liệu trong một sequence (trả về một sequence rỗng)             |
| 8   | insert(value, index) | Thêm một phần tử vào 1 vị trí được chỉ định cụ thể.                       |
| 9   | pop(index)           | Trả về và xóa giá trị tại index chỉ định                                  |
| 10  | remove(value)        | Xóa giá trị có index nhỏ nhất đầu tiên mà nó gặp trong một sequence       |
| 11  | reverse()            | Đảo ngược thứ tự giá trị của một sequence                                 |

