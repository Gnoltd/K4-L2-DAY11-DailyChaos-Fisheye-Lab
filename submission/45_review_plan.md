# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| `adasind_258420.jpg` — cụm xe đông bên trái, zone mid | `Toàn bộ lỗi L của slice: 4 SPURIOUS + 1 MISSING (L1/R5, L8, L10, L11); 3/4 là reference thiếu hoặc hẹp (E0), 1 box vẽ phình (E1, đã rework)` | `Cảnh đông, vật nhỏ ≈50–65 px che nhau: đúng chỗ cả người gán và reference dễ bỏ sót hoặc vẽ lệch; một frame chiếm hết lỗi L nên soát ở đây giảm nhiều lỗi nhất` | `compare.html và model_compare.html của frame, dòng findings L1+R5/L8/L10/L11, delta.md trước/sau, decision log D3–D5` |
| `ThreeWheeler trên adasind_258420.jpg và adasind_310008.jpg` (+ edge_zone ở 310008) | `5 box model gọi sai auto-rickshaw thành Truck/Car/Bus (E4) + 4 Pedestrian lệch edge_zone (E2)` | `Lỗi hệ thống, không phụ thuộc zone: nếu không tách riêng sẽ làm sai mọi thống kê có model và mọi so attribute; cần ai_team và guideline xử lý trước khi dùng số` | `screenshots/01_model_threewheeler_258420.png, Ticket 1, 20_guideline_patch.md (R05b), local_quality_conflicts.csv` |

Giới hạn của kết luận từ ba frame ADASIND: `Chỉ 3 frame, 20 box reference, một camera fisheye trên xe hai bánh; một frame (258420) chiếm hết lỗi L nên không tách được ảnh hưởng của zone với ảnh hưởng của cảnh đông. Reference là teaching reference có lỗi (E0), không phải gold. Không suy ra tỷ lệ lỗi, cũng không suy cho camera front/rear/left/right.`

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh
như nhiều ca độc lập), và vì sao kế hoạch đó chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi: `Chọn mẫu phân tầng theo camera × normal/hard như 45_sampling_plan.csv, trong mỗi ô lấy rải theo chuyến/ngày/địa điểm và đặt khoảng cách tối thiểu giữa các frame (vd. mỗi cảnh/clip tối đa 1–2 frame) để không đếm nhiều frame liền nhau của cùng một cảnh như nhiều ca độc lập. Gắn tag cho từng frame (seam, đêm, lóa, vạch ô đỗ, ThreeWheeler, cảnh đông) và kiểm mỗi tag có đủ vài ca trên mỗi camera; ô nào thiếu thì bổ sung ở vòng sau. Mẫu hard được lấy dư có chủ đích (≈60% so với ≈21% trong 50.000 frame) nên tỷ lệ lỗi trong 200 frame không đại diện cho toàn bộ dữ liệu; muốn đo tỷ lệ cần mẫu ngẫu nhiên có trọng số và reference đã được phân xử.`
