---
layout: post
title: "Các tham số trong mô hình LogisticRegression Sklearn"
author: "codedaoneu"
tags: tutorial
---


## penalty

Các loại penalty phổ biến được sử dụng trong Logistic Regression:
- L1 regularization (Lasso).
- L2 regularization (Ridge).
- None: Không sử dụng tham số penalty.
- elasticnet: Sử dụng cả L1 và L2.

L1 và L2 là phương pháp chuẩn hoá sử dụng để kiểm soát overfitting trong mô hình. Khi huấn luyện mô hình Logistic Regression, ta thường sử dụng một hàm mất mát có thêm thành phần penalty để giảm overfitting và tăng hiệu suất dự đoán của mô hình. Các loại penalty phổ biến được sử dụng trong Logistic Regression bao gồm L1 regularization (Lasso) và L2 regularization (Ridge).

## solver

Trong mô hình Logistic Regression, tham số "solver" được sử dụng để chỉ định thuật toán được sử dụng để tối ưu hóa hàm mất mát khi huấn luyện mô hình. Các giá trị phổ biến của tham số "solver" bao gồm:

1. "liblinear": Sử dụng thuật toán tối ưu hóa LIBLINEAR, phù hợp cho tập dữ liệu nhỏ hoặc khi cần xử lý đồng thời một số penalty khác nhau (như L1 và L2) hoặc khi yêu cầu chính xác cao.
2. "newton-cg": Sử dụng phương pháp Newton-Conjugate Gradient, phù hợp cho dữ liệu lớn hơn và không thể xử lý đồng thời nhiều penalty.
3. "lbfgs": Sử dụng thuật toán tối ưu hóa Limited-memory Broyden-Fletcher-Goldfarb-Shanno, phù hợp cho tập dữ liệu lớn.
4. "sag": Sử dụng thuật toán tối ưu hóa Stochastic Average Gradient, phù hợp cho tập dữ liệu lớn với nhiều features.
5. "saga": Sự cải tiến của thuật toán SAG cho cả L1 và L2 penalty, phù hợp cho tập dữ liệu lớn và hỗ trợ parallel computing.

Việc lựa chọn thông số "solver" phù hợp giữa các giá trị trên phụ thuộc vào đặc điểm của dữ liệu và yêu cầu của bài toán cụ thể.

## max_iter

Trong mô hình Logistic Regression, tham số "max_iter" là một tham số quy định số lượng lần lặp tối đa mà thuật toán sẽ thực hiện để tối ưu hóa hàm mất mát. Nếu sau số lần lặp này mà thuật toán chưa hội tụ (tức là chưa đạt được giá trị tối ưu), huấn luyện sẽ dừng và trả về kết quả gần đúng nhất có thể. 

Tham số "max_iter" quan trọng vì nó giúp kiểm soát thời gian huấn luyện và cũng có thể ngăn ngừa overfitting. Tuy nhiên, nếu giá trị của "max_iter" quá nhỏ, có thể dẫn đến việc thuật toán không hội tụ và mô hình không đạt hiệu suất cần thiết. Do đó, việc thiết lập giá trị hợp lý cho "max_iter" cần được thực hiện cẩn thận. Thường thì giá trị của "max_iter" sẽ được chọn dựa trên kinh nghiệm hoặc thông qua việc sử dụng các phương pháp tinh chỉnh siêu tham số.

## C

Trong mô hình Logistic Regression, tham số "C" là một tham số quan trọng điều chỉnh mức độ chuẩn hoá (regularization) trong quá trình huấn luyện mô hình. Tham số "C" được sử dụng để kiểm soát độ cứng của mô hình, ảnh hưởng đến việc mô hình sẽ "tin tưởng" vào dữ liệu huấn luyện đến đâu.

Giá trị của tham số "C" càng lớn, mức độ chuẩn hoá càng ít và mô hình sẽ cố gắng tối ưu hóa đúng hơn trên dữ liệu huấn luyện (có thể dẫn đến overfitting). Ngược lại, nếu "C" nhỏ, mô hình sẽ tin tưởng vào mức độ chung và đơn giản hơn (có thể dẫn đến underfitting).

Như vậy, việc điều chỉnh tham số "C" là một phần quan trọng trong việc điều chỉnh mô hình Logistic Regression để đạt được hiệu suất dự đoán tốt nhất trên tập dữ liệu. Thông thường, giá trị của "C" cần được tinh chỉnh thông qua các phương pháp tinh chỉnh siêu tham số như Grid Search hoặc Random Search để chọn ra giá trị tối ưu cho mô hình.

## dual

Trong mô hình Logistic Regression của thư viện scikit-learn, tham số "dual" là một tham số boolean (True hoặc False) quy định phương pháp giải bài toán tối ưu hóa. 

Tham số "dual" có ảnh hưởng đến hiệu suất của thuật toán, nhưng thường ít được sử dụng nếu số lượng features (đặc trưng) lớn hơn số lượng mẫu dữ liệu.

Nếu "dual=True", thuật toán sẽ tối ưu hóa bài toán cực tiểu hóa bằng cách giải hệ phương trình đối ngẫu (dual problem). Đây là phương pháp thích hợp khi số lượng features nhỏ hơn số lượng mẫu dữ liệu.

Nếu "dual=False", thuật toán sẽ tối ưu hóa trực tiếp bài toán cực tiểu hóa (primal problem). Đây là phương pháp phù hợp khi số lượng features lớn hơn số lượng mẫu dữ liệu.

Trong hầu hết các trường hợp thông thường, thực hiện mô hình Logistic Regression với tham số "dual=False" là được khuyến nghị. DefaultValue cho tham số "dual" là False.

## tol

Tham số "tol" trong mô hình Logistic Regression của thư viện scikit-learn là một ngưỡng dừng được sử dụng để kiểm tra sự hội tụ của thuật toán tối ưu hóa. "tol" đại diện cho tolerance và quy định mức độ chấp nhận được cho sự thay đổi trong hàm mất mát giữa các lần cập nhật trọng số trong quá trình huấn luyện. 

Khi sự thay đổi trong hàm mất mát giảm dưới ngưỡng "tol", thuật toán sẽ dừng lại vì coi rằng mô hình đã hội tụ đủ. Trong quá trình huấn luyện, nếu giá trị thay đổi của hàm mất mát giữa các lần cập nhật trọng số nhỏ hơn "tol", thuật toán sẽ dừng sớm giúp tiết kiệm thời gian huấn luyện.

Một giá trị "tol" thấp có thể dẫn đến thời gian huấn luyện tăng lên, nhưng cung cấp sự chính xác cao hơn. Ngược lại, giá trị "tol" cao có thể giảm thời gian huấn luyện, nhưng cũng có thể giảm chính xác của mô hình.

Việc chọn giá trị thích hợp cho "tol" thường phụ thuộc vào độ chính xác mà bạn muốn đạt được và cũng có thể được tinh chỉnh thông qua việc thử nghiệm và đánh giá hiệu suất trên tập dữ liệu kiểm tra. DefaultValue cho tham số "tol" là 1e-4.

## fit_intercept

Trong mô hình Logistic Regression của thư viện scikit-learn, tham số "fit_intercept" là một tham số boolean (True hoặc False) xác định xem mô hình sẽ học tham số chệch (bias) hay không.

Nếu "fit_intercept=True", mô hình sẽ học một giá trị chệch (bias) trong quá trình huấn luyện. Bias là giá trị cố định được thêm vào kết quả của hàm dự đoán để điều chỉnh giá trị dự đoán chính xác hơn với dữ liệu thực tế.

Nếu "fit_intercept=False", mô hình sẽ không học giá trị chệch (bias) và giả định rằng mô hình đi qua gốc tọa độ (0,0) trong không gian đặc trưng.

Việc sử dụng giá trị chệch (bias) thường giúp cải thiện khả năng dự đoán của mô hình trên tập dữ liệu thực tế. Thông thường, nếu không có lý do đặc biệt, việc cài đặt "fit_intercept=True" là được khuyến nghị.

DefaultValue cho tham số "fit_intercept" là True.

## intercept_scaling

Trong mô hình Logistic Regression của thư viện scikit-learn, tham số "intercept_scaling" là một hệ số nhân được áp dụng cho intercept. Tính năng này cho phép cân nhắc mức độ ảnh hưởng của intercept đối với các trọng số của mô hình.

Khi "intercept_scaling" được đặt khác 1, intercept sẽ được nhân với giá trị "intercept_scaling" trước khi tính toán hàm mất mát. Điều này có thể giúp kiểm soát mức độ ảnh hưởng của intercept đối với việc huấn luyện mô hình.

Mặc định, giá trị của "intercept_scaling" là 1. Nếu không có nhu cầu cụ thể, bạn có thể giữ giá trị mặc định này. Tuy nhiên, nếu muốn điều chỉnh vai trò của intercept trong mô hình, bạn có thể thay đổi giá trị của "intercept_scaling" để đạt được hiệu quả tối ưu trong quá trình huấn luyện.

Việc điều chỉnh "intercept_scaling" thường không phổ biến và chỉ được sử dụng trong trường hợp cụ thể của việc tinh chỉnh mô hình Logistic Regression.

## class_weight

Trong mô hình Logistic Regression của thư viện scikit-learn, tham số "class_weight" cho phép bạn cân chỉnh trọng số của các lớp trong mô hình. Điều này hữu ích khi dữ liệu không cân bằng, với một số lớp có số lượng mẫu ít hơn so với các lớp khác.

Có thể đặt "class_weight" bằng một số giá trị khác nhau như:
- "class_weight=None": Mọi lớp được coi là có cùng trọng số.
- "class_weight='balanced'": Cân bằng tỷ lệ số lượng mẫu giữa các lớp tự động.
- "class_weight={class_label: weight}": Đối với mỗi nhãn lớp, bạn có thể xác định trọng số cụ thể.

Việc sử dụng "class_weight" đúng cách có thể giúp cải thiện khả năng dự đoán của mô hình trên dữ liệu không cân bằng. Bằng cách tăng trọng số của các lớp thiểu số, mô hình có thể học tốt hơn từ các lớp ít mẫu hơn.

Nên xác định xem có cần thiết điều chỉnh trọng số của các lớp bằng "class_weight" dựa trên sự không cân bằng của dữ liệu của bạn để cải thiện hiệu suất của mô hình Logistic Regression.

## random_state

Trong mô hình Logistic Regression của thư viện scikit-learn, tham số "random_state" được sử dụng để cài đặt seed cho quá trình tạo các giá trị ngẫu nhiên trong quá trình huấn luyện mô hình. Seed này đảm bảo rằng các kết quả huấn luyện sẽ được tái tạo một cách đáng tin cậy nếu bạn chạy mô hình nhiều lần với cùng một giá trị "random_state".

Khi bạn cung cấp một giá trị cụ thể cho "random_state", mô hình sẽ sử dụng seed đó để tạo ngẫu nhiên các tham số ban đầu và tạo ra các phân chia ngẫu nhiên của dữ liệu (nếu áp dụng). Điều này giúp kiểm soát tính ngẫu nhiên trong quá trình huấn luyện và đảm bảo kết quả kiểm tra có thể tái tạo.

Nếu "random_state" không được cung cấp hoặc được đặt là None, mỗi lần chạy mô hình có thể tạo ra kết quả khác nhau, giữa các lần chạy khác nhau. Điều này có thể gây khó khăn trong việc so sánh kết quả giữa các lần thử nghiệm.

Vì vậy, khi bạn muốn kết quả huấn luyện có thể tái tạo và so sánh dễ dàng, hãy cung cấp một giá trị cụ thể cho "random_state". Điều này sẽ giúp đảm bảo tính xác định và đáng tin cậy của quá trình huấn luyện mô hình Logistic Regression
