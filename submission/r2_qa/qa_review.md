# QA review · B4-edge

Mã khóa: 41EB-462A (XML đã xác minh SHA-256 khớp lock trên `origin/hoang`).

**Hình thức:** review mù theo phân công, dùng ảnh gốc, overlay và rules v1.0.0; không dùng teaching reference hoặc model. `object_ref` là thứ tự box trong XML của frame.

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| adasind_236370.jpg | L3 | R02 | Box `Truck` (408,654)–(767,922) bao trùm không chỉ xe tải/van trắng phía sau mà còn một phần người và xe máy ở phía trước. Hình học hiện có vẻ gộp nhiều vật vào một box; đề nghị annotator vẽ lại theo phần nhìn thấy của riêng xe và kiểm tra class theo R04. |
| adasind_258420.jpg | L6–L8, L9, L11 | R03 | Cụm xe máy/người đi bộ sát trái có nhiều box chồng/tiếp giáp. Ảnh overlay cho thấy có thể là nhiều xe và người riêng, nhưng không đủ rõ để kết luận box trùng hay xác định ai đang lái/dắt xe. Đề nghị phóng to ảnh gốc, xác nhận từng rider theo R03 và giữ Bike/Pedestrian riêng chỉ khi người đó đang dắt xe. |
| adasind_310008.jpg | L1–L4 | R02, R05 | Bốn box `Pedestrian` chồng mạnh tại mép trái; ảnh gốc cho thấy một nhóm người nhưng ranh giới từng người và việc box L4 bị cắt bởi biên ảnh cần được kiểm tra ở mức zoom cao. Xác nhận mỗi box ứng với một người riêng; đặt `truncated=true` cho người thực sự bị khung ảnh cắt, không chỉ vì các box lân cận chồng nhau. |

Đây là nhận xét QA, chưa phải kết luận WHY hay phán quyết teaching reference. Các ca chưa rõ cần annotator/reviewer kiểm tra ảnh gốc; ghi finding `r2_qa` với `cell=L_only`, `rule_id` có giá trị và để trống `why`.
