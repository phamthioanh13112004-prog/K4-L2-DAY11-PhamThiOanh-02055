# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 6 | 2 | 2 | 2 | 5 | MISSING (1) |
| mid | 6 | 2 | 1 | 3 | 4 | MISSING (2) |
| edge | 5 | 1 | 1 | 3 | 3 | BOX_GEOMETRY (1) |

## Nhận xét

- L có nhiều khác biệt nhất ở `center` và `mid`: mỗi zone thiếu 2 box; `center` còn thừa 2 box. Phần lớn tập trung ở frame `adasind_199770.jpg`, còn `adasind_123090.jpg` khớp 3/3 box với teaching reference ở ngưỡng IoU 0,5. M thiếu 3 ở `mid` và 3 ở `edge`; số M thừa cao nhất ở `center` (5). Các hàng số phía trên là phép đếm từ ba ảnh, không phải tỷ lệ lỗi cho camera thật.
- Ca rõ: ở `adasind_128310.jpg`, L thiếu Car trắng R4/M6 giữa đường. Ở `adasind_199770.jpg`, polygon `ego_body` bên phải của L phủ một xe khác; R4 là ThreeWheeler tại mép phải. M cũng nhầm một số class xe nhỏ hoặc bị cắt biên (`M6`, `M8`, `M13` trong frame 199770), nhưng đây mới là giả thuyết lỗi model từ vài ví dụ. Những box chênh IoU như L3/R9 và cặp Bike mép trái cần xem ảnh phóng to trước khi quyết định sửa theo reference. `center/mid/edge` chỉ là khoảng cách tương đối tới tâm vòng kính; ba frame và teaching reference chưa được kiểm độc lập không đủ để kết luận chất lượng hệ SVM bốn camera.
