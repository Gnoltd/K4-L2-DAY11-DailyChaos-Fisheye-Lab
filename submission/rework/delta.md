# Rework delta

| zone | matched before | matched after | missing before | missing after | spurious before | spurious after |
|---|---:|---:|---:|---:|---:|---:|
| center | 4 | 4 | 0 | 0 | 0 | 0 |
| mid | 8 | 8 | 1 | 1 | 4 | 4 |
| edge | 7 | 7 | 0 | 0 | 0 | 0 |

## Findings action=rework
- adasind_019560.jpg L1+R3 WRONG_CLASS: không áp dụng

## Giải thích

- Thay đổi thật: `chỉ sửa 1 box — adasind_258420.jpg L11 (Bike, zone mid). Box cũ (233.7,792.5)-(256.9,856.9) vẽ phình, lấn sang trái vào xe máy L6 và kéo xuống dưới phần nhìn thấy; box mới (239.0,792.5)-(256.9,843.6) bám phần nhìn thấy theo R02. Class Bike và occluded=true giữ nguyên. Mã khóa rework: BF96-F5CE.`
- Vì sao số trước/sau không đổi: `reference không có box nào ở vị trí L11, nên dù hình học tốt hơn L11 vẫn được tính là spurious ở zone mid (4 → 4). Phép so với teaching reference không đo được cải thiện hình học của một box không có cặp R; đây là giới hạn của phép so, không phải rework thất bại.`
- Các khác biệt còn lại không sửa, có lý do: `L1+R5 / R5 (ô tô trắng): reference box hẹp hơn phần xe nhìn thấy (E0), L1 đúng hơn nên giữ; L8 (người trên xe máy) và L10 (người cầm ô): vật cao ≥40 px thấy rõ nhưng reference thiếu (E0), giữ theo R01. Các dòng M_only/LR_noM là lỗi model (E4), không sửa nhãn. Dòng C0 L1+R3 (action=rework) thuộc vòng calib, không nằm trong slice B4-edge nên "không áp dụng" ở đây.`
