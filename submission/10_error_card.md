# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B3 | BOX_GEOMETRY | 1 |
| center | B3 | MISSING | 4 |
| center | B3 | SPURIOUS | 7 |
| center | C0 | SPURIOUS | 2 |
| edge | B3 | BOX_GEOMETRY | 1 |
| edge | B3 | DUPLICATE | 1 |
| edge | B3 | MISSING | 3 |
| edge | B3 | SPURIOUS | 4 |
| mid | B3 | MISSING | 6 |
| mid | B3 | SPURIOUS | 5 |
| mid | C0 | SPURIOUS | 1 |
| unknown | B3 | IGNORE_SCOPE | 1 |

## Top defects
- SPURIOUS: 19 (ví dụ frame adasind_019560.jpg)
- MISSING: 13 (ví dụ frame adasind_128310.jpg)
- BOX_GEOMETRY: 2 (ví dụ frame adasind_199770.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ: `E1_annotator_error` ở frame `adasind_199770.jpg`, polygon `P4` đặt `reason=ego_body` lên xe khác ở mép phải. Điều này làm vùng cần gán nhãn bị loại khỏi phạm vi (`IGNORE_SCOPE`, R07/R09). Các dòng `M_only` nhiều ở `center` còn gồm model tách rider thành Pedestrian và nhầm class xe nhỏ; xem từng vật, không suy rằng mọi `SPURIOUS` đều có cùng nguyên nhân.
- Cách sửa: Theo yêu cầu của người dùng, Codex đã mở CVAT Job #13, bỏ polygon `ego_body` bên phải và thêm box `ThreeWheeler` cho xe bị cắt mép phải ở frame `adasind_199770.jpg`, với `truncated=true`. Bản export mới đã khóa với mã `419F-1DFD`; người giữ vai B vẫn cần kiểm lại. `delta.md` tiếp tục ghi R4 “chưa sửa” vì polygon ignore trong teaching reference bao trọn cả R4 lẫn box mới, nên bộ so sánh loại box này trước khi ghép cặp. Đây là giới hạn của phép so sánh, không phải bằng chứng để xóa box nhìn thấy trên ảnh. Ca Pedestrian R3 vẫn còn mở.
- Bằng chứng: `assets/images/adasind_199770.jpg`, `submission/r1_craft/annotations.xml`, `submission/rework/annotations-v2.xml`, `submission/rework/lock2.txt`, `submission/rework/delta.md`, `submission/findings.csv` (`r2_qa/P4`, `r3_diag/R4`) và R07/R09 trong `docs/02-rules-vi.md`. [Ảnh CVAT sau sửa R4](screenshots/B3-edge_199770_R4_fixed.png) cho thấy box xe mép phải; [ảnh frame 128310](screenshots/B3-edge_128310_car_rework.png) minh họa ca Car đã sửa trước đó.
