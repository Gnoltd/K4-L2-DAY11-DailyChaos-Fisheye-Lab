# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `e89d402cb0fdd0da5ee6128112e88152b8e8a5448c49826e0c21a14e2593c34c`; slice `B2-mid`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_060000.jpg, adasind_086220.jpg, adasind_102750.jpg. Frame thiếu trong export: không.
TP=15; FP=6; FN=5; số lần đối chiếu=25; mean IoU của TP=0.832.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.600 | 0.927 | 0.880 |
| precision | 0.714 | 0.537 | 0.000 |
| recall | 0.750 | 0.454 | 0.000 |
| jaccard | 0.577 | 0.367 | 0.000 |
| dice | 0.732 | 0.460 | 0.000 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 2 | 1 | 2 | 0.880 | 0.667 | 0.500 | 0.400 | 0.571 |
| Bus | 0 | 1 | 0 | 0.960 | 0.000 | 0.000 | 0.000 | 0.000 |
| Car | 0 | 1 | 0 | 0.960 | 0.000 | 0.000 | 0.000 | 0.000 |
| Pedestrian | 4 | 2 | 0 | 0.920 | 0.667 | 1.000 | 0.667 | 0.800 |
| ThreeWheeler | 8 | 1 | 1 | 0.920 | 0.889 | 0.889 | 0.800 | 0.889 |
| Truck | 1 | 0 | 2 | 0.920 | 1.000 | 0.333 | 0.333 | 0.500 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_060000.jpg | 8 | 2 | 2 | 0.667 | 0.800 | 0.800 |
| adasind_086220.jpg | 4 | 2 | 1 | 0.571 | 0.667 | 0.800 |
| adasind_102750.jpg | 3 | 2 | 2 | 0.500 | 0.600 | 0.600 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Bus | Car | Pedestrian | ThreeWheeler | Truck | <missing> |
|---|---:|---:|---:|---:|---:|---:|---:|
| Bike | 2 | 0 | 0 | 0 | 0 | 0 | 2 |
| Bus | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| Car | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| Pedestrian | 0 | 0 | 0 | 4 | 0 | 0 | 0 |
| ThreeWheeler | 0 | 0 | 0 | 0 | 8 | 0 | 1 |
| Truck | 0 | 0 | 1 | 0 | 0 | 1 | 1 |
| <extra> | 1 | 1 | 0 | 2 | 1 | 0 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
