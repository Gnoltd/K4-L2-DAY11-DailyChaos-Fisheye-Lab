# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B1 | IGNORE_SCOPE | 1 |
| center | B1 | MISSING | 5 |
| center | B1 | SPURIOUS | 8 |
| center | B1 | WRONG_CLASS | 3 |
| center | C0 | BOX_GEOMETRY | 1 |
| center | C0 | SPURIOUS | 2 |
| edge | B1 | BOX_GEOMETRY | 1 |
| edge | B1 | MISSING | 2 |
| edge | B1 | SPURIOUS | 5 |
| mid | B1 | MISSING | 3 |
| mid | B1 | SPURIOUS | 8 |

## Top defects
- SPURIOUS: 23 (ví dụ frame adasind_019560.jpg)
- MISSING: 10 (ví dụ frame adasind_006840.jpg)
- WRONG_CLASS: 3 (ví dụ frame adasind_006840.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: lỗi nổi bật nhất là **SPURIOUS (23)**, nhưng 15/23 là dòng `M_only` của model (mỗi ca của người được đếm lặp ở nhiều round) chứ không phải của người gán nhãn. Mình gán `E4_model_domain` vì cùng một mẫu lặp lại ở cả ba frame, không suy từ một box: model tách rider thành Pedestrian + Bike (vd `006840` M3, M6, M9; `036720` M1, M2, M6; `056040` M2, M3, M9, M11 — trái R03) và gọi xe ba bánh là Car/Truck vì không có class ThreeWheeler (`006840` M8, M10, M13; `036720` M4; `056040` M5 — trái R04). Phần SPURIOUS của người gán nhãn chỉ có 2 ca ở B1 (`006840` L11, `056040` L3) và 2 ca ở C0 (L1, L7), đều là bất đồng về phạm vi vật, đã ghi E0/E5.
- Cách sửa và ai nhận việc (`owner`): `ai_team` — ánh xạ output model sang taxonomy lab trước khi so (gộp person chồng lên motorcycle ≥50% thành một `Bike`; thêm class ThreeWheeler hoặc fine-tune trên ảnh có auto-rickshaw) rồi chạy lại `model` để đo lại. Không sửa nhãn người vì các dòng này. `qa` — phân xử hai ca giữ nhãn (`006840` Bus, Car) và ca escalate `056040` L3. `guideline` — thêm ví dụ R03 cho người ngồi sau / người đứng cạnh xe (xem `20_guideline_patch.md`).
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule): `screenshots/056040_L3_pedestrian_escalate.png` (box model M chồng rider), `screenshots/006840_bus_vs_threewheeler_L_vs_R.png`; `findings.csv` các dòng `r3_diag` có `why=E4_model_domain` (12 dòng R03, 9 dòng R04); `r3_diag/model_compare.md` bảng Zone × cell (M_only: center 5, mid 5, edge 5); rules R03, R04. Giới hạn: 3 frame, một camera, teaching reference chưa phải gold.
