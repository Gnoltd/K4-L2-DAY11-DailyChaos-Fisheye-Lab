# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_006840.jpg
- L10 center IGNORE_SCOPE
- L9+R4 center WRONG_CLASS
- L11 center SPURIOUS
## adasind_036720.jpg
## adasind_056040.jpg
- L3 mid SPURIOUS

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 10 | 9 | 1 | 2 |
| mid | 7 | 7 | 0 | 1 |
| edge | 3 | 3 | 0 | 0 |
