# Sensor context

- Rig: một camera fisheye duy nhất, ảnh dọc 1080×1920, gắn phía sau/bên hông xe hai bánh hoặc xe ba bánh
  (thấy chân người ngồi, tay cầm lái và bóng người trên mặt đường), nhìn chếch xuống mặt đường phía trước–bên.
  ADASIND không kèm tài liệu rig, calibration hay timestamp đồng bộ, nên đây chỉ là mô tả theo quan sát.
- `ego_body`: nửa dưới bên trái khung hình — chân/dép người lái, ống quần, tay nắm tay lái, gương/thân xe
  (vd. slice B1-center: `adasind_036720.jpg` tay áo và tay lái ở cạnh trái từ y≈1250 xuống đáy vòng kính;
  các frame khác trong bộ như `adasind_236370.jpg` thấy dép/chân ở góc dưới trái).
- Vòng kính (lens circle): hình tròn gần như chạm hai cạnh trái/phải, tâm hơi dưới giữa khung (y≈950–1000),
  đường kính ≈1080–1150 px, chiếm khoảng 55–60% diện tích khung; ngoài vòng là viền đen. Méo mạnh ở rìa vòng,
  vật ở rìa bị cong và kéo dài.
- Giới hạn: chỉ một camera, không đại diện đủ front/rear/left/right của SVM; không có seam hay track chéo
  camera để kiểm.
