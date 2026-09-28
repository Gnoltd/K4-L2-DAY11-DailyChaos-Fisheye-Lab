# Rework delta

| zone | matched before | matched after | missing before | missing after | spurious before | spurious after |
|---|---:|---:|---:|---:|---:|---:|
| center | 9 | 9 | 1 | 1 | 2 | 2 |
| mid | 7 | 7 | 0 | 0 | 1 | 2 |
| edge | 3 | 3 | 0 | 0 | 0 | 0 |

## Findings action=rework
- adasind_006840.jpg missing@x92-106,y838-900 MISSING: không áp dụng
- adasind_056040.jpg L7+R7+M6 BOX_GEOMETRY: đã sửa
- adasind_056040.jpg L7 ATTRIBUTE: đã sửa

## Đọc số trước/sau

Bản rework `7968-8D80` (khoá lại bằng `--relock`, lịch sử bản 8F87-0D1E giữ trong `lock2.txt`) thực hiện đúng ba
quyết định của C (Đào Xuân Tùng) sau QA của B (Nguyễn Văn Hoàng) — decision log D6, D8:

- `adasind_056040.jpg` L7 Car: cạnh trái thu từ x=0 về **x=103**, `truncated` true → **false**, giữ `occluded=true`.
  Tool xác nhận "đã sửa" cho cả BOX_GEOMETRY và ATTRIBUTE. Matched mid giữ 7 vì trước và sau đều ghép được với
  reference R7 (80,755)–(195,990); sửa này làm box bám phần nhìn thấy (R02), không đổi số đếm. Mục tiêu phân xử là
  x≈80, A kéo về x=103 nên box hụt khoảng x 80–103 của thân xe — chấp nhận, IoU với R7 vẫn ≈0.73.
- `adasind_006840.jpg`: **thêm** `Pedestrian` (92,832)–(109,904), `occluded=true` — người áo trắng đứng sau xe máy L1.
  Vật này không có trong teaching reference, nên tool đếm là **spurious mid 1 → 2** và ghi "không áp dụng". Đây là
  kết quả dự kiến: nhóm cho rằng reference thiếu vật (E0 phụ ở dòng findings `missing@x92-106`), không sửa số bằng tay.
- Không sửa: xe vàng Bus và box Car (301,833) ở 006840 (keep_with_reason, D2–D3); 056040 L3 và người cạnh xe ba bánh
  ở 006840 đang escalate (D5, D7).

Center giữ 9 matched / 1 missing / 2 spurious vì hai ca keep_with_reason không đổi. Giới hạn: teaching reference chưa
phải gold; khi reference được bổ sung người áo trắng, spurious mid sẽ về 1 và matched mid thành 8.
