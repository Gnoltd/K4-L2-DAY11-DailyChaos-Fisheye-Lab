# Thành viên và phân vai — Day11 SVM 360 Fisheye

## 1. Thông tin nhóm

- Khóa/lớp: K4-L2
- Tên nhóm: DailyChaos
- Repo Public: https://github.com/Gnoltd/K4-L2-DAY11-DailyChaos-Fisheye-Lab
- Máy giữ hồ sơ chính / người quản lý: máy của Đỗ Thành Long (CVAT local, `exports/`, `data/_ref/`); hồ sơ chung ở nhánh `main`
- Slice chung lấy từ mode.json: **B1-center** (`adasind_006840.jpg`, `adasind_036720.jpg`, `adasind_056040.jpg`)
- Tên định danh vai A dùng cho --self: `long` (`python3 lab11.py mode --members long,tung,hoang --self long`)
- Kênh trao đổi nội bộ: [Điền]
- Đại diện nộp (vai C): Đào Xuân Tùng, 2A202602177
- Commit chốt bài: [SHA hoặc URL commit — C điền khi nộp]

## 2. Ba vai chính

| Vai | Họ và tên | MSSV | Tên định danh trong mode | Trách nhiệm | Bằng chứng đóng góp |
|---|---|---|---|---|---|
| A · Gán nhãn | Đỗ Thành Long | 2A202602199 | long | Parking/C0/slice, self-QC, lock, rework | `submission/parking/`, `p1_calib/` (lock 1605-E959), `r1_craft/` (lock 8F87-0D1E, selfqc 9 mục), `rework/` (lock2 8F87-0D1E, delta); commit `8d79122`, `9da5adc` |
| B · QA độc lập | Nguyễn Văn Hoàng | 2A202602176 | hoang | Review trước reference, finding QA, kiểm lại ca sửa | [Chờ: `submission/r2_qa/qa_review.md`, `qa_overlay.html`, ≥3 dòng `r2_qa` trong findings, ảnh bằng chứng, commit] |
| C · Chẩn đoán & điều phối | Đào Xuân Tùng | 2A202602177 | tung | Báo cáo, phân xử, kế hoạch, tích hợp, check và nộp | [Chờ: kiểm và xác nhận `r3_diag/`, dòng `r3_diag`, `10_error_card.md`, 20/30/40/45/46/50, phân xử QA của B, `check`, commit chốt] |

Bảng này xác định vai của nhóm. Vòng QA tự sinh trong team.json thuộc quy trình nhiều hồ sơ của CLI; nhóm dùng một slice chung và quy trình A → B → C đã nêu trong hướng dẫn.

## 3. Bàn giao theo pha

| Mốc | Người giao → nhận | File / commit / mã khóa | Người nhận đã kiểm gì? | Trạng thái / vướng mắc |
|---|---|---|---|---|
| P0 · Chốt môi trường và vai | C → A, B | `00_setup/mode.json` (slice B1-center), `parking/annotations.xml` (20 parking_line, 2 free_space) | [C/B điền] | Xong phần A. Vai A/B/C chốt muộn, xem mục 4 |
| P2 · Khóa bản đầu | A → B, C | `r1_craft/annotations.xml`, `lock.txt`, slice B1-center, mã **8F87-0D1E**, commit `8d79122` | [B điền: mã khớp khi chạy `qa`] | Xong |
| P3 · Chốt QA mù | B → C, A | [`r2_qa/qa_review.md`, findings r2_qa, ảnh, commit] | [C điền] | **Chờ B** |
| P4 · Quyết định sửa | C → A, B | `r3_diag/`, findings r3_diag, `40_decision_log.csv` D1–D5, commit `2f6e6f5` | [C điền sau khi kiểm] | Bản nháp đã có; C cần kiểm và phân xử thêm các ca QA của B |
| P5 · Kiểm bản sửa | A → B → C | `rework/annotations-v2.xml`, `lock2.txt` (8F87-0D1E, không đổi nhãn), `delta.md` | [B điền: kiểm lại ca giữ nhãn] | Không có ca rework; 2 ca keep_with_reason, 1 ca escalate |
| P6 · Chốt nộp | A, B → C | `manifest.json`, commit chốt | [C điền] | Chờ P3 |

## 4. Bất đồng và phối hợp

- Một ca đã phân xử: `adasind_006840.jpg` L9 (303,818)–(360,879), R04 — A gán `Bus` (xe to hơn xe ba bánh bên cạnh, đuôi lớn, có kính góc trái), teaching reference gọi `ThreeWheeler`. Quyết định: giữ nhãn, `E0_reference_defect`, `keep_with_reason` (findings r1_craft L9+R4, r3_diag L9+M12/R4; decision log D2; `screenshots/006840_bus_vs_threewheeler_L_vs_R.png`). Chờ B kiểm độc lập và C xác nhận lần cuối.
- Ca còn mở: `adasind_056040.jpg` L3 Pedestrian (219,772)–(245,861), R03 — người ngồi sau hay đứng cạnh xe máy. Người theo dõi: C. Phép kiểm tiếp: xem frame liền kề trong video ADASIND gốc (`30_escalation_ticket.md`, decision log D5, status escalated).
- Đóng góp của A/B/C vào kế hoạch và exit ticket: bản nháp `45_sampling_plan.csv`, `45_review_plan.md`, `46_gold_set_plan.md`, `50_exit_ticket.md` được soạn trên máy chính trong lúc A làm; [C kiểm, sửa và ghi phần mình đóng góp; B bổ sung nếu có].
- Thay đổi phân công nếu có: **Có.** Lúc đầu (khoảng 15:30–18:30 ngày 2026-09-28) nhóm làm theo mô hình mỗi người một hồ sơ trên branch riêng: `long` → B1-center, `tung` → B2-mid (khoá E89D-402C), `hoang` → B4-edge. Sau khi nhận hướng dẫn nhóm (~18:45), nhóm chuyển sang một hồ sơ chung trên slice B1-center của A. Hệ quả cần ghi rõ:
  - Teaching reference B1-center đã được mở (P4) **trước** khi có QA mù của B. QA của B vẫn làm mù: B không mở `findings.csv`, `r3_diag/`, `rework/` hay reference trước khi chốt review.
  - Bản cold review A tự làm và bản QA của A cho bài B2-mid của Tùng **không** được tính là QA của nhóm; đã chuyển ra `archive/pre-group-long/`.
  - Bài B2-mid (branch `tung`) và B4-edge (branch `hoang`) là phần luyện tập riêng, không thuộc hồ sơ nộp.

## 5. Xác nhận trước khi nộp

- [ ] A xác nhận nhãn và export đúng phiên bản: [Đỗ Thành Long / `r1_craft/lock.txt`, `rework/lock2.txt`]
- [ ] B xác nhận đã QA độc lập trước reference và kiểm lại ca sửa: [Nguyễn Văn Hoàng / bằng chứng]
- [ ] C xác nhận báo cáo đúng bản khóa, các file đầy đủ và check exit 0: [Đào Xuân Tùng / bằng chứng]
- [ ] manifest.json tại commit chốt có failed_gates rỗng.
- [ ] Repo nhóm Public, ảnh và các bằng chứng mở được.
- [ ] C đã push và gửi link repo nhóm + commit qua kênh lớp công bố.

Chỉ đánh dấu việc đã kiểm thật. Nhóm nộp một hồ sơ chung; check không tự chấm đóng góp từng người. Giữ nguyên header/các cột enum của findings.csv; tên người được ghi trong tài liệu này hoặc phần note thích hợp.
