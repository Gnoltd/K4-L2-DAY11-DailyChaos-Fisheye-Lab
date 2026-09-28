# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 10 | 1 | 2 | 5 | 6 | WRONG_CLASS (1) |
| mid | 7 | 0 | 1 | 3 | 6 | SPURIOUS (1) |
| edge | 3 | 0 | 0 | 2 | 5 | — |

## Nhận xét

- Zone nào người (L) và model (M) gãy nhiều nhất, dẫn số ở bảng trên: người gãy ở **center** (1 missing, 2 spurious trên n_ref=10), cả ba lỗi đều ở frame 006840 là vùng xa, vật nhỏ và chồng nhau (xe vàng gọi Bus thay vì ThreeWheeler, box Car thừa trên túi hàng của rider); mid chỉ 1 spurious (056040 L3, chưa phân xử), edge 0 lỗi. Model gãy đều ở cả ba zone nhưng nặng nhất theo tỉ lệ ở **edge**: thiếu 2/3 vật reference và 5 box thừa, so với center 5/10 thiếu và mid 3/7 thiếu.
- Giả thuyết vì sao (méo fisheye, box lỏng, thiếu `ego_body`, ...) và giới hạn của slice ba frame: lỗi của model phần lớn **không do zone** mà do lệch taxonomy — (1) tách rider thành person + motorcycle, 12 dòng M_only/LR_noM theo R03; (2) không có class ThreeWheeler nên gọi Car/Truck/Bus, 9 dòng theo R04. Ở edge thêm giả thuyết méo fisheye: hai xe ba bánh lớn bị vòng kính cắt (036720 L2, 056040 L6) model không ra box nào, và model tạo box Pedestrian trên cánh tay ego ở mép dưới (036720 M5, 056040 M10) — nằm trong `ego_body` nên không tính. Lỗi người ở center là class/scope trên vật nhỏ ở xa, không phải méo. Giới hạn: chỉ 3 frame, 20 vật reference, edge chỉ có n_ref=3 nên một vật đổi kết quả là đổi 33%; reference là teaching reference sửa tay, chưa phải gold; không suy khoảng cách hay mức rủi ro từ zone.
