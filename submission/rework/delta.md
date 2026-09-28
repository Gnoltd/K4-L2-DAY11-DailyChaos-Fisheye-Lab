# Rework delta

| zone | matched before | matched after | missing before | missing after | spurious before | spurious after |
|---|---:|---:|---:|---:|---:|---:|
| center | 9 | 9 | 1 | 1 | 2 | 2 |
| mid | 7 | 7 | 0 | 0 | 1 | 1 |
| edge | 3 | 3 | 0 | 0 | 0 | 0 |

## Findings action=rework
Không có dòng `action=rework`. Bản rework là **chính bản r1_craft đã khoá** (cùng mã 8F87-0D1E), nên số trước/sau
bằng nhau ở cả ba zone — đây là quyết định có căn cứ, không phải bỏ bước.

## Vì sao không sửa

Ba khác biệt với teaching reference đều nằm ở center (1 missing, 2 spurious) và đã được xem lại trên ảnh gốc:

- `006840` xe vàng (303,818)–(360,879) — reference gọi ThreeWheeler, mình giữ **Bus**: xe to hơn xe ba bánh bên cạnh,
  đuôi xe lớn, có phần kính ở góc trái thân xe. `keep_with_reason`, E0, cần người soát thứ ba.
- `006840` box Car (301,833)–(324,896) — reference không có, mình giữ **Car**: vật màu trắng khác phần màu xám phía sau
  xe máy L6, đọc được là đầu một xe màu trắng. `keep_with_reason`, E0, cần người soát thứ ba.
- `056040` Pedestrian (219,772)–(245,861) — reference không có, model có (M4). Chưa đủ bằng chứng người ngồi sau hay
  người đứng cạnh → `escalate` (xem `30_escalation_ticket.md`), không sửa trước khi có phân xử.

Nếu người soát thứ ba đồng ý với reference ở hai ca đầu, sửa sẽ đổi center thành matched 10, missing 0, spurious 0.
Giới hạn: reference là teaching reference sửa tay trên 3 frame, không phải gold set; hai nguồn (mình và model) cùng
gọi Bus không chứng minh bên nào đúng vì model không có class ThreeWheeler.
