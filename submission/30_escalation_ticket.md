# Escalation ticket

## Ticket 1

- **Frame:** `adasind_056040.jpg`, object L3 `Pedestrian` (219,772)–(245,861), slice B1-center, zone mid.
  Liên quan: `findings.csv` dòng `r1_craft` L3 và `r3_diag` L3+M4 (`action=escalate`); `40_decision_log.csv` D5.
- **Ảnh chụp:** `submission/screenshots/056040_L3_pedestrian_escalate.png` (box L đỏ, box model M xanh dương).
- **Expected impact:** nếu đây là người ngồi sau thì box của mình là SPURIOUS và nhãn đúng là một `Bike` duy nhất;
  nếu là người đứng cạnh thì teaching reference thiếu một `Pedestrian` (E0). Ca này quyết định 1/1 spurious của zone
  mid trong slice (n_ref=7), và cùng loại bất đồng với `adasind_019560.jpg` người áo đỏ ở C0 — nếu không có quy ước,
  mọi slice có xe máy chở người sẽ cho số spurious/missing phụ thuộc người vẽ chứ không phụ thuộc ảnh.
- **Owner:** `qa` (phân xử ca cụ thể), chuyển `guideline` cho rule R03b.
- **Recommendation:** (1) người soát thứ ba xem frame liền trước/sau trong video ADASIND gốc để xác định người ngồi
  sau hay đứng cạnh, rồi cập nhật reference hoặc nhãn; (2) duyệt R03b trong `20_guideline_patch.md` (v1.1.0) để các
  ca không thấy chân/yên có quy tắc chung; (3) trong lúc chờ, không tính ca này vào so sánh chất lượng của slice.

## Ticket 2

- **Frame:** `adasind_006840.jpg`, vùng (368,825)–(392,900), slice B1-center, zone center — người áo trắng quần tối cạnh
  cột trước bên trái xe ba bánh L3 (362,789)–(568,1008). Nhận xét gốc: QA của B (Hoàng), `r2_qa` dòng 2.
  Liên quan: `findings.csv` dòng `r3_diag` `missing@x368-392,y825-900` (`action=escalate`); decision log D7.
- **Ảnh chụp:** `submission/screenshots/006840_person_beside_threewheeler_escalate.png` (trái: ảnh gốc phóng to 5×;
  phải: box L đỏ, reference xanh lá, vùng QA vàng).
- **Expected impact:** nếu người này đứng ngoài xe thì cả L và teaching reference đều thiếu một `Pedestrian` ~75 px ở
  center (recall center của slice đổi từ 9/10 thành 9/11 khi reference được sửa); nếu ngồi ở mép ghế trước thì theo
  R03 không box riêng và nhãn hiện tại đúng. Cùng họ với Ticket 1: R03 chưa nói cách quyết định khi không thấy chân
  hoặc chỗ ngồi.
- **Owner:** `qa` (phân xử ca), `guideline` (mở rộng R03b cho người sát xe ba bánh).
- **Recommendation:** người soát thứ ba xem frame liền trước/sau trong video ADASIND gốc; nếu chân chạm đất bên ngoài
  xe → thêm `Pedestrian` `occluded=true` vào nhãn và reference; nếu ở trong xe → giữ nguyên. Bổ sung ví dụ này vào
  R03b trong `20_guideline_patch.md`.
