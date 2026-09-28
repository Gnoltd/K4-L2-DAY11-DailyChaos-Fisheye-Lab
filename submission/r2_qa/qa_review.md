# QA review · B1-center

Mã khóa: 8F87-0D1E

Soát mù bản khóa của long chỉ bằng ảnh gốc, `qa_overlay.html` và rules v1.0.0. Chưa mở teaching reference, model
hay worked overlay. Tọa độ theo pixel ảnh gốc 1080×1920.

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| `adasind_006840.jpg` | `missing@x92-106,y838-900` | `R01` | `Có một người mặc đồ trắng đứng sau/bên trái xe máy L1, cao khoảng 60 px (≥ H=40) nhưng chưa có box Pedestrian; người này không ngồi trên xe nên không gộp vào Bike L1 theo R03. Cần thêm box với occluded=true.` |
| `adasind_006840.jpg` | `missing@x368-392,y825-900` | `R01;R03` | `Người đứng phía sau auto-rickshaw L3, bị che một phần nhưng vẫn còn nhìn thấy được, cao khoảng 75 px, nằm trong box L3 nhưng không có box riêng. Cần có thêm box Pedestrian (R01). Cần annotator xác nhận trên ảnh gốc.` |
| `adasind_036720.jpg` | `L1–L4, ego_body` | `R05;R07;R08` | `Không thấy lỗi: L2 (auto ở mép phải) đã đặt truncated=true vì bị khung cắt; người trong auto không box riêng (R03); ego_body phủ tay/đầu gối người lái ở góc dưới trái; 2 polygon lens_border khớp vòng kính.` |
| `adasind_056040.jpg` | `L7` | `R02;R05` | `Box Car L7 (x 0–189) kéo sang tận mép trái khung, nhưng ô tô xám chỉ thấy được từ x≈83 trở sang phải; phần bên trái bị người lái áo đỏ (L8) che, không phải bị mép khung cắt. Theo R02 box chỉ bám phần nhìn thấy nên cạnh trái cần thu về x≈83; theo R05 xe bị vật khác che nên giữ occluded=true nhưng truncated=true không có căn cứ. Cần annotator xem lại.` |
| `adasind_056040.jpg` | `L8, ego_body` | `R05;R07` | `Không thấy lỗi: L8 (xe máy người áo đỏ) chạm mép trái khung nên truncated=true đúng; ego_body phủ tay/chân người lái ở góc dưới trái.` |

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.
