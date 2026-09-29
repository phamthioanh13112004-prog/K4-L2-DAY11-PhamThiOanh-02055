# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide,
**không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có
normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference
ADASIND hoặc nhãn bạn vừa vẽ. Nếu cần, dùng `notebooks/day11-svm360-colab.ipynb` để thử tổng phân bổ; notebook
không làm thay phần lý do.

| camera_id | Hard case cần chọn | Vì sao dễ sai | Annotation space / calibration cần giữ | Cách review trước khi gọi là gold |
|---|---|---|---|---|
| front | Bike/người cắt ngang khi ngược sáng; normal là đường thẳng đủ sáng | Rider dễ bị tách khỏi xe, vật nhỏ ở rìa kính | Ảnh fisheye gốc, intrinsics, extrinsics, vòng kính, timestamp; nếu tạo BEV thì giữ ánh xạ sang ảnh gốc | Hai người gán độc lập theo R01–R09, so từng object và phân xử khác biệt trước khi đóng băng nhãn |
| rear | Người đi sau xe khi lùi, vật sát cản; normal là bãi đỗ thoáng | Thân xe ego che vật; dễ nhầm truncated với occluded | Ảnh gốc, vùng `ego_body`, calibration và timestamp đồng bộ với front/side | Reviewer thứ hai kiểm polygon ignore và box ngoài ignore; ca khó có ảnh và quyết định của người phân xử |
| left | Bike vượt sát sườn và đi qua seam front/left; normal là làn bên trái thông thoáng | Méo rìa và vật xuất hiện đồng thời ở hai camera | Intrinsics/extrinsics, FOV và mặt phẳng/biến đổi BEV nếu sử dụng | Hai reviewer kiểm từng camera trên ảnh gốc trước; chỉ so seam sau khi có timestamp và calibration |
| right | Người và xe ở lề phải, gần gương/ego; normal là đường bên phải đủ sáng | Dễ gán xe khác thành `ego_body`, như lỗi P4 đã thấy ở ADASIND một camera | Ảnh gốc, polygon ego, mốc hiệu chuẩn, timestamp; lưu liên kết sang front/rear | Người QA độc lập xác nhận ranh giới ego/vật ngoài; bất đồng ghi ticket và ảnh trước khi đưa vào gold |

- Refresh khi thay camera, ống kính/vị trí lắp, calibration, rule hoặc khi kiểm thử phát hiện lỗi mới theo ánh sáng/thời tiết. Ghi phiên bản và chỉ sửa tập gold sau review độc lập; giữ lịch sử bản cũ.
- Ca seam: một Bike đi từ front sang left cùng timestamp có thể có hai box per-camera hợp lệ. Policy trước tiên giữ hai nhãn ở không gian ảnh gốc; nếu đầu ra đòi một object BEV/track, chỉ ghép sau khi kiểm đồng bộ thời gian, intrinsics/extrinsics, vùng chồng và identity. Lưu cả hai frame, hai box, timestamp, calibration version và quyết định phân xử. Không xoá một box chỉ vì cùng vật xuất hiện ở hai camera.
- Peer agreement hay quality report trên ADASIND một camera chỉ đo sự nhất quán trong tập đó. Chúng không kiểm được seam, đồng bộ, BEV hoặc phân bố cảnh của rear/left/right; cần review riêng từng camera và kiểm chéo trước khi gọi 200 frame là gold set.
