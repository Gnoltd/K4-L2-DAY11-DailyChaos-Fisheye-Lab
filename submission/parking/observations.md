# Quan sát vạch ô đỗ

- Hai vạch `parking_line` đã vẽ (mô tả vị trí trong ảnh):
`7 polyline ở dãy ô đỗ khoảng 1 phần 3 phía dưới ảnh. Một vạch dài gần nằm ngang chạy từ mép trái tới gần mép phải của ảnh. 6 vạch chéo ngắn cắt qua vạch dài, mỗi vạch chéo là ranh giới giữa hai ô liền kề. Mỗi polyline dừng ở chỗ sơn kết thúc, không nối qua phần không thấy.`

- Một vạch/dấu sơn hoặc biên **không** vẽ, và vì sao: `Không vẽ các vạch ở dãy phía xa (phía gần xe ô tô) vì các vạch ở đó quá nhỏ, mờ và bị lóa nên khó xác định được chính xác hai đầu vạch.`

- Polygon `free_space` dừng ở đâu; có phần bị che nào không:
`Cạnh trên bám sát theo các polyline của vạch parking_line đã vẽ ở trên. Cạnh dưới, trái, phải dừng ở mép khung ảnh. Polygon khoét quanh các vạch chéo (ở trên) và 4 vạch sơn trắng ở gần mép dưới của ảnh để không phủ lên sơn. Trong vùng này không có xe hay vật che.`

- Ca chưa chắc cần hỏi người soát (nếu không có, ghi “không có”):
`không có`
