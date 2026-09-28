# Escalation ticket

## Ticket 1

- **Frame:** `adasind_258420.jpg (L2+R1/M4, L3+R4/M8, L4+R8/M11) và adasind_310008.jpg (L5+R1/M6, M7)`
- **Ảnh chụp:** `submission/screenshots/01_model_threewheeler_258420.png`
- **Expected impact:** `Model YOLO26m gọi cả 4 auto-rickshaw của slice là Truck, Car hoặc Bus (có box bị gán cả Truck lẫn Bus). Nếu dùng model làm pre-label hoặc để so chất lượng, mọi ThreeWheeler sẽ bị tính là MISSING + SPURIOUS, làm cột M của zone_table (center 2+2, mid 3+8) phóng đại lỗi và che lỗi thật của người gán nhãn.`
- **Owner:** `ai_team`
- **Recommendation:** `Không dùng số của model cho class ThreeWheeler cho tới khi có lớp tương ứng; trước mắt ánh xạ lại các class gần (Truck/Car/Bus trên box auto-rickshaw) chỉ khi người soát xác nhận, về lâu dài fine-tune trên ảnh fisheye có auto-rickshaw và kiểm lại trên 48 frame. Findings liên quan: r3_diag action=escalate.`

## Ticket 2

- **Frame:** `adasind_019560.jpg (C0, L4 zone mid, x≈324–368, y≈741–832)`
- **Ảnh chụp:** `submission/screenshots/02_c0_019560_L4.png`
- **Expected impact:** `Có một vật cao ≈91 px (≥40) bị che giữa hai rickshaw mà teaching reference không có box; mình chưa phân biệt được là xe đạp (Bike) hay xích lô (ThreeWheeler). Nếu reference thiếu thật, mọi người vẽ box ở đây đều bị tính SPURIOUS và số calib bị lệch.`
- **Owner:** `qa`
- **Recommendation:** `Người quản lý reference xem ảnh gốc độ phân giải đầy đủ, quyết định có box hay không và class nào theo R01/R04; ghi quyết định vào reference và decision log. Cùng lượt, bổ sung L8 (xe máy đỗ) của frame này vào reference.`
