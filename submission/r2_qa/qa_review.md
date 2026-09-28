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

---

# QA review · B2-mid (bài của tung)

Mã khóa: E89D-402C — `python3 lab11.py qa` xác nhận mã khớp file `submission/r1_craft/annotations.xml` trên branch
`tung` (lock 2026-09-28T18:29). Overlay: `qa_overlay.html`; overlay cold review cũ đổi tên thành
`qa_overlay_cold_B1-center.html`.

**Hình thức:** review mù theo vòng nhóm (long soát tung). Chỉ dùng rules v1.0.0, ảnh gốc và bản khoá; không mở
teaching reference, model overlay, worked HTML hay các file P4 của tung. `object_ref` là thứ tự box cao ≥ 40 px theo XML.

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| adasind_060000.jpg | (không có box) | R01 | **Thiếu box** người đội mũ bảo hiểm đỏ lái xe máy đi cùng chiều, khoảng (80,825)–(170,1050), cao ~220 px, nằm rõ trong vòng kính. Theo R01 và R03 cần một box `Bike` bao cả người và xe. |
| adasind_060000.jpg | (không có polygon) | R07 | **Thiếu `ego_body`**: tay áo sơ mi kẻ và tay lái ở góc dưới trái (khoảng x 0–200, y 1140–1720) là thân xe ego nhìn thấy nhưng không có polygon. |
| adasind_086220.jpg | ego_body | R07 | Polygon `ego_body` chỉ rộng 7 px (bbox (0,1161)–(7,1509)), không bao phần tay/tay lái ở mép trái (khoảng x 0–90, y 1160–1660). Cần vẽ lại theo phần thân xe thấy được. |
| adasind_102750.jpg | (không có polygon) | R07 | **Thiếu `ego_body`**: tay áo và tay lái ở mép trái phía dưới (khoảng x 0–120, y 1080–1520). |
| adasind_086220.jpg | L4 | R04 | `Bus` (322,962)–(377,1009) cao 47 px: phóng to thấy một xe van/xe con màu trắng, không thấy kích thước hay cửa kiểu xe buýt. Theo R04 van chở người → `Car`; cần xem lại class. |
| adasind_102750.jpg | L5 | R04 | `Car` (0,848)–(87,969) ở mép trái: phóng to thấy thân cao, đuôi mở, dáng xe ba bánh chở người/hàng nhìn từ sau hơn là ô tô con. Cần xem lại `ThreeWheeler` (hoặc `Truck` nếu là xe tải nhỏ). `truncated=true` đúng vì chạm mép ảnh. |
| adasind_060000.jpg | vùng (270,855)–(360,917) | R01 | Giữa L4 và L10 có thêm 1–2 xe ba bánh và một xe máy ở xa, cao khoảng 45–60 px, chưa có box. Ảnh nhỏ nên cần soát lại chiều cao từng vật trước khi thêm. |
| adasind_060000.jpg | L7, L8, L9 | R01 | Ba `Pedestrian` cao 42–43 px, sát ngưỡng H=40; giữ được nhưng cần chắc box bám đúng đỉnh đầu và chân. |

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.
