# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide,
**không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có
normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference
ADASIND hoặc nhãn bạn vừa vẽ. Nếu cần, dùng `notebooks/day11-svm360-colab.ipynb` để thử tổng phân bổ; notebook
không làm thay phần lý do.

| camera_id | Hard case cần chọn | Vì sao dễ sai | Annotation space / calibration cần giữ | Cách review trước khi gọi là gold |
|---|---|---|---|---|
| front | Người/xe hai bánh cắt ngang sát mũi xe; xe ba bánh và xe lớn ở rìa vòng kính; ngược sáng | Vật ở rìa bị méo và truncated; ở slice ADASIND model bỏ sót cả hai xe ba bánh lớn bị vòng kính cắt; class hiếm ThreeWheeler bị gọi Car/Truck | Ảnh fisheye gốc (không undistort), tâm + bán kính vòng kính của camera front, polygon `ego_body` (capo) theo từng rig | Hai người gán nhãn độc lập, không xem nhãn của nhau; so bằng IoU ≥0.5 + class; ca bất đồng lên người soát thứ ba; ca rìa vòng kính kiểm thêm trên overlay vòng kính |
| rear | Vật thấp và trẻ em sát cản sau khi lùi; vật bị `ego_body` (cản sau) che một phần; hầm tối | Vật thấp dễ dưới ngưỡng H=40 hoặc lẫn với cản; ranh giới ego/vật khó; ánh sáng yếu | Ảnh gốc, polygon `ego_body` cản sau riêng cho camera rear, ngưỡng H=40 đo trên ảnh gốc | Hai người độc lập + người thứ ba cho ca dưới/sát ngưỡng H; kiểm riêng mọi box chồng `ego_body` ≥50% theo R09 |
| left | Xe máy vượt sát bên trái; người ngồi sau xe máy; vật đi qua seam front-left / rear-left | Trong slice ADASIND có 3 ca bất đồng rider/người ngồi sau/dắt xe (C0 L1, 056040 L3), model tách rider ở 12 dòng — R03 chưa đủ | Ảnh gốc; timestamp đồng bộ với front và rear; calibration để biết vùng seam; rules v1.1.0 (R03b) | Hai người độc lập; ca rider/pillion áp dụng R03b, không rõ thì escalate; ca seam gắn cờ để review cross-camera, không tự xoá box |
| right | Lề phải dày đặc người đi bộ, xe đỗ, xe ba bánh chồng nhau; seam front-right / rear-right | Vật nhỏ ở xa và chồng nhau là nơi người gán nhãn sai class/phạm vi nhiều nhất trong slice ADASIND (006840: Bus vs ThreeWheeler, box thừa, vùng unreadable) | Ảnh gốc; quy ước `unreadable` có ngưỡng rõ; timestamp + calibration với front và rear | Hai người độc lập + người thứ ba; ca `unreadable`/vật nhỏ ghi lý do; đối chiếu bảng độ phủ thẻ (mật độ, class hiếm) trước khi chốt |

- Khi nào cần refresh gold set (đổi camera, calibration hoặc rule): khi đổi vị trí gắn hoặc loại camera/ống kính (vòng
  kính, `ego_body` đổi), khi calibration hay đồng bộ timestamp thay đổi, khi rules đổi version (ví dụ v1.0.0 → v1.1.0
  thêm R03b thì mọi box rider/pillion phải soát lại), khi thêm class mới, hoặc khi dữ liệu mới có miền chưa có trong
  gold (đêm, mưa, quốc gia khác). Mỗi lần refresh ghi version gold + rules version dùng.
- Một ca seam/cross-camera cần policy và evidence trước khi ghép hai box: một xe máy vượt ở góc trước-trái xuất hiện
  cùng lúc ở edge của camera front và mid của camera left với hai box khác nhau. Cần timestamp đồng bộ để biết hai ảnh
  cùng thời điểm, calibration để chiếu hai box về cùng không gian (ví dụ BEV) và kiểm có trùng vị trí, và policy output
  (giữ cả hai box theo từng camera, hay hợp nhất một vật với một track ID). Chưa có đủ ba thứ đó thì giữ hai box, không
  gọi là `DUPLICATE`.
- Vì sao peer agreement hoặc quality report trên ảnh một camera chưa chứng minh gold set đúng cho cả bốn camera: ADASIND
  chỉ có một camera, không có seam, track liên camera hay `ego_body` của cản sau/hông xe; zone center/mid/edge là vị trí
  trên một ảnh, không phải camera thứ hai. Hai người đồng ý có thể cùng sai (ở slice này mình và model cùng gọi Bus
  một xe mà reference gọi ThreeWheeler), và teaching reference hiện tại là bản sửa tay trên vài frame, chưa qua review
  độc lập — nên chỉ số local quality đo độ khớp với reference đó, không đo độ đúng của gold cho bốn camera.
