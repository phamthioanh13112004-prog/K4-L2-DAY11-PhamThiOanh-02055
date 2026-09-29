# Rework delta

| zone | matched before | matched after | missing before | missing after | spurious before | spurious after |
|---|---:|---:|---:|---:|---:|---:|
| center | 4 | 5 | 2 | 1 | 2 | 2 |
| mid | 4 | 4 | 2 | 2 | 1 | 1 |
| edge | 4 | 4 | 1 | 1 | 1 | 1 |

## Findings action=rework
- adasind_019560.jpg L1 SPURIOUS: không áp dụng
- adasind_019560.jpg L8 SPURIOUS: không áp dụng
- adasind_128310.jpg R4+M6 MISSING: đã sửa
- adasind_199770.jpg R3+M10 MISSING: chưa sửa
- adasind_199770.jpg R4 MISSING: chưa sửa

## Đối chiếu thủ công ca R4 sau export

Trong CVAT Job #13, đã bỏ polygon `ego_body` bên phải che xe khác và thêm box `ThreeWheeler` `(926.08, 820.79)–(1075.08, 1299.57)`, `truncated=true`. Export mới là `submission/R3-B3-edge.zip`, mã khóa rework `419F-1DFD`; [ảnh CVAT sau sửa](../screenshots/B3-edge_199770_R4_fixed.png). Bản khóa `r1_craft` không thay đổi.

Dòng tự tính R4 vẫn là “chưa sửa” vì teaching reference chứa chính box R4 `(935, 990)–(1080, 1300)` hoàn toàn bên trong polygon `ignore_region` của reference `(924, 813)–(1080, 1552)`. Hàm so sánh loại box mới khi nó nằm trong polygon đó; việc này đã được xác nhận với `ignored_by_reference=True` cho cả box mới và R4. Giữ nguyên bảng số và trạng thái do lệnh tạo, không chỉnh tay để báo cải thiện. Cần Lab Coach kiểm tra phạm vi ignore trong teaching reference; B cần xác nhận lại nhãn trên ảnh. Ca Pedestrian R3 vẫn chưa sửa.
