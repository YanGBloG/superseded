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

<div class="content-node image"><div class="image-content">    
    <table class="snug" align="center">
        <tbody>
        	<tr>
        		<th class="r90">Religiousness</th>
        		<td>
        			<div id="chart_rawdata_knn" class="knn_chart">
        				<svg width="600" height="400" class="RdBu">
        					<circle r="5" class="q0-9" transform="translate(492.1939697265625,199.24085998535156)"></circle>
        					<circle r="5" class="q0-9" transform="translate(41.277313232421875,38.01535415649414)"></circle>
        					<circle r="5" class="q8-9" transform="translate(463.0407409667969,236.74703979492188)"></circle>
        					<circle r="5" class="q8-9" transform="translate(338.7109375,207.85240173339844)"></circle>
        					<circle r="5" class="q8-9" transform="translate(61.01599884033203,331.3340148925781)"></circle>
        					<circle r="5" class="q8-9" transform="translate(63.94195556640625,158.50253295898438)"></circle>
        					<circle r="5" class="q8-9" transform="translate(184.0235137939453,283.739013671875)"></circle>
        					<circle r="5" class="q8-9" transform="translate(199.14537048339844,327.7568359375)"></circle>
        					<circle r="5" class="q8-9" transform="translate(496.7530517578125,374.82012939453125)"></circle>
        					<circle r="5" class="q0-9" transform="translate(479.40472412109375,251.28416442871094)"></circle>
        					<circle r="5" class="q8-9" transform="translate(46.534584045410156,371.33074951171875)"></circle>
        					<circle r="5" class="q0-9" transform="translate(53.27717208862305,20.52057647705078)"></circle>
        					<circle r="5" class="q0-9" transform="translate(235.30166625976562,235.4990692138672)"></circle>
        					<circle r="5" class="q0-9" transform="translate(117.60407257080078,55.628902435302734)"></circle>
        					<circle r="5" class="q0-9" transform="translate(392.0682373046875,21.42414093017578)"></circle>
        					<circle r="5" class="q8-9" transform="translate(90.65819549560547,268.73529052734375)"></circle>
        					<circle r="5" class="q0-9" transform="translate(403.6700134277344,304.0859069824219)"></circle>
        					<circle r="5" class="q8-9" transform="translate(34.500770568847656,274.3841247558594)"></circle>
        					<circle r="5" class="q8-9" transform="translate(87.38031005859375,354.0915832519531)"></circle>
        					<circle r="5" class="q0-9" transform="translate(544.7617797851562,93.47618865966797)"></circle>
        					<circle r="5" class="q0-9" transform="translate(182.7562713623047,89.41451263427734)"></circle>
        					<circle r="5" class="q8-9" transform="translate(483.5508728027344,298.5349426269531)"></circle>
        					<circle r="5" class="q0-9" transform="translate(453.55120849609375,24.839033126831055)"></circle>
        					<circle r="5" class="q8-9" transform="translate(326.82147216796875,241.4149169921875)"></circle>
        					<circle r="5" class="q8-9" transform="translate(229.1647491455078,235.63323974609375)"></circle>
        					<circle r="5" class="q0-9" transform="translate(343.154541015625,75.55409240722656)"></circle>
        					<circle r="5" class="q0-9" transform="translate(79.63373565673828,77.7381362915039)"></circle>
        					<circle r="5" class="q8-9" transform="translate(299.98248291015625,365.9923095703125)"></circle>
        					<circle r="5" class="q0-9" transform="translate(371.7185363769531,62.3734130859375)"></circle>
        					<circle r="5" class="q0-9" transform="translate(542.741943359375,106.87908935546875)"></circle>
        					<circle r="5" class="q8-9" transform="translate(63.34486389160156,342.9246826171875)"></circle>
        					<circle r="5" class="q0-9" transform="translate(203.39825439453125,189.7144317626953)"></circle>
        					<circle r="5" class="q8-9" transform="translate(241.31497192382812,207.5205841064453)"></circle>
        					<circle r="5" class="q8-9" transform="translate(222.06427001953125,280.3869934082031)"></circle>
        					<circle r="5" class="q8-9" transform="translate(299.4081726074219,368.1298828125)"></circle>
        					<circle r="5" class="q8-9" transform="translate(299.2140197753906,274.07659912109375)"></circle>
        					<circle r="5" class="q0-9" transform="translate(490.3083190917969,81.23583984375)"></circle>
        					<circle r="5" class="q8-9" transform="translate(430.3426513671875,214.74851989746094)"></circle>
        					<circle r="5" class="q8-9" transform="translate(349.3872375488281,117.28694152832031)"></circle>
        					<circle r="5" class="q8-9" transform="translate(175.8174285888672,353.39892578125)"></circle>
        					<circle r="5" class="q0-9" transform="translate(570.575927734375,35.584983825683594)"></circle>
        					<circle r="5" class="q0-9" transform="translate(533.6995239257812,280.29742431640625)"></circle>
        					<circle r="5" class="q0-9" transform="translate(460.73095703125,128.9247589111328)"></circle>
        					<circle r="5" class="q8-9" transform="translate(98.0711441040039,247.55484008789062)"></circle>
        					<circle r="5" class="q8-9" transform="translate(286.7738952636719,95.5040512084961)"></circle>
        					<circle r="5" class="q0-9" transform="translate(41.88449478149414,87.62808227539062)"></circle>
        					<circle r="5" class="q8-9" transform="translate(463.1479797363281,174.11895751953125)"></circle>
        					<circle r="5" class="q8-9" transform="translate(445.68035888671875,323.7693176269531)"></circle>
        					<circle r="5" class="q8-9" transform="translate(460.5453186035156,233.65042114257812)"></circle>
        					<circle r="5" class="q0-9" transform="translate(138.59002685546875,104.2143783569336)"></circle>
        					<circle r="5" class="q0-9" transform="translate(238.8720245361328,96.55712127685547)"></circle>
        					<circle r="5" class="q0-9" transform="translate(546.7451171875,44.48590087890625)"></circle>
        					<circle r="5" class="q0-9" transform="translate(188.1507568359375,158.98707580566406)"></circle>
        					<circle r="5" class="q0-9" transform="translate(465.7481384277344,173.49327087402344)"></circle>
        					<circle r="5" class="q0-9" transform="translate(528.0020751953125,172.5897979736328)"></circle>
        					<circle r="5" class="q0-9" transform="translate(457.9385070800781,139.91033935546875)"></circle>
        					<circle r="5" class="q8-9" transform="translate(354.7146301269531,159.19662475585938)"></circle>
        					<circle r="5" class="q8-9" transform="translate(391.6455383300781,202.49876403808594)"></circle>
        					<circle r="5" class="q8-9" transform="translate(443.2760009765625,373.2785949707031)"></circle>
        					<circle r="5" class="q8-9" transform="translate(87.19535827636719,211.9920654296875)"></circle>
        					<circle r="5" class="q8-9" transform="translate(302.1697082519531,198.36839294433594)"></circle>
        					<circle r="5" class="q8-9" transform="translate(217.9697265625,23.31383514404297)"></circle>
        					<circle r="5" class="q0-9" transform="translate(395.8767395019531,22.722166061401367)"></circle>
        					<circle r="5" class="q8-9" transform="translate(471.37933349609375,221.81716918945312)"></circle>
        					<circle r="5" class="q0-9" transform="translate(456.6429138183594,150.89186096191406)"></circle>
        					<circle r="5" class="q8-9" transform="translate(281.1766052246094,363.0153503417969)"></circle>
        					<circle r="5" class="q0-9" transform="translate(129.83004760742188,115.98701477050781)"></circle>
        					<circle r="5" class="q8-9" transform="translate(248.09552001953125,310.2545471191406)"></circle>
        					<circle r="5" class="q8-9" transform="translate(267.7306213378906,256.0012512207031)"></circle>
        					<circle r="5" class="q8-9" transform="translate(503.8079528808594,307.702880859375)"></circle>
        					<circle r="5" class="q0-9" transform="translate(359.4011535644531,85.88597869873047)"></circle>
        					<circle r="5" class="q8-9" transform="translate(66.51846313476562,288.3641052246094)"></circle>
        					<circle r="5" class="q0-9" transform="translate(505.07562255859375,187.4217987060547)"></circle>
        					<circle r="5" class="q8-9" transform="translate(25.364213943481445,102.55750274658203)"></circle>
        					<circle r="5" class="q8-9" transform="translate(526.5156860351562,320.646240234375)"></circle>
        					<circle r="5" class="q0-9" transform="translate(169.91429138183594,123.78865051269531)"></circle>
        					<circle r="5" class="q0-9" transform="translate(333.4569091796875,49.331241607666016)"></circle>
        					<circle r="5" class="q0-9" transform="translate(106.98843383789062,107.00733947753906)"></circle>
        					<circle r="5" class="q8-9" transform="translate(468.4338684082031,264.2528381347656)"></circle>
        					<circle r="5" class="q8-9" transform="translate(102.01782989501953,223.71153259277344)"></circle>
        					<circle r="5" class="q8-9" transform="translate(484.446044921875,240.8489227294922)"></circle>
        					<circle r="5" class="q8-9" transform="translate(87.84510040283203,189.85060119628906)"></circle>
        					<circle r="5" class="q8-9" transform="translate(496.26214599609375,312.71136474609375)"></circle>
        					<circle r="5" class="q8-9" transform="translate(400.3122253417969,149.65794372558594)"></circle>
        					<circle r="5" class="q0-9" transform="translate(115.96427154541016,165.25311279296875)"></circle>
        					<circle r="5" class="q8-9" transform="translate(35.45072937011719,167.74996948242188)"></circle>
        					<circle r="5" class="q8-9" transform="translate(262.7864990234375,107.24049377441406)"></circle>
        					<circle r="5" class="q0-9" transform="translate(148.0567626953125,130.81072998046875)"></circle>
        					<circle r="5" class="q0-9" transform="translate(483.81048583984375,255.5757598876953)"></circle>
        					<circle r="5" class="q0-9" transform="translate(528.1555786132812,70.51458740234375)"></circle>
        					<circle r="5" class="q8-9" transform="translate(237.88682556152344,46.45689010620117)"></circle>
        					<circle r="5" class="q8-9" transform="translate(396.8204650878906,372.3489685058594)"></circle>
        					<circle r="5" class="q0-9" transform="translate(22.547168731689453,232.76669311523438)"></circle>
        					<circle r="5" class="q0-9" transform="translate(555.05615234375,125.5079116821289)"></circle>
        					<circle r="5" class="q0-9" transform="translate(570.7529907226562,62.965824127197266)"></circle>
        					<circle r="5" class="q0-9" transform="translate(556.2977905273438,351.1795349121094)"></circle>
        					<circle r="5" class="q8-9" transform="translate(220.56419372558594,147.11245727539062)"></circle>
        					<circle r="5" class="q0-9" transform="translate(475.1058044433594,86.54938507080078)"></circle>
        					<circle r="5" class="q8-9" transform="translate(293.83984375,373.2276306152344)"></circle>
        					<circle r="5" class="q8-9" transform="translate(338.9353332519531,251.5997772216797)"></circle>
        					<circle r="5" class="q8-9" transform="translate(276.5592041015625,257.11260986328125)"></circle>
        					<circle r="5" class="q8-9" transform="translate(389.1197204589844,288.9963073730469)"></circle>
        					<circle r="5" class="q8-9" transform="translate(149.27972412109375,303.0163269042969)"></circle>
        					<circle r="5" class="q8-9" transform="translate(559.0577392578125,364.5559997558594)"></circle>
        					<circle r="5" class="q8-9" transform="translate(331.72119140625,296.37628173828125)"></circle>
        					<circle r="5" class="q0-9" transform="translate(95.77204895019531,247.94696044921875)"></circle>
        					<circle r="5" class="q8-9" transform="translate(41.61444091796875,372.7494812011719)"></circle>
        					<circle r="5" class="q0-9" transform="translate(441.72735595703125,86.87793731689453)"></circle>
        					<circle r="5" class="q0-9" transform="translate(140.7775421142578,75.46820068359375)"></circle>
        					<circle r="5" class="q8-9" transform="translate(182.0389862060547,276.8058166503906)"></circle>
        					<circle r="5" class="q0-9" transform="translate(202.5406036376953,216.5498809814453)"></circle>
        					<circle r="5" class="q8-9" transform="translate(299.04315185546875,168.8763885498047)"></circle>
        					<circle r="5" class="q0-9" transform="translate(529.181396484375,297.0206604003906)"></circle>
        					<circle r="5" class="q8-9" transform="translate(139.98130798339844,377.7989807128906)"></circle>
        					<circle r="5" class="q8-9" transform="translate(111.42061614990234,108.31428527832031)"></circle>
        					<circle r="5" class="q8-9" transform="translate(151.09185791015625,242.54393005371094)"></circle>
        					<circle r="5" class="q0-9" transform="translate(368.9268798828125,24.75046157836914)"></circle>
        					<circle r="5" class="q0-9" transform="translate(536.3154296875,252.55616760253906)"></circle>
        					<circle r="5" class="q8-9" transform="translate(452.62371826171875,256.2213439941406)"></circle>
        					<circle r="5" class="q0-9" transform="translate(225.11679077148438,203.98851013183594)"></circle>
        					<circle r="5" class="q8-9" transform="translate(182.08050537109375,325.4248962402344)"></circle>
        					<circle r="5" class="q8-9" transform="translate(353.0858459472656,146.5047149658203)"></circle>
        					<circle r="5" class="q0-9" transform="translate(434.111572265625,326.67401123046875)"></circle>
        					<circle r="5" class="q8-9" transform="translate(434.906494140625,187.9200897216797)"></circle>
        					<circle r="5" class="q0-9" transform="translate(380.0408020019531,324.248779296875)"></circle>
        					<circle r="5" class="q8-9" transform="translate(299.91339111328125,339.29681396484375)"></circle>
        					<circle r="5" class="q0-9" transform="translate(575.4949951171875,239.56126403808594)"></circle>
        					<circle r="5" class="q8-9" transform="translate(354.6059265136719,352.96917724609375)"></circle>
        					<circle r="5" class="q8-9" transform="translate(248.9258270263672,296.1717224121094)"></circle>
        					<circle r="5" class="q8-9" transform="translate(465.7021179199219,313.189453125)"></circle>
        					<circle r="5" class="q0-9" transform="translate(166.57713317871094,21.030960083007812)"></circle>
        					<circle r="5" class="q0-9" transform="translate(95.28401947021484,162.99789428710938)"></circle>
        					<circle r="5" class="q0-9" transform="translate(173.1535186767578,183.5015411376953)"></circle>
        					<circle r="5" class="q0-9" transform="translate(120.80987548828125,99.61750030517578)"></circle>
        					<circle r="5" class="q0-9" transform="translate(33.54658889770508,114.09160614013672)"></circle>
        					<circle r="5" class="q8-9" transform="translate(430.86700439453125,269.39971923828125)"></circle>
        					<circle r="5" class="q0-9" transform="translate(215.43499755859375,199.58534240722656)"></circle>
        					<circle r="5" class="q8-9" transform="translate(473.8622741699219,228.45526123046875)"></circle>
        					<circle r="5" class="q8-9" transform="translate(331.2964172363281,355.81427001953125)"></circle>
        					<circle r="5" class="q8-9" transform="translate(298.1474304199219,208.82431030273438)"></circle>
        					<circle r="5" class="q0-9" transform="translate(566.571533203125,236.34466552734375)"></circle>
        					<circle r="5" class="q0-9" transform="translate(346.45867919921875,69.40186309814453)"></circle>
        					<circle r="5" class="q0-9" transform="translate(189.14517211914062,117.88835144042969)"></circle>
        					<circle r="5" class="q0-9" transform="translate(166.14617919921875,69.12361145019531)"></circle>
        					<circle r="5" class="q0-9" transform="translate(497.62506103515625,84.65994262695312)"></circle>
        					<circle r="5" class="q0-9" transform="translate(375.1168518066406,37.54997634887695)"></circle>
        					<circle r="5" class="q8-9" transform="translate(140.68917846679688,358.8636169433594)"></circle>
        					<circle r="5" class="q8-9" transform="translate(347.2258605957031,261.93585205078125)"></circle>
        					<circle r="5" class="q0-9" transform="translate(169.5237274169922,100.87321472167969)"></circle>
        					<circle r="5" class="q0-9" transform="translate(395.77569580078125,79.0986328125)"></circle>
        					<circle r="5" class="q0-9" transform="translate(378.5339050292969,68.93370056152344)"></circle>
        					<circle r="5" class="q8-9" transform="translate(136.6710662841797,62.36529541015625)"></circle>
        					<circle r="5" class="q0-9" transform="translate(445.03387451171875,33.4532585144043)"></circle>
        					<circle r="5" class="q0-9" transform="translate(465.58831787109375,200.67352294921875)"></circle>
        					<circle r="5" class="q8-9" transform="translate(271.95452880859375,235.83436584472656)"></circle>
        					<circle r="5" class="q8-9" transform="translate(267.9061279296875,270.6490783691406)"></circle>
        					<circle r="5" class="q8-9" transform="translate(24.31011390686035,310.4570617675781)"></circle>
        					<circle r="5" class="q8-9" transform="translate(272.7624816894531,246.74542236328125)"></circle>
        					<circle r="5" class="q0-9" transform="translate(370.9999694824219,89.14434814453125)"></circle>
        					<circle r="5" class="q8-9" transform="translate(375.7814636230469,207.64511108398438)"></circle>
        					<circle r="5" class="q8-9" transform="translate(281.4026794433594,290.4798889160156)"></circle>
        					<circle r="5" class="q0-9" transform="translate(54.108299255371094,59.19814682006836)"></circle>
        					<circle r="5" class="q8-9" transform="translate(387.88092041015625,211.8555145263672)"></circle>
        					<circle r="5" class="q8-9" transform="translate(350.8575744628906,173.6025848388672)"></circle>
        					<circle r="5" class="q0-9" transform="translate(502.1966247558594,265.15411376953125)"></circle>
        					<circle r="5" class="q8-9" transform="translate(87.32137298583984,236.05125427246094)"></circle>
        					<circle r="5" class="q0-9" transform="translate(405.4254455566406,33.89897918701172)"></circle>
        					<circle r="5" class="q0-9" transform="translate(322.5069580078125,117.27385711669922)"></circle>
        					<circle r="5" class="q0-9" transform="translate(568.90234375,289.54400634765625)"></circle>
        					<circle r="5" class="q0-9" transform="translate(499.20172119140625,75.82920837402344)"></circle>
        					<circle r="5" class="q0-9" transform="translate(265.84857177734375,59.455989837646484)"></circle>
        					<circle r="5" class="q8-9" transform="translate(123.64678955078125,360.34051513671875)"></circle>
        					<circle r="5" class="q0-9" transform="translate(166.49551391601562,21.817346572875977)"></circle>
        					<circle r="5" class="q8-9" transform="translate(378.2764892578125,356.90350341796875)"></circle>
        					<circle r="5" class="q0-9" transform="translate(216.76722717285156,223.9311981201172)"></circle>
        					<circle r="5" class="q0-9" transform="translate(337.97467041015625,84.76957702636719)"></circle>
        					<circle r="5" class="q0-9" transform="translate(243.56332397460938,160.54934692382812)"></circle>
        					<circle r="5" class="q8-9" transform="translate(120.55567932128906,265.2567138671875)"></circle>
        					<circle r="5" class="q0-9" transform="translate(65.74116516113281,79.61673736572266)"></circle>
        					<circle r="5" class="q0-9" transform="translate(459.7825012207031,118.3598861694336)"></circle>
        					<circle r="5" class="q0-9" transform="translate(189.94607543945312,140.02113342285156)"></circle>
        					<circle r="5" class="q8-9" transform="translate(304.4588928222656,104.10541534423828)"></circle>
        					<circle r="5" class="q0-9" transform="translate(261.3569030761719,270.5807800292969)"></circle>
        					<circle r="5" class="q8-9" transform="translate(279.62353515625,360.4432067871094)"></circle>
        					<circle r="5" class="q0-9" transform="translate(240.43460083007812,88.80514526367188)"></circle>
        					<circle r="5" class="q0-9" transform="translate(149.41082763671875,22.48920249938965)"></circle>
        					<circle r="5" class="q0-9" transform="translate(523.6578979492188,34.55793380737305)"></circle>
        					<circle r="5" class="q0-9" transform="translate(474.19281005859375,109.02759552001953)"></circle>
        					<circle r="5" class="q0-9" transform="translate(205.18589782714844,212.4634246826172)"></circle>
        					<circle r="5" class="q0-9" transform="translate(416.6171569824219,62.990596771240234)"></circle>
        					<circle r="5" class="q8-9" transform="translate(38.19607925415039,250.56129455566406)"></circle>
        					<circle r="5" class="q0-9" transform="translate(304.1872253417969,120.23667907714844)"></circle>
        					<circle r="5" class="q0-9" transform="translate(493.12664794921875,148.14089965820312)"></circle>
        					<circle r="5" class="q0-9" transform="translate(26.939172744750977,321.69110107421875)"></circle>
        					<circle r="5" class="q8-9" transform="translate(20.564626693725586,36.26818084716797)"></circle>
        					<circle r="5" class="q8-9" transform="translate(79.79217529296875,202.5304718017578)"></circle>
        					<circle r="5" class="q0-9" transform="translate(508.4207458496094,60.40113067626953)"></circle>
        					<circle r="5" class="q0-9" transform="translate(576.4546508789062,233.82789611816406)"></circle>
        					<circle r="5" class="q0-9" transform="translate(196.57908630371094,142.49337768554688)"></circle>
        					<circle r="5" class="q8-9" transform="translate(270.008544921875,22.246728897094727)"></circle>
        				</svg>
    				</div>
				</td>
			</tr>
        	<tr>
        		<th></th>
        		<th>Wealth</th>
        	</tr>
    	</tbody>
	</table>  
</div>
	<center><div class="caption">Hình 2: Đăng kí cử tri (Tôn giáo (trục y) vs độ giàu có (trục x)).</div></center>
</div>






