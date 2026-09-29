# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| `B3-edge` · `adasind_199770.jpg` | QA thấy polygon `P4` sai phạm vi và L7 dưới H; compare có 2 ca geometry, 2 missing ở mid và các vật mép phải cần kiểm | Ưu tiên P0 `ego_body` che vật thật rồi kiểm từng Bike/ThreeWheeler bị cắt biên | Ảnh gốc, XML khóa `CD87-D5B5`, `qa_review.md`, compare và ảnh chụp CVAT khi có |
| `B3-edge` · `adasind_128310.jpg` | R4/M6 Car trắng thiếu ở L; M4 chỉ bao một phần Truck lớn | Ca thiếu Car rõ trên ảnh và ca box model lỏng giúp hiệu chuẩn cách tìm vật nhỏ ở giữa và xe lớn ở rìa | Ảnh gốc, L/R/M overlay, `local_quality_conflicts.csv`, quyết định `QA-01` |

Giới hạn của kết luận từ ba frame ADASIND: đây là một slice từ một camera, không chứa tracking hoặc vùng seam bốn camera. Teaching reference là bản dạy học, chưa được nhiều người duyệt. Không dùng số lỗi ở ba ảnh này để ước lượng tỷ lệ lỗi ngoài tập mẫu.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh
như nhiều ca độc lập), và vì sao kế hoạch đó chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi: lấy đúng 8 tổ hợp `front/rear/left/right × normal/hard`, cộng 200 frame; chia theo hành trình, thời điểm, ánh sáng và cảnh để tránh chọn các frame liền nhau của một lần xuất hiện. Mỗi camera có hard case riêng, kể cả seam. Ghi số cảnh độc lập và điều kiện lấy mẫu trước khi diễn giải tỷ lệ lỗi; kế hoạch này cố ý tăng hard case nên không đại diện tự động cho phân bố 50.000 frame giả lập.
