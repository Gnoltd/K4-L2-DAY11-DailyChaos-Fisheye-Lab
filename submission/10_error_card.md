# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B4 | MISSING | 2 |
| center | B4 | SPURIOUS | 2 |
| center | C0 | SPURIOUS | 1 |
| edge | B1 | ATTRIBUTE | 1 |
| edge | B1 | BOX_GEOMETRY | 1 |
| edge | B4 | ATTRIBUTE | 1 |
| edge | B4 | MISSING | 1 |
| edge | B4 | SPURIOUS | 1 |
| edge | C0 | WRONG_CLASS | 1 |
| mid | B4 | BOX_GEOMETRY | 1 |
| mid | B4 | MISSING | 3 |
| mid | B4 | SPURIOUS | 14 |
| mid | C0 | SPURIOUS | 1 |
| unknown | B1 | MISSING | 2 |

## Top defects
- SPURIOUS: 19 (ví dụ frame adasind_019560.jpg)
- MISSING: 8 (ví dụ frame adasind_006840.jpg)
- BOX_GEOMETRY: 2 (ví dụ frame adasind_056040.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: `Lỗi nổi bật nhất là SPURIOUS (19), dồn ở zone mid của B4 (14), gần hết ở adasind_258420.jpg. Phần lớn không phải lỗi annotator: 11 dòng là box chỉ model có (M_only) do model gọi auto-rickshaw là Truck/Car/Bus (M4, M8, M11; 310008 M6/M7) hoặc tách người lái thành Pedestrian (M2, M3, M5, M10) → E4_model_domain, vì cùng một mẫu lặp lại ở nhiều xe trên 2–3 frame chứ không phải một box lệch. Các SPURIOUS của L (L8, L10, L1+M6) là vật thấy rõ ≥40 px mà reference thiếu hoặc vẽ hẹp → E0_reference_defect. Chỉ L11 là lỗi của mình (box vẽ phình, E1).`
- Cách sửa và ai nhận việc (`owner`): `ai_team: không dùng số của model YOLO26m cho ThreeWheeler khi chưa có lớp tương ứng; ánh xạ lại hoặc fine-tune trên ảnh fisheye có auto-rickshaw (Ticket 1). qa: bổ sung L8, L10 và nới R5 trong teaching reference của 258420 (Ticket 2 cùng loại với C0 L4/L8). annotator: đã rework L11 theo R02 (rework/delta.md). guideline: định nghĩa edge_zone (20_guideline_patch.md).`
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule): `screenshots/01_model_threewheeler_258420.png (model_compare.html frame 258420); findings r3_diag 258420 M4/M8/M11, L2+R1/L3+R4/L4+R8 (R04), M2/M3/M5/M10 (R03); r1_craft/r3_diag L8, L10, L1+R5 (R01, R02); L11 rework (R02).`
