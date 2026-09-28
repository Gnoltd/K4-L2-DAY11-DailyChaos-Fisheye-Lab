# Quan sát vạch ô đỗ

- Tự review trên ảnh core: hai ứng viên rõ là vạch chéo ở tiền cảnh giữa ảnh (xấp xỉ từ x=400,y=650 xuống mép dưới gần x=540) và vạch chéo ở tiền cảnh bên phải (xấp xỉ x=695,y=625 đến mép phải gần y=690). Export hiện chưa biểu diễn sạch cả hai: vạch giữa đi theo hai mép sơn rồi quay ngược, còn vạch bên phải đang là polygon `parking_line`; cần vẽ lại mỗi vạch thành một polyline đơn bám phần sơn nhìn thấy.
- Không gán nhãn đường chân trời/biên ngang xa của bãi là `parking_line`: đó không phải vạch chia hai ô đỗ riêng. Cũng không nối polyline qua phần sơn khuất hoặc ra ngoài mép ảnh.
- `free_space` nên giới hạn ở phần mặt đường/lối xe chạy trống nhìn thấy giữa các hàng ô. Polygon dưới trong export hiện phủ xuống phần lớn các ô đỗ tiền cảnh và băng qua nhiều vạch; polygon trên cũng cần soát mép theo lối xe chạy. Không thể kết luận vùng lái xe an toàn từ ảnh tĩnh.
- Cần sửa hình học hai vạch ứng viên và vẽ lại `free_space` trong CVAT rồi export lại; các polyline ngắn/nhỏ còn lại trong XML cần được đối chiếu từng điểm trên ảnh trước khi giữ. Đây là self-review theo ảnh + XML, chưa có peer review độc lập.
