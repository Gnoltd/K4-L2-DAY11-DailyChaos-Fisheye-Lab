# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| Center, cảnh đường đông có vật nhỏ ở xa — `adasind_006840.jpg` | 3 bất đồng người–reference: 1 WRONG_CLASS/MISSING (xe vàng L9 Bus vs R4 ThreeWheeler), 1 SPURIOUS (L11 Car), 1 IGNORE_SCOPE (L10 trong vùng `unreadable` của reference) | Toàn bộ lỗi của người trong slice nằm ở đây (center: 1 missing, 2 spurious / n_ref=10); vật cao 40–70 px, chồng nhau, nên class và phạm vi vật dễ lệch giữa người với nhau | `screenshots/006840_bus_vs_threewheeler_L_vs_R.png`, dòng `findings.csv` L9+R4, L11, R4, quyết định D2–D3 trong decision log |
| Xe hai bánh chở/đứng cạnh người — `adasind_056040.jpg` (mid) và C0 `adasind_019560.jpg` | 1 SPURIOUS escalate (056040 L3) + 2 bất đồng ở C0 (L1 Pedestrian, L2 Bike); model thêm 12 dòng tách rider (R03) trên cả ba frame B1 | Cùng một khoảng trống của R03 (không thấy chân/yên, người ngồi sau) gây bất đồng ở cả người, reference và model; sửa luật sẽ đổi nhãn ở mọi slice có xe máy | `screenshots/056040_L3_pedestrian_escalate.png`, `30_escalation_ticket.md`, `20_guideline_patch.md` (R03b), dòng `r3_diag` E4 R03 |

Giới hạn của kết luận từ ba frame ADASIND: chỉ 3 frame, 20 vật trong reference, một camera fisheye; zone edge chỉ có
n_ref=3 nên một vật đổi kết quả là đổi 33%. Teaching reference là bản sửa tay, chưa kiểm bởi nhiều người, nên số
bất đồng không phải tỷ lệ lỗi. Các frame lấy từ cùng một chuyến đi, cảnh ban ngày đường phố Ấn Độ; không suy ra cho
đêm, mưa, bãi đỗ hay camera gắn ô tô.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh
như nhiều ca độc lập), và vì sao kế hoạch đó chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi: lấy mẫu theo **cảnh**
(clip/chuyến đi) trước rồi mới lấy frame — tối đa 1–2 frame mỗi cảnh, cách nhau ≥ vài giây, để 200 frame không phải
vài chục frame liền nhau của cùng một cảnh bị đếm như ca độc lập. Với mỗi ô camera × normal/hard, lập bảng độ phủ
theo thẻ: ngày/đêm, thời tiết, loại đường/bãi đỗ, mật độ, có seam hay không, class hiếm (ThreeWheeler, người ngồi sau
xe máy, vật thấp sau cản); ô nào thiếu thẻ thì bổ sung trước khi tăng số frame ở ô đã đủ. Hai bài học từ slice này
được đưa vào ô hard: xe ba bánh/xe lớn bị vòng kính cắt ở rìa (model bỏ sót cả hai ca) và người sát xe hai bánh.
Kế hoạch này chọn ca có **khả năng** sai cao nên mẫu bị thiên về hard: nó giúp tìm ca cần soi và viết luật, nhưng
không cho tỷ lệ lỗi của 50.000 frame. Muốn ước lượng tỷ lệ cần thêm một mẫu ngẫu nhiên có trọng số riêng cho từng
camera.
