---
layout: post
title: "Công thức tính chỉ số chứng khoán VN30"
author: "codedaoneu"
tags: mystockself
---


1. Công thức tổng quát của VN30
$$
\text{VN30}t = \frac{\displaystyle\sum{i=1}^{30} P_{i,t} \times Q_i \times f_i \times c_i}{D_t} \times \text{Giá trị cơ sở}
$$

| Ký hiệu | Ý nghĩa |
|---|---|
| P_{i,t} | Giá khớp lệnh của mã i tại thời điểm t |
| Q_i     | Khối lượng cổ phiếu đang lưu hành |
| f_i     | Tỷ lệ free-float (làm tròn lên bội số 5%) |
| c_i     | Hệ số giới hạn tỷ trọng (capping), đảm bảo w_i ≤ 10% |
| D_t     | Số chia (Divisor), chuẩn hóa tại ngày cơ sở |
| BaseValue | Giá trị cơ sở (VN-Index tại 02/01/2009) |

3. Ba lớp điều chỉnh

3.1. Free-float

$$
f_i = \frac{Q_i - Q_i^{restricted}}{Q_i}
$$

Loại trừ khỏi $Q_i$:

- Cổ phiếu Nhà nước 
- Cổ đông sáng lập
- Cổ đông chiến lược nắm giữ
- Cổ phiếu quỹ
- Cổ phiếu hạn chế chuyển nhượng
- Sở hữu chéo > 5%

Kết quả làm tròn lên bội số 5% (ví dụ: 32% → 35%).

3.2. Capping 10%

Ràng buộc:

$$
w_i = \frac{P_i \cdot Q_i \cdot f_i \cdot c_i}{\sum_{j=1}^{30} P_j \cdot Q_j \cdot f_j \cdot c_j} \le 10\%
$$

3.3. Điều chỉnh số chia (Divisor)

$$
D_{new} = D_{old} \times \frac{MCap_{after}}{MCap_{before}}
$$

| Sự kiện | Có đổi D? |
|---|:---:|
| Thêm / loại mã khỏi rổ | ✓ |
| Phát hành thêm cổ phiếu | ✓ |
| Đổi tỷ lệ free-float | ✓ |
| Đổi hệ số capping | ✓ |
| Cổ tức bằng cổ phiếu, cổ phiếu thưởng, quyền mua | ✓ |
| Cổ tức tiền mặt | ✗ |
| Chia tách cổ phiếu (split) | ✗ |
