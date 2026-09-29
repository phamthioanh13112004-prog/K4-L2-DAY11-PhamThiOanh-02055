# Escalation ticket

## Ticket 1

- **Frame:** `adasind_199770.jpg`, Bike L3 `(540,841)–(658,1006)` so với teaching reference R9 `(539,880)–(610,997)`.
- **Ảnh chụp:** [ảnh review frame 199770](screenshots/B3-edge_199770_car_review.png) cho thấy vùng Bike và người đi bộ ở giữa ảnh; ảnh chưa phóng đủ gần để kết luận ranh giới L3. Đối chiếu thêm `assets/images/adasind_199770.jpg`, `submission/r1_craft/compare.html` và `submission/r2_qa/qa_review.md`.
- **Expected impact:** Nếu L3 ôm cả người đi bộ L1, hình học box Bike sai; nếu R9 bỏ bớt phần xe nhìn thấy, teaching reference cần sửa. Không thể kết luận chỉ từ IoU.
- **Owner:** `qa` để phóng to ảnh và đối chiếu R02/R03; chuyển `annotator` nếu L sai hoặc Lab Coach nếu R sai.
- **Recommendation:** Xem vùng `x=530–710, y=820–1030` ở frame `adasind_199770.jpg`, chỉ ra phần xe và vị trí người đứng; chụp đúng frame/vùng này trong CVAT, rồi quyết định giữ/sửa box và cập nhật finding `r3_diag/L3+M3` cùng decision `QA-04`. Trạng thái hiện tại: escalated, chưa chốt nhãn.
