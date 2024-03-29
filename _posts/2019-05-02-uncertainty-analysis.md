---
layout: post
title: Phân tích rủi ro với Well-log và minh giải địa vật lý
mathjax: true
tags : [petrophysic, data analysis]
---

### Nội dung bài viết
<!-- TOC -->
### <a href="#-gioi-thieu-chung">1. Giới thiệu chung</a>
### <a href="#-phan-tich-rui-ro-minh-giai-dia-vat-ly">2. Phân tích rủi ro trong minh giải địa vật lý</a>
#### <a href="#-interpreting-and-deriving">2.1. Phân tích rủi ro trong minh giải độ rỗng</a>
<!-- END TOC -->

Trước khi đi vào series phân tích rủi ro của mô phỏng vỉa với well log và địa vật lý, tôi xin đi vào một số lý thuyết cơ bản trước.

<a name="-gioi-thieu-chung"></a>

### 1. Giới thiệu chung

Phân tích minh giải địa vật lý là một mảng trong phân tích vỉa, kết quả minh giải sẽ trở thành các số liệu đầu vào cho quá trình xác định các tính chất và mô phỏng vỉa. Để xác định các nguồn tài nguyên nằm dưới lòng đất và các kiến thức về vỉa dầu khí, điều kiện tiên quyết là phải thu thập được các số liệu liên quan tới vỉa. Để làm được điều này, một phương pháp được đưa ra là sử dụng các thiết bị dưới lòng giếng được kết nối trực tiếp với bề mặt ghi lại một cách liên tục các thay đổi về những đặc tính của đất đá (điện trở suất, hàm lượng phóng xạ...). Từ đó các nhà địa chất học có thể thực hiện minh giải và đưa ra các tính chất của đá vỉa (độ rỗng, độ thấm...), phương pháp này được gọi là wire-line logs. Wire-line logs bao gồm nhiều phương pháp đo khác nhau, những phương pháp này có thể cung cấp các thông tin đánh giá cho giếng hay toàn vỉa.

Phương pháp đo log đầu tiên được sử dụng là đo đường log điện (electrical logging) năm 1927 cho các mỏ nhỏ tại Pháp. Cho đến ngày nay, nhiều phương pháp đo đạt và ghi chép dữ liệu được phát triển, đưa vào sử dụng cho quá trình đánh giá thành hệ. Những phương pháp phổ biến thường được sử dụng như đo hàm lượng phóng xạ (gamma-ray, GR), đo trường thế tự nhiên (spontaneous potential, SP), đo tỉ trọng (density), đo hàm lượng neutron, đo sóng siêu âm (sonic), đo cộng hưởng từ (magnetic resonance) và đo điện trở (resistivity). Dữ liệu well-log thường là nguồn cung cấp thông tin chính để đánh giá tính chất địa hình trong lòng đất khi phân tích mẫu và phân tích địa chấn không thể thực hiện được. Tuy nhiên, quá trình phân tích well-log thường mang nhiều rủi ro và giới hạn, nếu như không được xử lý đúng cách dễ dẫn tới đánh giá sai về thành hệ giếng khoan và toàn vỉa.

Đầu tiên, mọi phương pháp đo đạt đều đi kèm với rủi ro. Một vài tổ chức bao gồm Tổ chức Tiêu chuẩn Quốc tế (The International Standardization Organization), Cục đo lường trọng lượng Quốc tế (The Bureau International des Poids et Mesures), Viện Tiêu chuẩn và Công nghệ Quốc gia (The National Institute of Standardization and Technology) đều thừa nhận tính rủi ro của các phép đo. 

Thứ hai, các dụng cụ đo log không thể đo trực tiếp các tính chất địa vật lý cho mô phỏng vỉa hay đánh giá hàm lượng hydrocarbon (HC) trong vỉa. Ví dụ, hai tính chất quan trọng nhất để xác định lượng HC ban đầu trong vỉa là độ rỗng và độ bão hòa, hai tính chất này không thể đo được một cách trực tiếp mà phải thông các thuộc tính khác bằng cách sử dụng các mối quan hệ thực nghiệm.

Hầu hết các tính chất địa vật lý sử dụng trong minh giải đều thu được qua một loạt các quá trình bao gồm thu thập dữ liệu (data acquisition, measuring), xử lý số liệu (processing), hiệu chỉnh (calibration) và minh giải (interpretation). Mỗi quá trình này luôn có một độ rủi ro nhất định ảnh hưởng đến kết quả cuối cùng đạt được. Hầu hết các đường logs đều bao gồm các hiệu chỉnh cơ bản về sai số hệ thống thông qua hiệu chỉnh dụng cụ đo và môi trường đo. Do tính chất thống kê của các phép đo và độ phức tạp của giếng khoan, một số rủi ro nhất định sẽ được giữ lại trong phép đo, đặc biệt là các phép đo không thể loại bỏ hoặc định lượng các sai số trong quá trình thực hiện phép đo.

<a name="-phan-tich-rui-ro-minh-giai-dia-vat-ly"></a>

### 2. Phân tích rủi ro trong minh giải địa vật lý

Khi thực hiện đo logs các công cụ (tools) khác nhau hoặc giống nhau nhưng khác thế hệ sản xuất cần phải được hiệu chỉnh về cùng một tiêu chuẩn để có thể thống nhất số liệu đầu ra. Ví dụ như các tools đo độ rỗng hay điện trở suất cần phải hiệu chỉnh về điều kiện thành hệ hoặc điều kiện môi trường tùy theo nhà sản xuất, loại tool, thế hệ tool. Quá trình tìm kiếm các thông tin cho việc hiệu chỉnh thường tiêu tốn nhiều thời gian. Đối với các nhà phân tích, không có hiệu chỉnh phổ biến nhất, kể cả khi có cũng rất khó để xác định hiệu chỉnh đó có được sử dụng một cách đúng đắn hay không. Tuy nhiên, các hiệu chỉnh thực sự rất cần thiết, nếu như không thực hiện hoặc thực hiện không đúng cách thường dễ dẫn đến các sai số nghiêm trọng.

Trong quá trình minh giải nếu như đã có những dữ liệu khác như mẫu lõi, áp suất và thử dòng (flow tests) cần phải hiệu chỉnh và kết hợp dữ liệu đo log với các dữ liệu có sẵn đó. Đối với những giếng được đo log bằng các tools tốt, có thể dữ liệu log sẽ không giống với dữ liệu từ mẫu lõi hay các dữ liệu khác. Nếu như chỉ có dũ liệu cho một hoặc hai giếng, những nhà phân tích phải đưa ra quyết định dữ liệu đó có đại diện cho toàn vỉa hay chỉ cho một phần nhỏ của vỉa. Dữ liệu địa vật lý có thể có sự thay đổi lớn trong một vỉa, điều này dẫn tói rủi ro cho quá trình minh giải địa vật lý.

<a name="-interpreting-and-deriving"></a>

#### 2.1. Phân tích rủi ro trong minh giải độ rỗng

Độ rỗng có thể đo được bằng một vài đường logs khác nhau như sonic, neutron, density hoặc cũng có thể kết hợp các đường lại với nhau và so sánh với đồ thị phân tích mẫu lõi (core test).

<center><img src="/img/uncertainty-analysis/porosity-cross-plot.png" alt="img" style="width: 500px;"/></center>
<center><p>Hình 1: Đồ thị phân tích thời gian truyền sóng với các mẫu lõi cso độ rỗng khác nhau, với đường hồi quy tương quan (màu đen) đường trung bình thời gian truyền sóng (màu đỏ). Hệ số tương quan vào khoảng 0.75</p></center>

Để có thể thực hiện được công việc với độ chính xác cao nhất, các nhà minh giải cần phải hiểu được các tính chất của khung đá trong vỉa và lưu chất vỉa, đặc biệt là các tham số của lưu chất vỉa do tính chất của lưu chất vỉa thường thay đổi theo vòng đời của vỉa (do suy giảm áp suất vỉa). Phương pháp thực hiện cho mỗi giếng có thể khác nhau phụ thuộc vào dữ liệu hiện có của giếng đó. 

Rủi ro trong quá trình thu thập và xử lý dữ liệu đồng thời làm cho việc minh giải khó khăn hơn. Mỗi lần tinh chỉnh dữ liệu đều có thể khiến cho quá trình minh giải lệch theo một hướng khác, mỗi mô hình độ rỗng được sử dụng đều phải xét đến các yếu tố lựa chọn tham số và sự thay đổi của tham số theo thời gian. Vì vậy, kết quả minh giải phụ thuộc rất nhiều vào người minh giải.
