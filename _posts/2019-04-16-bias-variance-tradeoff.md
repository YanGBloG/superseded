---
layout: post
title: Hiểu về Bias - Variance Tradeoff
mathjax: true
tags : [math]
---

### Nội dung bài viết
<!-- TOC -->
### <a href="#-gioi-thieu-ve-bias-variance"> 1. Giới thiệu về Bias và Variance</a> 
#### <a href="#-dinh-nghia-ve-khai-niem"> 1.1. Định nghĩa về mặt khái niệm</a>
#### <a href="#-dinh-nghia-ve-hien-thi"> 1.2. Định nghĩa về mặt hiển thị</a>
#### <a href="#-dinh-nghia-ve-toan-hoc"> 1.3. Định nghĩa về mặt toán học</a>
### <a href="#-vi-du-minh-hoa"> 2. Ví dụ minh họa</a>
### <a href="#-ung-dung"> 3. Ứng dụng</a> 
<!-- End TOC -->

<a name="-gioi-thieu-ve-bias-variance"></a>

### 1. Giới thiệu về Bias và Variance

Trong tiếng Việt Bias được hiểu là sai số hệ thống rời, Variance là phương sai.

Hiểu được hai khái niệm Bias, Variance và những nguyên nhân gây mất cân bằng Bias, Variance có thể giúp ta nâng cao độ tin cậy của mô 
hình. Bias và Variance thường được định nghĩa trong ba ngữ cảnh: Về mặt khái niệm, hiển thị và toán học.

<a name="-dinh-nghia-ve-khai-niem"></a>

#### 1.1. Định nghĩa về mặt khái niệm

  * __Lỗi do Bias__: Khi sai số hệ thống lớn thường làm chênh lệch kết quả dự đoán (hoặc trung bình) của mô hình so với kết quả mà chúng ta đang cố gắng dự đoán. Nếu như bạn chỉ chạy một mô hình thì việc nói đến các giá trị dự đoán (hay trung bình) thường không được rõ rằng lắm. Tuy nhiên, giả sử như bạn có thể thực hiện phân tích và xây dựng mô hình nhiều lần cho tập dữ liệu của bạn. Do mức độ ngẫu nhiên của  tập dự liệu, kết quả đạt được từ các mô hình sẽ là một chuỗi các giá trị dự đoán. Ở đây, Bias chính là thước đo mức độ chênh lệch giữa các giá trị dự đoán của các mô hình đó so với giá trị chính xác thực tế.
  
  * __Lỗi do Variance__: Phương sai chính là mức độ biến thiên của kết quả dự đoán từ mô hình. Phương sai lớn thường làm cho một mô hình đưa ra các kết quả dự đoán nằm trong một giải phân bố rộng. Quay lại với ví dụ ở phần __Bias__, bạn có thể lặp lại quá trình xây dựng mô hình nhiều lần. Variance là mức độ dự đoán cho một điểm nhất định khác nhau giữa các lần thực hiện khác nhau của mô hình.

<a name="-dinh-nghia-ve-hien-thi"></a>

#### 1.2. Định nghĩa về mặt hiển thị

Chúng ta có thể thể hiện mối quan hệ giữa Bias, Variance và giá trị dự đoán với đồ thị dạng bia như Hình 1 với tâm của bia tương ứng là giá trị dự đoán tốt nhất so với thực tế, giảm dần ra phía ngoài bia. Tiếp tục giả sử chúng ta có thể thực hiện xây dựng nhiều mô hình cho cùng tập dữ liệu. Đôi khi ta nhận được một kết quả dự đoán tốt, giá trị dự đoán phân bố tập trung ở trung tâm của bia, trong khi các mô hình khác đem lại kết quả xấu hơn, giá trị dự đoán phân bố ngoài rìa của bia.

Có bốn trường hợp có thể xảy ra tương ứng với bias, variance cao và thấp.

<center><img src="/img/bias_variance/bulls-eye.png" alt="img" style="width: 450px;"/></center>
<center><p>Hình 1: Ảnh hưởng của Bias và Variance lên giá trị dự đoán.</p></center>

<!-- <div style="text-align:center" markdown="1"> -->
<!--   <img src="/img/bias_variance/bulls-eye.png" alt="img" style="width: 450px;"/> -->
<!--   <div class="caption"> -->
<!--     Hình 1: Ảnh hưởng của Bias và Variance lên giá trị dự đoán. -->
<!--  </div> -->
<!-- </div> -->

<a name="-dinh-nghia-ve-toan-hoc"></a>

#### 1.3. Định nghĩa về mặt toán học

Hãy tưởng tượng rằng chúng ta đang giải một bài toán có các giá trị dự đoán (output) là \\(Y\\) và các biến (input) là \\(X\\), giả sử mối quan hệ giữa đầu vào và đầu ra của bài toán là \\(Y = f(X) + \epsilon\\) với \\(\epsilon\\) là tập hợp sai số (error) có phân phối chuẩn, \\(\epsilon \sim \mathcal{N}(0,\sigma_\epsilon)\\).

Theo đó, bằng phương pháp như _Hồi quy tuyến tính_ hay một số phương pháp khác, ta xây dựng được hàm \\(\hat{f}(X)\\) của \\(f(X)\\). Trong trường hợp này, bình phương sai số dự kiến tại điểm \\(\mathbf{x}\\) là:

<div style="text-align:center" markdown="1">
\\(Err(x) = E\left[(Y-\hat{f}(x))^2\right]\\)
</div>

Giá trị sai số này được thể hiện dưới dạng __Bias__ và __Variance__ như sau:

<div style="text-align:center" markdown="1">
\\(Err(x) = \left(E[\hat{f}(x)]-f(x)\right)^2 + E\left[\left(\hat{f}(x)-E[\hat{f}(x)]\right)^2\right] +\sigma_e^2\\)

\\(Err(x) = \mathrm{Bias}^2 + \mathrm{Variance} + \mathrm{Irreducible\ Error}\\)
</div>

Giá trị \\(\mathrm{Irreducible\ Error}\\) cơ bản là sẽ không thể làm giảm được bằng mọi phương pháp. Mục tiêu của chúng ta là thay đổi mô hình để có thể giảm được cả Bias và Variance về 0. Tuy nhiên, trong thực tế khó có thể làm cho mô hình đạt được trạng thái hoàn hảo như vậy, dẫn đến việc chúng ta phải lựa chọn giữa tối thiểu bias hoặc tối thiểu variance, hoặc chính là cân bằng hai đại lượng này. Đó chính là Bias-Variance Tradeoff.

<a name="-vi-du-minh-hoa">

### 2. Ví dụ minh họa

Chúng ta cùng một ví dụ đơn giản, thực hiện xây dựng một mô hình dự đoán tỉ số phần trăm số người sẽ bầu chọn cho Đảng Cộng Hòa trong lần tổng tuyển cử tiếp theo.

Giả sử sau khi thực hiện một cuộc khảo sát bằng điện thoại, ta thu được các kết quả bầu chọn như sau:

<div style="text-align:center">
<table align="center">
<thead>
<tr>
<th>Đảng Cộng Hòa</th>
<th>Đảng Dân Chủ</th>
<th>Không phản hồi</th>
<th>Tổng cộng</th>
</tr>
</thead>
<tbody>
<tr>
<td>13</td>
<td>16</td>
<td>21</td>
<td>50</td>
</tr>
</tbody>
</table>
</div>

Tỉ lệ số người bầu chọn cho Đảng Cộng Hòa vào khoảng 13/(16 + 13) = 44.8 %. Ta đưa ra dự đoán rằng Đảng Dân Chủ sẽ chiến thắng cuộc tuyển cử với khoảng 10 phiếu. Tuy nhiên, khi cuộc tuyển cử thực sự diễn ra Đảng Cộng Hòa đã chiến thắng. Điều đó phản ánh khả năng dự đoán không tốt của mô hình nhưng tại sao lại xảy ra vấn đề này, điều gì khiến mô hình không hoạt động đúng như mong muốn của chúng ta ?

Thực ra có rất nhiều nguyên nhân dẫn đến vấn đề này, một vài nguyên nhân tôi cũng đã đề cập ở bài viết trước. Ở đây, tập dữ liệu chính là nguyên nhân chính. Chúng ta chỉ thực hiện khảo sát bằng điện thoại, có nhiều người không phản hồi khảo sát và dữ liệu khảo sát thực sự quá ít. Đồng thời đó cũng là những nguyên nhân dẫn đến bias và variance cao.



<a name="-ung-dung">

### 3. Ứng dụng








