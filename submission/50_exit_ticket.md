# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling
đã nằm trong file tương ứng nên không hỏi lại ở đây.

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy
   tắc riêng? Vì sao? Hai box trên hai camera khác nhau có thể đều đúng trên ảnh gốc. Đây là một ca seam cần policy riêng về đầu ra per-camera hay BEV/track chung; chỉ gọi `DUPLICATE` nếu policy đó yêu cầu một object và chứng cứ cho thấy cùng timestamp, cùng vật, cùng không gian đánh giá.
2. Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái
   Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera. Giữ ID khi cùng vật tiếp tục quan sát được trên một camera; thêm keyframe khi vị trí, kích thước, che khuất hoặc thuộc tính đổi đáng kể; đặt Outside khi vật ra khỏi FOV theo quy tắc task. Qua hai camera cần timestamp đồng bộ, calibration/FOV, vùng seam, hình dáng và chuỗi chuyển động liên tục cùng policy output đích; không ghép chỉ vì hai box gần nhau.
3. Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`),
   bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm? Ở `adasind_199770.jpg`, polygon `P4` được gán `ego_body`, nhưng QA ảnh gốc thấy nó che một phương tiện khác; teaching reference còn có R4 ThreeWheeler ở vùng đó. Tôi đã ghi `r2_qa/P4`, `r3_diag/R4` và quyết định đề xuất `QA-02`. Sau yêu cầu sửa, Codex đã bỏ polygon bên phải và thêm box ThreeWheeler trong CVAT; bản rework khóa mã `419F-1DFD`, nhưng B chưa xác nhận lại. Delta vẫn ghi R4 chưa sửa vì polygon ignore của teaching reference bao trọn R4 và box mới, nên cần Lab Coach kiểm tra reference; xem ghi chú trong `rework/delta.md`. Nếu làm lại, tôi sẽ soát ranh giới ego/vật ngoài trên từng frame trước khi khóa và chụp bằng chứng cho ca mép ảnh.
