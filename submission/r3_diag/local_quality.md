# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `cd87d5b56d927c5f2c0c777739dd08a9c82522435569cacb93595cf0e0dae595`; slice `B3-edge`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_123090.jpg, adasind_128310.jpg, adasind_199770.jpg. Frame thiếu trong export: không.
TP=12; FP=4; FN=5; số lần đối chiếu=21; mean IoU của TP=0.829.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.571 | 0.914 | 0.810 |
| precision | 0.750 | 0.767 | 0.500 |
| recall | 0.706 | 0.700 | 0.500 |
| jaccard | 0.571 | 0.600 | 0.333 |
| dice | 0.727 | 0.727 | 0.500 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 2 | 2 | 2 | 0.810 | 0.500 | 0.500 | 0.333 | 0.500 |
| Car | 2 | 0 | 1 | 0.952 | 1.000 | 0.667 | 0.667 | 0.800 |
| Pedestrian | 2 | 1 | 1 | 0.905 | 0.667 | 0.667 | 0.500 | 0.667 |
| ThreeWheeler | 2 | 1 | 1 | 0.905 | 0.667 | 0.667 | 0.500 | 0.667 |
| Truck | 4 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_123090.jpg | 3 | 0 | 0 | 1.000 | 1.000 | 1.000 |
| adasind_128310.jpg | 4 | 0 | 1 | 0.800 | 1.000 | 0.800 |
| adasind_199770.jpg | 5 | 4 | 4 | 0.385 | 0.556 | 0.556 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Car | Pedestrian | ThreeWheeler | Truck | <missing> |
|---|---:|---:|---:|---:|---:|---:|
| Bike | 2 | 0 | 0 | 0 | 0 | 2 |
| Car | 0 | 2 | 0 | 0 | 0 | 1 |
| Pedestrian | 0 | 0 | 2 | 0 | 0 | 1 |
| ThreeWheeler | 0 | 0 | 0 | 2 | 0 | 1 |
| Truck | 0 | 0 | 0 | 0 | 4 | 0 |
| <extra> | 2 | 0 | 1 | 1 | 0 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
