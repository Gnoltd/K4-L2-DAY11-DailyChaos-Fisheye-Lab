# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `8f870d1e40b07271b28c04c479f292f9a93b1b53542e6d4584184db95152d4d5`; slice `B1-center`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_006840.jpg, adasind_036720.jpg, adasind_056040.jpg. Frame thiếu trong export: không.
TP=19; FP=3; FN=1; số lần đối chiếu=22; mean IoU của TP=0.812.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.864 | 0.964 | 0.955 |
| precision | 0.864 | 0.710 | 0.000 |
| recall | 0.950 | 0.771 | 0.000 |
| jaccard | 0.826 | 0.681 | 0.000 |
| dice | 0.905 | 0.734 | 0.000 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 6 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |
| Bus | 0 | 1 | 0 | 0.955 | 0.000 | 0.000 | 0.000 | 0.000 |
| Car | 3 | 1 | 0 | 0.955 | 0.750 | 1.000 | 0.750 | 0.857 |
| Pedestrian | 4 | 1 | 0 | 0.955 | 0.800 | 1.000 | 0.800 | 0.889 |
| ThreeWheeler | 6 | 0 | 1 | 0.955 | 1.000 | 0.857 | 0.857 | 0.923 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_006840.jpg | 8 | 2 | 1 | 0.800 | 0.800 | 0.889 |
| adasind_036720.jpg | 4 | 0 | 0 | 1.000 | 1.000 | 1.000 |
| adasind_056040.jpg | 7 | 1 | 0 | 0.875 | 0.875 | 1.000 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Bus | Car | Pedestrian | ThreeWheeler | <missing> |
|---|---:|---:|---:|---:|---:|---:|
| Bike | 6 | 0 | 0 | 0 | 0 | 0 |
| Bus | 0 | 0 | 0 | 0 | 0 | 0 |
| Car | 0 | 0 | 3 | 0 | 0 | 0 |
| Pedestrian | 0 | 0 | 0 | 4 | 0 | 0 |
| ThreeWheeler | 0 | 1 | 0 | 0 | 6 | 0 |
| <extra> | 0 | 0 | 1 | 1 | 0 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
