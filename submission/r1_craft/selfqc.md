# Tự soát

Không còn cảnh báo tự động ở bản cuối (export lần 5). Các cảnh báo đã xử lý qua bốn bản nháp:

- adasind_036720.jpg: 5 box cao < 40 px (Car ×3, Pedestrian, ThreeWheeler ở cuối đường) → đã xoá theo R01.
- adasind_036720.jpg, adasind_056040.jpg: thiếu ego_body → mình đã nối vùng tay áo vào polygon lens_border; sửa lại
  thành polygon `ego_body` riêng và trả `lens_border` về đúng vòng kính (R06, R07, R08).
- adasind_056040.jpg Car (0,750) và Bike (0,718): box chạm mép ảnh x=0 → `truncated=true` (R05).
- Tên task thiếu raw_fisheye → đổi tên task và export từ trang task thay vì job.

## Checklist thủ công
- [x] Phạm vi H=40 và vật cần vẽ — mọi box còn lại cao ≥ 40 px; box thấp nhất là Pedestrian 006840 (71,838) cao 41 px, giữ.
- [x] lens_border và ego_body — 2 lens_border mỗi frame khớp vòng kính; ego_body ở 036720 và 056040; 006840 không có thân xe nên không vẽ.
- [x] Class sáu nhãn — 036720 van bạc chở người (362,1022) đổi Truck → Car theo R04; xe ba bánh vàng đều là ThreeWheeler.
- [x] Rider và Bike — người ngồi trên xe máy gộp một box Bike (006840 L1, L6; 056040 Bike người áo đỏ).
- [x] Geometry trên ảnh fisheye gốc — 056040 Car sau xe ba bánh thu mép phải về x=632, chỉ bao phần nhìn thấy (R02).
- [x] truncated và occluded — ThreeWheeler lớn bị vòng kính/mép phải cắt: truncated; Car/Bus bị che ở 006840 và 056040: occluded.
- [x] Vật thiếu hoặc box trùng — soát lại 5 box prefill ở 006840, thêm 6 box; không có hai box cho cùng vật.
- [x] ignore_region có reason — mỗi polygon có đúng một reason (lens_border hoặc ego_body).
- [x] Tên task raw_fisheye và export CVAT 1.1 — `Day11 · ADASIND · B1-center · raw_fisheye`, CVAT for images 1.1, không kèm ảnh.
