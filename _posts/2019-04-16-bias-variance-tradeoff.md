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
#### <a href="#-k-nearest-neighbor"> 3.1. Thuật toán _k_ - Nearest Neighbor</a>
#### <a href="#-variance-va-bias"> 3.2. Variane và Bias</a>
#### <a href="-phan-tich-bias-variance"> 3.3. Phân tích bias và variance</a>
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

Chúng ta có thể thể hiện mối quan hệ giữa Bias, Variance và giá trị dự đoán với đồ thị dạng bia (bulls-eye diagram) như Hình 1 với tâm của bia tương ứng là giá trị dự đoán tốt nhất so với thực tế, giảm dần ra phía ngoài bia. Tiếp tục giả sử chúng ta có thể thực hiện xây dựng nhiều mô hình cho cùng tập dữ liệu. Đôi khi ta nhận được một kết quả dự đoán tốt, giá trị dự đoán phân bố tập trung ở trung tâm của bia, trong khi các mô hình khác đem lại kết quả xấu hơn, giá trị dự đoán phân bố ngoài rìa của bia.

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
<table align="center" border="2">
<thead>
<tr>
<th>&nbsp;&nbsp;Đảng Cộng Hòa&nbsp;&nbsp;</th>
<th>&nbsp;&nbsp;Đảng Dân Chủ&nbsp;&nbsp;</th>
<th>&nbsp;&nbsp;Không phản hồi&nbsp;&nbsp;</th>
<th>&nbsp;&nbsp;Tổng cộng&nbsp;&nbsp;</th>
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

Cụ thể như thực hiện khảo sát qua điện thoại dễ dẫn đến bias cao vì chỉ thực hiện trên nhóm người sử dụng điện thoại. Không tập trung vào các thành phần không phản hồi cũng là một nguyên nhân dẫn đến bias cao. Kết quả dự đoán được thể hiện trên bulls-eye diagram có xu hương dịch ra xa tâm hơn, tuy nhiên điều này không làm tăng mức độ phân tán của kết quả dự đoán.

Mặt khác, số lượng khảo sát quá ít dễ dẫn đến variance cao. Nếu có thể tăng số lượng khảo sát lên sẽ tăng mức độ phù hợp của mô hình, mặc dù chưa hẳn sẽ làm kết quả dự đoán chính xác hơn do bias cao nhưng variance của kết quả dự đoán sẽ giảm. Trên bulls-eye diagram, kết quả dự đoán có mức độ phân tán cao, tăng kích thước tập dữ liệu sẽ làm giảm độ phân tán nhưng có thể kết quả vẫn lệch xa tâm của đồ thị.

Thực tế thì người làm mô hình không nên chỉ tập trung vào việc giảm một trong hai giá trị bias và variance, thay vào đó, hãy cố gắng giảm tối đa tổng sai số bằng cách cân bằng bias và variance.

<a name="-ung-dung">

### 3. Ứng dụng

Hãy cùng đi vào một ứng dụng thực tế hơn. Giả sử ta có tập dữ liệu bao gồm: Người đăng ký, mức độ giàu có và mức độ tôn giáo của người đăng kí trở thành cử tri, dữ liệu được thể hiện trong đồ thị Hình 2. Trục \\(x\\) thể hiện mức độ giàu có, trục \\(y\\) thể hiện mức độ tôn giáo của cử tri, màu đỏ là những của tri thuộc Đảng Cộng Hòa, màu xanh là những cử tri thuộc Đảng Dân Chủ. Chúng ta sẽ dự đoán cử tri thông các đặc tính là mức độ giàu có và tôn giáo của mỗi người.

<center><img src="/img/bias_variance/registration.png" alt="img" style="width: 651px;"/></center>
<center><p>Hình 2: Đăng kí cử tri (Tôn giáo (trục y) vs độ giàu có (trục x)).</p></center>

<a name="-k-nearest-neighbor">

#### 3.1. Thuật toán _k_ - Nearest Neighbor

Có khá nhiều cách để thực hiện bài toán này, đối với những bài toán phân loại nhị phân (binary classification) mô hình hồi quy hậu cần  (một cách rất không hợp lý), logistic regressions thường xuyên được xử dụng. Tuy nhiên, đối với bài toán này một kĩ thuật khác sẽ được sử dụng, đó là _k_ - Nearest Neighbor, _k_-NN. Về thuật toán này tôi đã có một bài viết về nó nên sẽ không nhắc lại nhiều.

Trong _k_-NN, một voter (người đăng ký trở thành cử tri) được xác định bằng cách xác định _k_ voters gần nhất với voter mục tiêu. Nếu các voters gần nhất thuộc Đảng Dân Chủ (dựa trên tôn giáo và tiền bạc) thì voter mục tiêu cũng thuộc Đảng Dân Chủ.

Ví dụ với _k_ = 1, các voter trong tập dữ liệu huấn luyện sẽ có diện tích ảnh hưởng được khoanh vùng xung quanh các điểm xanh, đỏ (Hình 3). Voter mới sẽ được xác định rơi vào diện tích của chấm xanh hay đỏ mà từ đó suy ra kết quả dự đoán cho voter đó.

<center><img src="/img/bias_variance/nns.PNG" alt="img" style="width: 607px;"/></center>
<center><p>Hình 3: _k_-NN với _k_ = 1 cho tập dữ liệu huấn luyện.</p></center>

Thực hiện huấn luyện mô hình với _k_ = 5. Sau khi huấn luyện, tiếp tục thực hiện dự đoán trên tập kiểm thử. Kết quả thu được như sau:

<center><img src="/img/bias_variance/nns_prediction.PNG" alt="img" style="width: 610px;"/></center>
<center><p>Hình 4: Huấn luyện mô hình với _k_ = 5.</p></center>

Mỗi các nhân cũng có thể được xác định thuộc Đảng Dân Chủ hay Cộng Hòa bằng cách thể hiện qua đồ thị phân chia ranh giới đối với tập kiểm thử.

<center><img src="/img/bias_variance/nns_k-5.PNG" alt="img" style="width: 609px;"/></center>
<center><p>Hình 5: Phân chia ranh giới của kết quả dự đoán (Với _k_ = 5).</p></center>

Đối với những cá nhân ở gần vùng ranh giới có màu nhạc hơn do mức độ chính xác thấp, ở những vị trí màu đậm cho mức độ chính xác cao hơn. Phía trên đường ranh giới là các cá nhân thuộc Đảng Cộng Hòa, phía dưới thuộc Đảng Dân Chủ.

Nhân tố ảnh hưởng lớn nhất đến một mô hình sử dụng _k_-NN chính là việc lựa chọn số lượng _k_. Lựa chọn _k_ phù hợp sẽ tăng mức độ dự đoán chính xác cho mô hình.

<a name="#-variance-va-bias">

#### 3.2. Variance và Bias

Với ví dụ trên, khi tăng _k_ kết quả dự đoán nhận được có vẻ "mượt" hơn do lấy trung bình của nhiều voter hơn. Với _k_ = 1, đường biên giới không được mượt cho lắm, đồng thời có nhiều giá trị dự đoán sai nằm sâu bên trong vùng phân chia (được gọi là island). Với _k_ = 20, có thể thấy được đường biên giới mượt hơn hẳn và không còn trong thấy các "island" nữa (Hình 6, 7).

<center><img src="/img/bias_variance/k-1.PNG" alt="img" style="width: 609px;"/></center>
<center><p>Hình 6: Phân chia ranh giới của kết quả dự đoán (Với _k_ = 1).</p></center>

<center><img src="/img/bias_variance/k-20.PNG" alt="img" style="width: 609px;"/></center>
<center><p>Hình 7: Phân chia ranh giới của kết quả dự đoán (Với _k_ = 20).</p></center>

Tuy nhiên, khi tăng _k_ quá lớn, tới giá trị _k_ = 80, ranh giới phân chia trở nên quá mượt, không thể phân biệt được cá nhân nào thuộc Đảng Cộng Hòa hay Dân Chủ và đường rang giới dự đoán không thể đem lại một kết quả chính xác được.

<center><img src="/img/bias_variance/k-80.PNG" alt="img" style="width: 609px;"/></center>
<center><p>Hình 8: Phân chia ranh giới của kết quả dự đoán (Với _k_ = 80).</p></center>

Đường phân chia ranh giới không mượt hay xuất hiện các "island" chính là dấu hiệu của variance. Mặt khác, đường phân chia quá mượt chính là dấu hiệu của bias.

Ta dễ dàng nhận thấy được khi tăng _k_ sẽ dẫn đến tăng bias và giảm variance. Trong khi giảm _k_ sẽ dẫn đến điều ngược lại. Nếu có thể, bạn đọc nên thực hiện trên nhiều tập dữ liệu khác nhau thể thấy được tính tự nhiên này của __Bias-Variance Tradeoff__.

<a name="-phan-tich-bias-variance">

#### 3.3. Phân tích bias và variance

Trong thuật toán _k_-NN chúng ta có thể tính toán tổng sai số như sau:

<div style="text-align:center" markdown="1">
\\(Err(x) = \left(f(x)-\frac{1}{k}\sum\limits_{i=1}^k f(x_i)\right)^2+\frac{\sigma_\epsilon^2}{k} + \sigma_\epsilon^2\\)

\\(Err(x) = \mathrm{Bias}^2 + \mathrm{Variance} + \mathrm{Irreducible\ Error}\\)
</div>






