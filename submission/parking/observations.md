# Quan sát vạch ô đỗ

- Hai vạch `parking_line` đã vẽ (mô tả vị trí trong ảnh): (1) vạch trắng xiên ở tiền cảnh bên phải, từ (699,623)
  đến (956,684), chia hai ô đỗ của dãy gần camera; (2) vạch xiên ở dãy giữa bên trái, từ (247,563) đến (178,524),
  là một trong các vạch song song chia dãy ô giữa thành từng ô riêng. Tổng cộng export có 20 polyline: tiền cảnh
  (4 vạch), dãy giữa (6 vạch xiên) và các đầu vạch ngắn ở dãy xa; chỉ vẽ phần sơn nhìn thấy, dừng khi vạch mờ/hết.
- Một vạch/dấu sơn hoặc biên **không** vẽ, và vì sao: vết sơn nhạt/ố ở đáy giữa ảnh (khoảng x≈340–390, y≈712–720)
  không vẽ vì không tạo ranh giới ô nào, chỉ là dấu mặt đường bị cắt bởi mép ảnh. Mép bãi và hàng rào phía xa
  (y≈450–470) cũng không vẽ: đó là biên bãi, không phải vạch chia ô.
- Polygon `free_space` dừng ở đâu; có phần bị che nào không: polygon chính bao lối xe chạy trống giữa dãy ô giữa và
  dãy ô tiền cảnh (mép trên y≈526–574, mép dưới y≈591–682), không đi vào đầu các vạch tiền cảnh bên phải. Polygon thứ
  hai là dải lối xe hẹp giữa dãy giữa và dãy xa (y≈488–523); ở xa ảnh bị nén nên ranh giới với đầu vạch dãy xa kém
  chính xác. Không có xe hay vật che trong hai polygon; chiếc xe đỏ ở xa nằm ngoài polygon.
- Ca chưa chắc cần hỏi người soát (nếu không có, ghi “không có”): vạch dài gần nằm ngang ở dãy giữa, từ (1,541) đến
  (833,511). Guideline không nhắc riêng loại vạch này; mình **giữ** nhãn `parking_line` theo định nghĩa "đoạn sơn tạo
  ranh giới một ô đỗ riêng lẻ": (a) nó nằm giữa hai dãy ô xiên quay lưng vào nhau, không nằm ở mép lối xe chạy;
  (b) các vạch xiên của dãy giữa (ví dụ (247,563)→(178,524), (417,553)→(286,521)) cắt qua nó, nên nó là cạnh đầu
  chung khép kín từng ô ở cả hai phía; (c) xe không chạy dọc theo vạch vì hai bên đều là ô đỗ, nên nó không phải
  "dải sơn dài chỉ dẫn lối xe chạy". Nhờ người soát xác nhận cách đọc này; nếu guideline muốn chỉ gán vạch ngăn giữa
  hai ô cạnh nhau, vạch này sẽ bị loại mà không ảnh hưởng hai vạch chính ở trên.
