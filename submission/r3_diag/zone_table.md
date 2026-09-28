# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 4 | 0 | 0 | 2 | 2 | — |
| mid | 9 | 1 | 4 | 3 | 8 | SPURIOUS (3) |
| edge | 7 | 0 | 0 | 1 | 1 | — |

## Nhận xét

- Zone nào người (L) và model (M) gãy nhiều nhất, dẫn số ở bảng trên: `Cả L và M đều gãy ở zone mid. L: 1 missing + 4 spurious ở mid, center và edge đều 0; M: 3 missing + 8 thừa ở mid, so với 2+2 ở center và 1+1 ở edge. Toàn bộ lỗi mid của L nằm ở một frame (adasind_258420, cụm xe đông bên trái). Edge không gãy: L khớp 7/7 box reference ở edge dù slice là B4-edge.`
- Giả thuyết vì sao (méo fisheye, box lỏng, thiếu `ego_body`, ...) và giới hạn của slice ba frame: `Lỗi mid của L chủ yếu không phải do méo fisheye mà do cảnh đông và che khuất: 3/4 spurious là vật nhỏ ≈50–65 px mà reference bỏ sót (L8 người trên xe máy, L10 người cầm ô → E0), 1 ca chưa phân xử (L11 Bike hay Pedestrian → E5); missing R5 + spurious L1 là cùng một ô tô, R5 hẹp hơn phần xe nhìn thấy (iou_sweep: ở IoU 0.3 missing mid của L về 0). Lỗi M theo hai mẫu hệ thống: gọi auto-rickshaw là Truck/Car/Bus (5 box ở 2 frame) và tách người lái thành Pedestrian (4 box), tức lệch miền/khác luật R03-R04, không phụ thuộc zone. Giới hạn: chỉ 3 frame, 20 box reference, một frame chiếm hết lỗi L; zone là vị trí trên ảnh, không cho biết xa gần; reference là teaching reference có lỗi, không phải gold. Không đủ để kết luận zone nào khó hơn nói chung.`
