# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide,
**không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có
normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference
ADASIND hoặc nhãn bạn vừa vẽ. Nếu cần, dùng `notebooks/day11-svm360-colab.ipynb` để thử tổng phân bổ; notebook
không làm thay phần lý do.

| camera_id | Hard case cần chọn | Vì sao dễ sai | Annotation space / calibration cần giữ | Cách review trước khi gọi là gold |
|---|---|---|---|---|
| front | Vật nhỏ ở xa, bị che một phần, lóa/ngược sáng và vật đi vào vùng overlap với camera bên | Kích thước nhỏ, tương phản thấp và vùng giao nhau làm ranh giới object/visibility khó thống nhất | Ảnh gốc theo camera, mask hợp lệ/ignore, phiên bản calibration intrinsics/extrinsics và quy ước tọa độ; không suy ra BEV nếu chưa có calibration | Hai annotator gán độc lập, adjudicator xem ảnh gốc cùng projection đã hiệu chuẩn; ghi rõ bất đồng và phiên bản rule |
| rear | Xe/người khuất một phần, cảnh tối hoặc chói, vật tại overlap phía sau-góc | Occlusion và điều kiện chiếu sáng làm thiếu/thừa box dễ xảy ra; overlap có thể khiến cùng vật xuất hiện hai lần | Frame rear đồng bộ, mask vùng hợp lệ, calibration có phiên bản và timestamp đồng bộ với camera kề | Review độc lập theo cùng checklist; kiểm tra các ca khó bằng frame lân cận nếu policy cho phép, rồi adjudicate và lưu lý do |
| left | Xe máy/người đi bộ chen cụm, vật bị cắt ở rìa và vật tại overlap trước/sau bên trái | Mật độ đối tượng, méo rìa và truncation làm tách instance, class và extent không ổn định | Ảnh gốc left, lens/ignore masks, calibration và định nghĩa ranh giới instance; lưu đồng bộ thời gian với front/rear | Lấy mẫu có cả cảnh thường và khó; hai lượt độc lập, adjudicator kiểm class, visibility, box và mọi liên kết cross-camera |
| right | Cụm phương tiện/người, vật nhỏ hoặc che khuất ở rìa và vùng overlap trước/sau bên phải | Cùng vật có thể bị che khác nhau theo góc nhìn; box không nhất thiết có hình dạng tương tự giữa camera | Ảnh gốc right, mask vùng hợp lệ, calibration và timestamp đồng bộ; giữ annotation theo từng camera trước khi áp dụng policy hợp nhất | Hai annotator độc lập và adjudication; xác nhận từng camera label trước, chỉ hợp nhất sau khi có bằng chứng đồng bộ và policy |

- Khi nào cần refresh gold set (đổi camera, calibration hoặc rule): refresh khi thay/lắp lại camera hoặc lens, thay calibration hay preprocessing, đổi taxonomy/rule, phát hiện drift miền dữ liệu hoặc có lỗi lặp lại trong audit; giữ phiên bản cũ để so sánh và tạo lại mẫu đại diện sau thay đổi.
- Một ca seam/cross-camera cần policy và evidence trước khi ghép hai box: cùng một xe đi từ front sang right/left ở góc overlap. Chỉ liên kết khi có timestamp đồng bộ, calibration/transform được xác nhận, tiêu chí continuity rõ và reviewer kiểm được ảnh ở cả hai camera; nếu thiếu điều kiện, giữ hai annotation camera-local, không tự gán chung track ID.
- Vì sao peer agreement hoặc quality report trên ảnh một camera chưa chứng minh gold set đúng cho cả bốn camera: người review có thể cùng chia sẻ một lỗi quy tắc; mỗi camera có góc nhìn, méo, occlusion và phân bố cảnh khác nhau; chỉ số trên một camera/slice không đo coverage, calibration hay lỗi cross-camera. Cần adjudication độc lập theo từng camera và audit seam riêng.
