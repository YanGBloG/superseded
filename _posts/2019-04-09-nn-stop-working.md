---
layout: post
title: 37 lý do mạng neuron nhân tạo không hoạt động
tags : [machine learning]
---

<!-- <div class="block">
	<center>
		<img src="{{ site.baseurl }}/img/tutheader_spatial.png" alt="Img">
	</center>
</div>  -->

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
  
### I. Các vấn đề về tập dữ liệu:

##### 1. Kiểm tra dữ liệu đầu vào

Kiểm tra xem dữ liệu đầu vào bạn cung cấp cho mô hình có hợp lý hay không ? Ví dụ, nhầm lẫn giữa chiều rộng và cao của hình ảnh, 
hay sử dụng một tập con dữ liệu (batch) nhiều lần... Vì vậy, cần phải in các cặp dữ liệu đầu vào - đầu ra để có thể chắc chăn rằng 
không có vấn đề gì xảy ra với chúng.

##### 2. Sử dụng dữ liệu đầu vào ngẫu nhiên

Thay vì sử dụng dữ liệu thực tế ban đầu, hãy có gắng sử dụng tập hợp các điểm dữ liệu ngẫu nhiên để có thể xem xét lỗi có xảy ra theo 
cùng một cách hay không. Nếu điều đó xảy ra, có lẽ mô hình của bạn đang biến một số điểm dữ liệu thành "rác". Hãy có gắng gỡ lỗi theo
từng lớp, từng hàm tối ưu để có thể thấy được điều đang diễn ra trong mô hình.

##### 3. Kiểm tra công cụ tải dữ liệu (data loader)

Sau khi kiểm tra toàn bộ dữ liệu đầu vào mà vẫn không tìm được nguyên nhân gây lỗi, có thể vấn đề nằm ở phần code tải dữ liệu vào 
mô hình. In ra dữ liệu đầu vào của lớp đầu tiên trước khi thực hiện các tác vụ khác để có thể kiểm tra vấn đề này.

##### 4. Chắc chắn rằng dữ liệu không bị sai nhãn

Kiểm tra dữ liệu có bị gắn sai nhãn hay không, đồng thời chắc chắn rằng quá trình trộn dữ liệu không làm thay đổi nhãn của dữ liệu.

##### 5. Kiểm tra mối quan hệ giữa đầu vào và đầu ra của dữ liệu

Có thể mối quan hệ có điều kiện giữa đầu vào và đầu ra của bộ dữ liệu quá ít so với mối quan hệ ngẫu nhiên. Thực tế rất khó để xác 
định điều này vì nó phụ thuộc vào bản chất của bộ dữ liệu.

##### 6. Bộ dữ liệu chứa quá nhiều nhiễu (Noise)

Điều này thường xuyên xảy ra đối với các bộ dữ liệu thô, kiểm tra lại các dữ liệu đầu vào bằng cách thủ công và cố gắng gắn lại nhãn 
hoặc loại bỏ các điểm nhiễu.

##### 7. Trộn tập dữ liệu

Trộn tập dữ liệu sẽ tránh được các ảnh hưởng xấu của bản chất dữ liệu lên quá trình huấn luyện

##### 8. Cân bằng lớp dữ liệu

Giả sử tập dữ liệu có 1000 mẫu dữ liệu được gắn nhãn A so với chỉ một mẫu được gắn nhãn B, bạn cần phải thực hiện [cân bằng dữ liệu](https://machinelearningmastery.com/tactics-to-combat-imbalanced-classes-in-your-machine-learning-dataset/) 
để có thể đặt kết quả tốt hơn.

##### 9. Không đủ dữ liệu cho quá trình huấn luyện

Nếu bạn đang thực hiện huấn luyện một mô hình thô (Chưa có sự tinh chỉnh về các thông số) bạn cần phải có rất nhiều dữ liệu để có thể 
đạt kết quả tốt.

##### 10. Tập con chứa các dữ liệu gắn cùng một nhãn

Điều này có thể xảy ra khi thực hiện sắp xếp dữ liệu, bạn phải chắc chắn được rằng điều này không xảy ra trong quá trình huấn luyện.

##### 11. Giảm kích thước tập con

Khi kích thước tập con quá lớn sẽ làm giảm tính tổng quát hóa của mô hình (Tham khảo [On Large-Batch Training for Deep Learning](https://arxiv.org/abs/1609.04836)).

Ngoài ra, có một cách khác để tránh được một số rắc rối đã nêu, đó là sử dụng những bộ dữ liệu chuẩn cho những mô hình mới trước khi sử dụng dữ liệu của bạn.

### II. Các vấn đề về chuẩn hóa và tăng cường dữ liệu

##### 12. Chuẩn hóa các thuộc tính

Chuẩn hóa các thuộc tính để đưa dữ liệu có cùng giá trị trung bình và phương sai.

##### 13. Tăng cường quá nhiều dữ liệu

Điều này có thể làm cho mô hình không khớp (Underfit).

##### 14. Kiểm tra quá trình tiền xử của các mô hình pretrained trước khi sử dụng

Nếu bạn sử dụng các mô hình pretrained phải chắc chắn được rằng dữ liệu của mô hình pretrained cũng được chuẩn hóa theo mô hình của bạn.

##### 15. Kiểm tra lại quá trình tiền xử lý của các tập huấn luyện, tập kiểm thử và tập thử

"Mọi quá trình tiền xử lý chỉ nên tính toán trên tập huấn luyện sau đó áp dụng cho các tập kiểm thử và tập thử". [Common pitfall](http://cs231n.github.io/neural-networks-2/#datapre)

Đồng thời kiểm tra quá trình tiền xử lý trên các tập con.

### III. Các vấn đề về triển khai

##### 16. Giải quyết cùng một vấn đề nhưng ở những phiên bản đơn giản hơn

Điều này giúp bạn nhanh chóng tìm thấy vấn đề nằm ở đâu. Ví dụ, nếu dữ liệu được gắn nhãn ở cả dạng chữ và số, hãy cố gắng thực hiện 
việc dự đoán trên một trong hai dạng đó.

##### 17. Tính toán hàm loss

Cố gắng tính toán chính xác hàm loss (softmax, sigmoid...) tại một điểm nào đó bằng cách khởi chạy mô hình với một lượng nhỏ các thông số đồng thời không thực hiện quy chuẩn hóa (regulaiazation) và tính toán loss thông qua các hàm loss đã chọn.

##### 18. Kiểm tra lại hàm loss

Nếu bạn không sử dụng các hàm loss mặc định, bạn cần kiểm tra lại lỗi, đơn vị của hàm. Việc sử dụng hàm loss tự định nghĩa thường dẫn đến nhiều sai sót trong quá trình huấn luyện do hàm loss không chuẩn xác.

##### 19. Kiểm tra lại loss input

Nếu bạn sử dụng các hàm loss mặc định, cần chắc chắn rằng những gì đưa vào tính toán trong hàm loss không bị sai lệch. Ví dụ hàm loss BinaryCrossEntropy cần các input là output của hàm softmax.

##### 20. Thay đổi loss weights

Nếu hàm loss của bạn là một tổ hợp của các hàm loss khác, cần xác định chính xác độ lớn của mỗi hàm loss bằng cách thử sai.





















