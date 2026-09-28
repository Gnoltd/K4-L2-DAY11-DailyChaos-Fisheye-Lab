# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_060000.jpg
- L8 mid SPURIOUS
- L9 center SPURIOUS
- R2 mid MISSING
- R9 center MISSING
## adasind_086220.jpg
- L4 center SPURIOUS
- L6 center SPURIOUS
- R4 center MISSING
## adasind_102750.jpg
- L3 center SPURIOUS
- L5+R2 edge WRONG_CLASS
- R5 center MISSING

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 9 | 6 | 3 | 4 |
| mid | 8 | 7 | 1 | 1 |
| edge | 3 | 2 | 1 | 1 |
