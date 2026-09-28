# Sensor context

- Rig: ảnh cho thấy một camera fisheye hướng ra cảnh giao thông; chưa đủ bằng chứng để xác định camera gắn ở vị trí nào trên xe hay hướng nhìn chính xác so với thân xe.
- `ego_body`: trong các frame B2-mid đã xem, có phần tay áo/cơ thể lọt vào sát mép dưới-trái. Chỉ vẽ vùng thân xe/thiết bị thực sự nhìn thấy trong từng frame; không suy rộng vùng này sang phần ảnh bị che.
- Vòng kính: vùng ảnh hữu dụng là một hình tròn lớn, gần giữa khung dọc và gần chạm các cạnh trái/phải; vành đen bao quanh rõ nhất ở phía trên và phía dưới. Giữ polygon `lens_border` theo prefill và soát trên từng frame; không dùng mô tả này thay cho hiệu chỉnh hình học.
