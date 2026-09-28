# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling
đã nằm trong file tương ứng nên không hỏi lại ở đây.

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy
   tắc riêng? Vì sao? **Không phải `DUPLICATE`.** `DUPLICATE` là hai box cho cùng một vật **trên cùng một ảnh**.
   Ở seam, mỗi camera là một ảnh riêng, và mỗi ảnh đều phải có box cho vật nhìn thấy trên ảnh đó (theo R01/R02 trên
   ảnh gốc) — nên hai box trên hai ảnh là hợp lệ, zone có thể khác nhau (edge ở camera này, mid ở camera kia). Việc
   có ghép hai box thành một vật hay không là quy tắc **riêng** của output đích (ví dụ BEV hoặc danh sách vật hợp
   nhất), cần timestamp đồng bộ, calibration hai camera và policy "giữ box nào/hợp nhất ra sao". Trước khi có các thứ
   đó, người gán nhãn giữ cả hai box, không xoá box nào.
2. Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái
   Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera. **Giữ cùng track ID** khi vẫn là cùng một vật
   quan sát được liên tục, kể cả khi bị che ngắn. **Thêm keyframe** khi hình học đổi lớn: vật đi từ center ra edge và
   bị méo/kéo dài, bị vòng kính cắt (truncated), bị che hoặc hết che — như xe ba bánh sát camera ở `adasind_056040.jpg`,
   nội suy sẽ lệch. **Outside** khi vật ra khỏi trường nhìn hoặc vào hẳn vùng ignore (thân xe ego, ngoài vòng kính);
   khi quay lại vẫn là cùng vật thì giữ ID cũ. Nối track **qua hai camera** chỉ khi có: timestamp đồng bộ giữa hai
   camera, calibration (nội + ngoại) để chiếu hai box về cùng không gian, và policy output đích; không nối chỉ vì
   cùng class hay cùng màu.
3. Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`),
   bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm? `adasind_006840.jpg` L9: mình gán
   **Bus** cho xe vàng (303,818)–(360,879) vì xe to hơn xe ba bánh cạnh đó, đuôi xe lớn và có phần kính ở góc trái;
   reference gọi ThreeWheeler và bản QA cũng nghi ca này. Mình không sửa âm thầm: ghi `E0_reference_defect`,
   `keep_with_reason` với lý do nhìn thấy trên ảnh, ghi D2 trong decision log, và khoá lại chính bản r1_craft làm
   rework nên `delta.md` giữ số trước/sau bằng nhau. Nếu làm lại, mình sẽ ghi lý do class ngay trong self-QC lúc vẽ
   cho các vật nhỏ ở xa, và kiểm vùng ignore trước khi vẽ nhanh — ở cùng frame, box L10 Car nằm trong vùng
   `unreadable` của reference, và ở P2 mình đã phải sửa `ego_body` bị nối vào `lens_border` qua bốn bản nháp.
