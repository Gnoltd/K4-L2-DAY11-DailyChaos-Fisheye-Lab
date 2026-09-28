# QA review · B1-center

Mã khóa: 8F87-0D1E

**Hình thức:** cold review chính slice của mình (nhóm long/tung/hoang; người kế bên là tung chưa khoá bài sau hơn
5 phút, theo `docs/03-roles-rotation-vi.md`). Soát chỉ bằng rules v1.0.0 trên `qa_overlay.html` và ảnh gốc, chưa mở
teaching reference, model overlay hay worked HTML. Giới hạn: người soát cũng là người vẽ nên dễ bỏ sót lỗi của
chính mình; hoang sẽ soát mù độc lập bản khoá này.

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| adasind_006840.jpg | L11 | R04 | Box `Car` (301,833)–(324,896) nằm sát mép phải rider L6; phóng to thấy vật màu đỏ sẫm/trắng giống túi hàng hoặc phần xe của L6, không thấy thân ô tô. Nghi sai class hoặc box thừa; cần xem lại có vật riêng không. |
| adasind_006840.jpg | L9 | R04 | Box `Bus` (303,818)–(360,879): xe vàng có kính trước rộng, ở xa. Có thể là minibus (→ Bus theo R04) hoặc van chở người (→ Car); ảnh nhỏ nên chưa phân biệt chắc. |
| adasind_006840.jpg | L2 | R01 | `Pedestrian` (71,838)–(89,879) cao 41 px, sát ngưỡng H=40; giữ box nhưng nếu kéo mép box sai 1–2 px thì vật rơi khỏi phạm vi. |
| adasind_056040.jpg | L3 | R03 | `Pedestrian` (219,772)–(245,861) chồng lên mép phải `Bike` L2 (người áo đỏ trên xe máy). Ảnh mờ; nếu đây là người ngồi sau (pillion) thì theo R03 không box riêng. Cần soát lại vị trí chân/yên. |
| adasind_056040.jpg | L7 | R02 | `Car` (0,750)–(189,980): phần thân bên trái bị rider L8 che; box kéo tới x=0 theo quyết định của người gán (phần thấy chạm mép ảnh), đã đặt `truncated=true`. Người soát nên kiểm lại phần xe thật sự thấy ở x<85. |
| adasind_036720.jpg | L4 | R04 | Van bạc chở người đã đổi từ `Truck` sang `Car` theo R04 — đúng luật, không cần sửa. |

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.
