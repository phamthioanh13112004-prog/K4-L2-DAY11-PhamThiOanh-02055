# QA ảnh gốc · B3-edge

- Người soát kỹ thuật: Codex, theo yêu cầu của Oanh. Đây chưa phải xác nhận của thành viên giữ vai B.
- Chủ bản nhãn: `oanh` theo `submission/00_setup/mode.json`.
- Bản đã khóa: `submission/r1_craft/annotations.xml`; mã `CD87-D5B5`.
- Nguồn kiểm: ba ảnh trong `assets/images/`, XML đã khóa, `docs/02-rules-vi.md`; chưa dùng teaching reference hoặc model.
- Quy ước: `L#` là thứ tự **box** trong frame của XML. `P4` là shape thứ tư (polygon `ego_body` bên phải) trong frame `adasind_199770.jpg`.

## Soát từng frame

| frame | object_ref | rule_id | điều nhìn thấy và việc cần kiểm |
|---|---|---|---|
| `adasind_123090.jpg` | `L1–L3`, ignore polygons | R02, R03, R07, R08 | Đã xem ảnh gốc: Bike gồm người lái và xe, Car ở giữa, Truck bị cắt ở mép trái; polygon ego bên trái và hai lens border hiện có. Không ghi lỗi chắc chắn ở frame này. |
| `adasind_128310.jpg` | `L1–L4`, ignore polygons | R01, R04, R07, R08 | Đã xem ảnh gốc: người bên trái, xe đỏ giữa, xe tối bên trái và xe tải nhiều màu bên phải đều có box; polygon ego bên trái và hai lens border hiện có. Không ghi lỗi chắc chắn ở frame này. |
| `adasind_199770.jpg` | `P4` | R07, R09, R10 | Polygon `ego_body` bên phải, khoảng `x=926–1080, y=813–1555`, phủ lên phương tiện màu tối ở mép phải (điểm `1000,1000` nằm trong polygon). Phương tiện này nhìn tách khỏi người/xe mang camera bên trái. Kiểm lại phạm vi; nếu đúng là xe khác, bỏ polygon sai và gán box theo class nhìn được. Đây là lỗi phạm vi có thể che mất vật cần gán. |
| `adasind_199770.jpg` | `L7` | R01 | Box `Pedestrian` `(204.05,823.74)–(213.73,858.44)` cao `34.70 px`, dưới H=40. Kiểm lại đối tượng trên ảnh; nếu phần nhìn thấy chỉ cao như box hiện tại, loại box theo luật. |
| `adasind_199770.jpg` | `L8+L9` | R03, R02 | Hai box `Bike` ở nhóm xe nhỏ mép trái chồng vùng `x≈92–118, y≈836–891`. Ảnh có nhiều xe/người nhỏ; cần phóng to trong CVAT để xác nhận đây là hai rider/xe khác nhau, tránh box trùng một đối tượng. Chưa kết luận là lỗi trùng. |

## Bàn giao

Ba frame đã được xem theo ảnh gốc và XML khóa. Hai ca rõ cần xử lý là `P4` và `L7`; `L8+L9` là ca cần kiểm thêm bằng phóng to. Chưa sửa XML, chưa mở reference/model, chưa có ảnh chụp màn hình CVAT. Người giữ vai B của nhóm cần xác nhận lại nhận xét trước khi dùng đây làm QA mù chính thức của nhóm; sau đó C mới phân xử và chạy P4.
