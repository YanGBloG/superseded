---
layout: post
title: 37 lý do mạng neuron nhân tạo không hoạt động
tags : [machine learning]
---

<div class="block">
	<center>
		<img src="{{ site.baseurl }}/img/nnsheader.png" alt="Img">
	</center>
</div> 

### Nội dung bài viết
<!-- TOC -->
### <a href="#-cac-van-de-ve-tap-du-lieu"> I. Các vấn đề về tập dữ liệu</a>
### <a href="#-cac-van-de-ve-tang-cuong"> II. Các vấn đề về chuẩn hóa và tăng cường dữ liệu</a>
### <a href="#-cac-van-de-ve-trien-khai"> III. Các vấn đề về triển khai</a>
### <a href="#-cac-van-de-ve-huan-luyen"> IV. Các vấn đề về huấn luyện</a>
<!-- END TOC -->

Bài viết này được dịch từ một bài trên medium.

Sau khi bạn huấn luyện một mô hình trong một thời gian dài, đồ thị thể hiện mất mát trên cả tập huấn luyện và tập thử trông rất tuyệt vời, 
nhưng khi tiến hành dự đoán lại đưa ra một kết quả xấu, có thể kết quả phân loại hoàn toàn trả về không, hoặc tồi tệ hơn nữa là 
chẳng có gì được trả về. Bạn tự hỏi điều gì đang xảy ra vậy ? Thực sự có rất nhiều lý do cho vấn đề này.

Dựa trên kinh nghiệm của tác giả bài viết, anh ấy đã đưa ra một số nguyên nhân điển hình xoay quanh việc model hoạt động không đúng 
như mong muốn.

Các vấn đề này được tác giả chia làm bốn nhóm chính bao gồm:

	  - Các vấn đề về tập dữ liệu,
	  - Các vấn đề về chuẩn hóa và tăng cường dữ liệu (Normalization and Augmentation),
	  - Các vấn đề về triển khai,
	  - Các vấn đề về huấn luyện.
  
<a href="-cac-van-de-ve-tap-du-lieu">
  
### I. Các vấn đề về tập dữ liệu:

##### 1. Sai sót tại dữ liệu đâu vào

Kiểm tra xem dữ liệu đầu vào bạn cung cấp cho mô hình có hợp lý hay không ? Ví dụ, nhầm lẫn giữa chiều rộng và cao của hình ảnh, 
hay sử dụng một tập con dữ liệu (batch) nhiều lần... Vì vậy, cần phải in các cặp dữ liệu đầu vào - đầu ra để có thể chắc chăn rằng 
không có vấn đề gì xảy ra với chúng.

##### 2. Sử dụng dữ liệu đầu vào ngẫu nhiên

Thay vì sử dụng dữ liệu thực tế ban đầu, hãy có gắng sử dụng tập hợp các điểm dữ liệu ngẫu nhiên để có thể xem xét lỗi có xảy ra theo 
cùng một cách hay không. Nếu điều đó xảy ra, có lẽ mô hình của bạn đang biến một số điểm dữ liệu thành "rác". Hãy có gắng gỡ lỗi theo
từng lớp, từng hàm tối ưu để có thể thấy được điều đang diễn ra trong mô hình.

##### 3. Sai sót tại công cụ tải dữ liệu (data loader)

Sau khi kiểm tra toàn bộ dữ liệu đầu vào mà vẫn không tìm được nguyên nhân gây lỗi, có thể vấn đề nằm ở phần code tải dữ liệu vào 
mô hình. In ra dữ liệu đầu vào của lớp đầu tiên trước khi thực hiện các tác vụ khác để có thể kiểm tra vấn đề này.

##### 4. Sai nhãn dữ liệu

Kiểm tra dữ liệu có bị gắn sai nhãn hay không, đồng thời chắc chắn rằng quá trình trộn dữ liệu không làm thay đổi nhãn của dữ liệu.

##### 5. Mối quan hệ giữa đầu vào và đầu ra của dữ liệu không thích hợp

Có thể mối quan hệ có điều kiện giữa đầu vào và đầu ra của bộ dữ liệu quá ít so với mối quan hệ ngẫu nhiên. Thực tế rất khó để xác 
định điều này vì nó phụ thuộc vào bản chất của bộ dữ liệu.

##### 6. Bộ dữ liệu chứa quá nhiều nhiễu (Noise)

Điều này thường xuyên xảy ra đối với các bộ dữ liệu thô, kiểm tra lại các dữ liệu đầu vào bằng cách thủ công và cố gắng gắn lại nhãn 
hoặc loại bỏ các điểm nhiễu.

##### 7. Không thực hiện trộn tập dữ liệu

Trộn tập dữ liệu sẽ tránh được các ảnh hưởng xấu của bản chất dữ liệu lên quá trình huấn luyện

##### 8. Các lớp dữ liệu không cân bằng

Giả sử tập dữ liệu có 1000 mẫu dữ liệu được gắn nhãn A so với chỉ một mẫu được gắn nhãn B, bạn cần phải thực hiện [cân bằng dữ liệu](https://machinelearningmastery.com/tactics-to-combat-imbalanced-classes-in-your-machine-learning-dataset/) 
để có thể đặt kết quả tốt hơn.

##### 9. Không đủ dữ liệu cho quá trình huấn luyện

Nếu bạn đang thực hiện huấn luyện một mô hình thô (Chưa có sự tinh chỉnh về các thông số) bạn cần phải có rất nhiều dữ liệu để có thể 
đạt kết quả tốt.

##### 10. Tập con chứa các dữ liệu gắn cùng một nhãn

Điều này có thể xảy ra khi thực hiện sắp xếp dữ liệu, bạn phải chắc chắn được rằng điều này không xảy ra trong quá trình huấn luyện.

##### 11. Kích thước tập con quá lớn

Khi kích thước tập con quá lớn sẽ làm giảm tính tổng quát hóa của mô hình (Tham khảo [On Large-Batch Training for Deep Learning](https://arxiv.org/abs/1609.04836)).

Ngoài ra, có một cách khác để tránh được một số rắc rối đã nêu, đó là sử dụng những bộ dữ liệu chuẩn cho những mô hình mới trước khi sử dụng dữ liệu của bạn.

<a href="-cac-van-de-ve-tang-cuong">

### II. Các vấn đề về chuẩn hóa và tăng cường dữ liệu:

##### 12. Thuộc tính không được chuẩn hóa

Chuẩn hóa các thuộc tính để đưa dữ liệu có cùng giá trị trung bình và phương sai.

##### 13. Tăng cường quá nhiều dữ liệu

Điều này có thể làm cho mô hình không khớp (Underfit).

##### 14. Sai sót khi thực hiện tiền xử của các mô hình pretrained

Nếu bạn sử dụng các mô hình pretrained phải chắc chắn được rằng dữ liệu của mô hình pretrained cũng được chuẩn hóa theo mô hình của bạn.

##### 15. Quá trình tiền xử lý của các tập huấn luyện, tập kiểm thử và tập thử có sai sót

"Mọi quá trình tiền xử lý chỉ nên tính toán trên tập huấn luyện sau đó áp dụng cho các tập kiểm thử và tập thử". [Common pitfall](http://cs231n.github.io/neural-networks-2/#datapre)

Đồng thời kiểm tra quá trình tiền xử lý trên các tập con.

<a href="-cac-van-de-ve-trien-khai">

### III. Các vấn đề về triển khai:

##### 16. Phương pháp giải quyết vấn đề quá phức tạp

Giải quyết bằng cách đưa vấn đề về dạng đơn giản hơn, điều này giúp bạn nhanh chóng tìm thấy vấn đề nằm ở đâu. Ví dụ, nếu dữ liệu được gắn nhãn ở cả dạng chữ và số, hãy cố gắng thực hiện việc dự đoán trên một trong hai dạng đó.

##### 17. Tính toán hàm loss

Cố gắng tính toán chính xác hàm loss (softmax, sigmoid...) tại một điểm nào đó bằng cách khởi chạy mô hình với một lượng nhỏ các thông số đồng thời không thực hiện quy chuẩn hóa (regulaiazation) và tính toán loss thông qua các hàm loss đã chọn.

##### 18. Hàm loss không đúng

Nếu bạn không sử dụng các hàm loss mặc định, bạn cần kiểm tra lại lỗi, đơn vị của hàm. Việc sử dụng hàm loss tự định nghĩa thường dẫn đến nhiều sai sót trong quá trình huấn luyện do hàm loss không chuẩn xác.

##### 19. Loss input không chính xác

Nếu bạn sử dụng các hàm loss mặc định, cần chắc chắn rằng những gì đưa vào tính toán trong hàm loss không bị sai lệch. Ví dụ hàm loss BinaryCrossEntropy cần các input là output của hàm softmax.

##### 20. Loss weights không chính xác

Nếu hàm loss của bạn là một tổ hợp của các hàm loss khác, cần xác định chính xác độ lớn (weights) của mỗi hàm loss bằng cách thử sai.

##### 21. Phương pháp đánh giá (metric) không phù hợp

Thay đổi một số metric khác nhau để tìm được metric phù hợp nhất.

##### 22. Vấn đề tại các lớp tự định nghĩa

Kiểm tra lại tất cả các lớp trong mô hình do bạn tự định nghĩa, chắc chắn rằng tất cả đều hoạt động một cách chuẩn xác.

##### 23. Vấn đề tại các lớp hoặc biến không được kích hoạt

Nếu trong mô hình xuất hiện các biến, lớp không được kích hoạt cần kiểm tra lại các thành phần này.

##### 24. Kích thước mô hình không đủ lớn

Kích thước mô hình không đủ lớn đối với vấn đề bạn đang giải quyết, bạn nên xem xét thêm vào một số lớp và node ẩn.

##### 25. Lỗi tại các chiều ẩn

##### 26. Sai sót khi sử dụng các thuật toán Gradient descent

Nếu bạn triển khai thuật toán gradient descent cho mo hình của mình, cần phải chắn chắn được thuật toán gradient hoạt động một cách trơ tru (Tham khảo [1](http://ufldl.stanford.edu/tutorial/supervised/DebuggingGradientChecking/), [2](http://cs231n.github.io/neural-networks-3/#gradcheck), [3](https://www.coursera.org/learn/machine-learning/lecture/Y3s6r/gradient-checking)).

<a href="-cac-van-de-ve-huan-luyen">

### IV. Các vấn đề về huấn luyện:

##### 27. Bài toán cần xử lý có tập dữ liệu quá nhỏ

##### 28. Khởi tạo trọng số không phù hợp

Trọng số không phù hợp thường đưa ra kết quả tại các điểm local minimum, thay đổi giá trị khởi tạo và huấn luyện lại mô hình (tham khảo một số phương pháp khởi tạo [Xavier](http://proceedings.mlr.press/v9/glorot10a/glorot10a.pdf), [He](http://www.cv-foundation.org/openaccess/content_iccv_2015/papers/He_Delving_Deep_into_ICCV_2015_paper.pdf))

##### 29. Lỗi tại các siêu tham số (hyper-parameters)

Sử dụng [Grid Search](http://scikit-learn.org/stable/modules/grid_search.html) hoặc [Random Search](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.RandomizedSearchCV.html) để giải quyết vấn đề.

##### 30. Regularization quá lớn

Regularization thường làm cho mô hình kém khớp (underfitting). Thực hiện một số phương pháp như dropout, batch-norm... để giảm regularization.

##### 31. Thiếu thời gian huấn luyện

Tăng thêm thời gian huấn luyện cho mô hình (thêm epochs) nếu thấy loss đang giảm mạnh.

##### 32. Ứng xử bất thường giữa trạng thái huấn luyện và trạng thái kiểm thử

Thay đổi qua lại giữa hai trạng thái

##### 33. Các tham số như trọng số, hàm kích hoạt, ... không đúng với input

Thể hiện quá trình huấn luyện lên đồ thị, tìm kiếm các điểm không thích hợp và xử lý.

##### 34. Hàm tối ưu không phù hợp

Thay đổi, sử dụng các hàm tối ưu khác nhau. Tham khảo [Sebastian Ruder](http://ruder.io/optimizing-gradient-descent/) để hiểu thêm về các hàm tối ưu.

##### 35. Xuất hiện hiện tượng tiêu biến gradient (vanishing gradient)

Kiểm tra lại các lớp, giá trị đầu vào của một lớp quá lớn thường dễ xảy ra hiện tượng tiêu biến gradient đồng thời thay đổi hàm kích hoạt. Sử dụng các ham ReLU, LeakyReLU thay cho Tanh, Sigmoid (là các hàm dễ gây tiêu biến gradient).

##### 36. Tốc độ học (learning rate) không phù hợp

Learning rate thấp làm mô hình khó hội tụ hoặc hội tụ chậm. Ngược lại, learning rate cao mô hình nhanh hội tụ nhưng tốn nhiều thời gian để tìm lời giải tốt nhất cho bài toán.

##### 37. Xuất hiện các giá trị NaNs

- Giảm learning rate

- Kiểm tra các phép toán chia cho 0, logarit tự nhiên của 0 hoặc số âm có xuất hiện trong mô hình hay không

- Tham khảo [Handle NaNs](http://russellsstewart.com/notes/0.html)

