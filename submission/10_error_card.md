# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B2 | MISSING | 9 |
| center | B2 | SPURIOUS | 16 |
| center | C0 | SPURIOUS | 2 |
| edge | B2 | MISSING | 2 |
| edge | B2 | SPURIOUS | 1 |
| edge | B2 | WRONG_CLASS | 1 |
| mid | B2 | MISSING | 6 |
| mid | B2 | SPURIOUS | 12 |
| mid | C0 | SPURIOUS | 1 |

## Top defects
- SPURIOUS: 32 (ví dụ frame adasind_019560.jpg)
- MISSING: 17 (ví dụ frame adasind_060000.jpg)
- WRONG_CLASS: 1 (ví dụ frame adasind_102750.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: TODO
- Cách sửa và ai nhận việc (`owner`): TODO
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule): TODO
