# Guideline patch

- **Rule mới đề xuất:** **R03b — Người sát xe hai bánh khi không thấy chân/yên.** Chỉ gộp người vào box `Bike` khi
  thấy được ít nhất một dấu hiệu *ngồi*: hông ngang hoặc trên yên, hai chân kẹp hai bên thân xe, hoặc người ngồi sau
  thẳng hàng phía sau người lái trên cùng yên. Nếu người đứng lệch hẳn sang một bên xe, đầu cao hơn tay lái rõ rệt,
  hoặc thấy chân chạm đất bước đi → `Pedestrian` + `Bike` tách. Nếu chân và yên đều bị che/blur và không có dấu hiệu
  nào ở trên → giữ nhãn theo phán đoán, đặt `occluded=true` và ghi ca vào `findings.csv` với `why=E2_guideline_gap`,
  `action=escalate`; không tự đổi reference.
  Ví dụ: `adasind_019560.jpg` người áo đỏ (455,730)–(537,898) — người gán nhãn đọc là dắt xe, reference gộp thành
  rider; `adasind_056040.jpg` Pedestrian (219,772)–(245,861) sát rider áo đỏ — người ngồi sau hay người đứng cạnh.
- **Áp dụng cho:** class `Bike` và `Pedestrian`, attribute `occluded`; mọi zone (hai ca trên ở center và mid).
  Không áp dụng cho người ngồi trong ô tô/xe buýt/xe ba bánh (vẫn theo R03 hiện tại).
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** R03 chỉ phân biệt "ngồi lên" và "dắt" nhưng không nói
  dựa vào dấu hiệu nào khi chân và yên không nhìn thấy. Trong bài này có hai ca như vậy và cả hai đều gây bất đồng
  giữa người gán nhãn, reference và model (model luôn tách person + motorcycle, nên không dùng được làm trọng tài).
  R03 cũng không nhắc người ngồi sau (pillion).
- **`rules_version` mới:** v1.0.0 → v1.1.0
- **Hiệu lực từ:** round `rework` của đợt sau và mọi slice mới; các bản đã khoá ở v1.0.0 giữ nguyên, chỉ phân xử lại hai
  ca đã escalate theo R03b.
