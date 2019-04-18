---
layout: post
title: Hiểu về Bias và Variance
tags : [math]
---

### 1. Bias và Variance

Trong tiếng Việt Bias được hiểu là sai số hệ thống rời, Variance là phương sai.

Hiểu được hai khái niệm Bias, Variance và những nguyên nhân gây mất cân bằng Bias, Variance có thể giúp ta nâng cao độ tin cậy của mô 
hình. Bias và Variance thường được định nghĩa trong ba ngữ cảnh: Về mặt khái niệm, hiển thị và toán học.

#### 1.1. Định nghĩa về mặt khái niệm

  * __Lỗi do Bias__: Khi sai số hệ thống lớn thường làm chênh lệch kết quả dự đoán (hoặc trung bình) của mô hình so với kết quả mà chúng ta đang cố gắng dự đoán. Nếu như bạn chỉ chạy một mô hình thì việc nói đến các giá trị dự đoán (hay trung bình) thường không được rõ rằng lắm. Tuy nhiên, giả sử như bạn có thể thực hiện phân tích và xây dựng mô hình nhiều lần cho tập dữ liệu của bạn. Do mức độ ngẫu nhiên của  tập dự liệu, kết quả đạt được từ các mô hình sẽ là một chuỗi các giá trị dự đoán. Ở đây, Bias chính là thước đo mức độ chênh lệch giữa các giá trị dự đoán của các mô hình đó so với giá trị chính xác thực tế.
  
  * __Lỗi do Variance__: Phương sai chính là mức độ biến thiên của kết quả dự đoán từ mô hình. Phương sai lớn thường làm cho một mô hình đưa ra các kết quả dự đoán nằm trong một giải phân bố rộng. Quay lại với ví dụ ở phần __Bias__, bạn có thể lặp lại quá trình xây dựng mô hình nhiều lần. Variance là mức độ dự đoán cho một điểm nhất định khác nhau giữa các lần thực hiện khác nhau của mô hình.
  
#### 1.2. Định nghĩa về mặt hiển thị

Chúng ta có thể thể hiện mối quan hệ giữa Bias, Variance và giá trị dự đoán với đồ thị dạng bia như Hình 1 với tâm của bia tương ứng là giá trị dự đoán tốt nhất so với thực tế, giảm dần ra phía ngoài bia. Tiếp tục giả sử chúng ta có thể thực hiện xây dựng nhiều mô hình cho cùng tập dữ liệu. Đôi khi ta nhận được một kết quả dự đoán tốt, giá trị dự đoán phân bố tập trung ở trung tâm của bia, trong khi các mô hình khác đem lại kết quả xấu hơn, giá trị dự đoán phân bố ngoài rìa của bia.

Có bốn trường hợp có thể xảy ra tương ứng với bias, variance cao và thấp.

<!-- <div style="text-align:center" markdown="1"> -->
  <img src="/img/bias_variance/bulls-eye.png" alt="drawing" width="218" height="225" class="center"/>
  <div class="caption">
   Hình 1: Ảnh hưởng của Bias và Variance lên giá trị dự đoán.
  </div>
<!-- </div> -->
