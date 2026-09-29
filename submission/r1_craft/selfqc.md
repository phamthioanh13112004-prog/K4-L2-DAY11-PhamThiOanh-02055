# Tự soát

- adasind_199770.jpg L7: chiều cao < H (xem lại phạm vi)
- Tên task thiếu raw_fisheye

## Checklist thủ công
- [x] Phạm vi H=40 và vật cần vẽ
- [x] lens_border và ego_body
- [x] Class sáu nhãn
- [x] Rider và Bike
- [x] Geometry trên ảnh fisheye gốc
- [x] truncated và occluded
- [x] Vật thiếu hoặc box trùng
- [x] ignore_region có reason
- [x] Tên task raw_fisheye và export CVAT 1.1

## Fill ratio (K12)
chưa vẽ polygon K12 (degrade)

## Xác nhận tự soát

Cả 9 mục checklist đã được Oanh xác nhận đã rà soát. Dấu [x] ghi nhận việc rà soát, không khẳng định bản khóa R1 không còn lỗi. Ngoại lệ cần giữ để xử lý: L7 ở adasind_199770.jpg cao dưới H=40; bản export R1 cũ thiếu raw_fisheye trong metadata dù task CVAT hiện tại đã đặt đúng tên; R3 Pedestrian và sai lệch reference của R4 được ghi trong rework/delta.md. Bước xác nhận QA của thành viên B được bỏ qua theo yêu cầu của Oanh.
