# Thành viên và phân vai — Day11 SVM 360 Fisheye

## 1. Thông tin nhóm

- Khóa/lớp: K4-L2
- Tên nhóm: DailyChaos
- Repo Public: https://github.com/Gnoltd/K4-L2-DAY11-DailyChaos-Fisheye-Lab
- Máy giữ hồ sơ chính / người quản lý: máy của Đỗ Thành Long (CVAT local, `exports/`, `data/_ref/`); hồ sơ chung ở nhánh `main`
- Slice chung lấy từ mode.json: **B1-center** (`adasind_006840.jpg`, `adasind_036720.jpg`, `adasind_056040.jpg`)
- Tên định danh vai A dùng cho --self: `long` (`python3 lab11.py mode --members long,tung,hoang --self long`)
- Kênh trao đổi nội bộ: làm trực tiếp cùng nhau trên máy chính của Long (một người sửa một file tại một thời điểm); branch cá nhân `long`, `tung`, `hoang` chỉ dùng để chuyển file
- Đại diện nộp (vai C): Đào Xuân Tùng, 2A202602177
- Commit chốt bài: [SHA hoặc URL commit — C điền khi nộp]

## 2. Ba vai chính

| Vai | Họ và tên | MSSV | Tên định danh trong mode | Trách nhiệm | Bằng chứng đóng góp |
|---|---|---|---|---|---|
| A · Gán nhãn | Đỗ Thành Long | 2A202602199 | long | Parking/C0/slice, self-QC, lock, rework | `submission/parking/`, `p1_calib/` (lock 1605-E959), `r1_craft/` (lock 8F87-0D1E, selfqc 9 mục), `rework/` (lock2 7968-8D80 sau phân xử QA, delta); commit `8d79122`, `9da5adc` |
| B · QA độc lập | Nguyễn Văn Hoàng | 2A202602176 | hoang | Review trước reference, finding QA, kiểm lại ca sửa | `submission/r2_qa/qa_review.md` + `qa_overlay.html` (QA mù bản 8F87-0D1E, 3 frame, 5 nhận xét), 4 dòng `r2_qa` trong findings; commit `4c89c63` trên branch `hoang`, tích hợp vào `main` |
| C · Chẩn đoán & điều phối | Đào Xuân Tùng | 2A202602177 | tung | Báo cáo, phân xử, kế hoạch, tích hợp, check và nộp | Phân xử 4 nhận xét QA của B: 4 dòng `r3_diag` mới (2 rework ở 056040 L7, 1 rework thêm Pedestrian 006840, 1 escalate), decision log D6–D8, `30_escalation_ticket.md` Ticket 2, 2 screenshot; kiểm lại cùng A bản P4–P6 (`r3_diag/`, `10_error_card.md`, 20/40/45/46/50); `check`, commit chốt |

Bảng này xác định vai của nhóm. Vòng QA tự sinh trong team.json thuộc quy trình nhiều hồ sơ của CLI; nhóm dùng một slice chung và quy trình A → B → C đã nêu trong hướng dẫn.

## 3. Bàn giao theo pha

| Mốc | Người giao → nhận | File / commit / mã khóa | Người nhận đã kiểm gì? | Trạng thái / vướng mắc |
|---|---|---|---|---|
| P0 · Chốt môi trường và vai | C → A, B | `00_setup/mode.json` (slice B1-center), `parking/annotations.xml` (20 parking_line, 2 free_space) | C (Tùng) kiểm `mode.json` self=long, slice B1-center; B (Hoàng) đối chiếu 2 vạch chia ô và vạch dài giữa hai dãy ô với `observations.md` | Xong. Vai A/B/C chốt muộn, xem mục 4 |
| P2 · Khóa bản đầu | A → B, C | `r1_craft/annotations.xml`, `lock.txt`, slice B1-center, mã **8F87-0D1E**, commit `8d79122` | B (Hoàng) chạy `qa --code 8F87-0D1E`: mã khớp file khoá, đủ 3 frame; C (Tùng) kiểm `selfqc.md` 9 mục đã tick | Xong |
| P3 · Chốt QA mù | B → C, A | `r2_qa/qa_review.md`, `qa_overlay.html`, 4 dòng r2_qa; commit `4c89c63` (branch `hoang`) | Mã 8F87-0D1E khớp khi B chạy `qa`; overlay đúng 3 frame B1-center; C (Tùng) kiểm 5 nhận xét đều có frame/object_ref/rule_id và 4 dòng r2_qa để trống `why` | QA đã chốt. Chờ C phân xử 4 nhận xét (2 MISSING ở 006840, BOX_GEOMETRY + ATTRIBUTE ở 056040 L7) |
| P4 · Quyết định sửa | C → A, B | `r3_diag/`, findings r3_diag, `40_decision_log.csv` D1–D8, Ticket 1–2 | C (Tùng) cùng A đối chiếu từng nhận xét QA với ảnh gốc phóng to, reference R7 và model M6 | Giao A rework: thêm Pedestrian 006840 (92,838)–(106,902); 056040 L7 thu về x≈80, bỏ truncated. 1 ca escalate (D7) |
| P5 · Kiểm bản sửa | A → B → C | `rework/annotations-v2.xml`, `lock2.txt` (relock **7968-8D80**, lịch sử 8F87-0D1E), `delta.md` | C (Tùng) so bản export với bản khoá r1_craft: đúng 3 thay đổi (thêm Pedestrian 006840, Car 056040 x=103 + truncated=false); B (Hoàng) mở lại ảnh 006840 và 056040 xác nhận Pedestrian mới `occluded=true`, Car 056040 bám phần thấy và bỏ `truncated` | Xong. Spurious mid 1→2 do reference thiếu người áo trắng (xem delta.md) |
| P6 · Chốt nộp | A, B → C | `manifest.json`, commit chốt | C (Tùng) chạy `triage`, `status`, `check` trên máy chính: exit 0, `failed_gates` rỗng; A/B đọc lại phần của mình | Chốt; commit ghi ở mục 1 |

## 4. Bất đồng và phối hợp

- Một ca đã phân xử: `adasind_006840.jpg` L9 (303,818)–(360,879), R04 — A gán `Bus` (xe to hơn xe ba bánh bên cạnh, đuôi lớn, có kính góc trái), teaching reference gọi `ThreeWheeler`. Quyết định: giữ nhãn, `E0_reference_defect`, `keep_with_reason` (findings r1_craft L9+R4, r3_diag L9+M12/R4; decision log D2; `screenshots/006840_bus_vs_threewheeler_L_vs_R.png`). Chờ B kiểm độc lập và C xác nhận lần cuối.
- Ca đã phân xử thứ hai: `adasind_056040.jpg` L7 Car, R02/R05 — A giữ box tới x=0 (cho rằng phần xe thấy tới mép ảnh); B (Hoàng) chỉ ra xe chỉ thấy từ x≈83, phần trái là rider L8. C (Tùng) đối chiếu reference R7 (80,755)–(195,990) và model M6 (81,751)–(192,982), quyết định rework: thu về x≈80, bỏ truncated (D8).
- Ca còn mở: `adasind_006840.jpg` người cạnh xe ba bánh L3 (368,825)–(392,900) — đứng ngoài hay ngồi trong xe (Ticket 2, D7, người theo dõi: C).
- Ca còn mở: `adasind_056040.jpg` L3 Pedestrian (219,772)–(245,861), R03 — người ngồi sau hay đứng cạnh xe máy. Người theo dõi: C. Phép kiểm tiếp: xem frame liền kề trong video ADASIND gốc (`30_escalation_ticket.md`, decision log D5, status escalated).
- Đóng góp của A/B/C vào kế hoạch và exit ticket: bản nháp `45_sampling_plan.csv`, `45_review_plan.md`, `46_gold_set_plan.md`, `50_exit_ticket.md` được soạn trên máy chính trong lúc A làm; C (Tùng) kiểm từng số/claim với báo cáo và ảnh, bổ sung Ticket 2, decision log D6–D9 và phản hồi QA trong findings; B (Hoàng) đối chiếu `50_exit_ticket.md` câu 3 và `20_guideline_patch.md` (R03b) với các ca rider/người đứng cạnh xe mà B đã nêu. Cả ba đọc và thống nhất bản cuối.
- Thay đổi phân công nếu có: **Có.** Lúc đầu (khoảng 15:30–18:30 ngày 2026-09-28) nhóm làm theo mô hình mỗi người một hồ sơ trên branch riêng: `long` → B1-center, `tung` → B2-mid (khoá E89D-402C), `hoang` → B4-edge. Sau khi nhận hướng dẫn nhóm (~18:45), nhóm chuyển sang một hồ sơ chung trên slice B1-center của A. Hệ quả cần ghi rõ:
  - Teaching reference B1-center đã được mở (P4) **trước** khi có QA mù của B. QA của B vẫn làm mù: B không mở `findings.csv`, `r3_diag/`, `rework/` hay reference trước khi chốt review.
  - Bản cold review A tự làm và bản QA của A cho bài B2-mid của Tùng **không** được tính là QA của nhóm; đã chuyển ra `archive/pre-group-long/`.
  - Bài B2-mid (branch `tung`) và B4-edge (branch `hoang`) là phần luyện tập riêng, không thuộc hồ sơ nộp.

## 5. Xác nhận trước khi nộp

- [x] A xác nhận nhãn và export đúng phiên bản: Đỗ Thành Long / `r1_craft/lock.txt` (8F87-0D1E), `rework/lock2.txt` (7968-8D80), export từ trang task CVAT
- [x] B xác nhận đã QA độc lập và kiểm lại ca sửa: Nguyễn Văn Hoàng / `r2_qa/qa_review.md`, commit `4c89c63`; kiểm lại rework ở mốc P5. Lưu ý: reference B1-center đã được A mở trước khi B QA (mục 4), B không đọc reference/findings/r3_diag khi soát
- [x] C xác nhận báo cáo đúng bản khóa, các file đầy đủ và check exit 0: Đào Xuân Tùng / `r1_craft/reference.txt`, `rework/delta.md`, `manifest.json`
- [x] manifest.json tại commit chốt có failed_gates rỗng.
- [x] Repo nhóm Public, ảnh và các bằng chứng mở được.
- [ ] C đã push và gửi link repo nhóm + commit qua kênh lớp công bố. (Tùng tick sau khi gửi)

Chỉ đánh dấu việc đã kiểm thật. Nhóm nộp một hồ sơ chung; check không tự chấm đóng góp từng người. Giữ nguyên header/các cột enum của findings.csv; tên người được ghi trong tài liệu này hoặc phần note thích hợp.
