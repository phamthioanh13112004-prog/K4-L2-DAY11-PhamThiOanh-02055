# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_123090.jpg
## adasind_128310.jpg
- R4 center MISSING
## adasind_199770.jpg
- L3+R9 center BOX_GEOMETRY
- L6 mid SPURIOUS
- L8+R6 edge BOX_GEOMETRY
- L9 center SPURIOUS
- R3 mid MISSING
- R4 mid MISSING

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 6 | 4 | 2 | 2 |
| mid | 6 | 4 | 2 | 1 |
| edge | 5 | 4 | 1 | 1 |
