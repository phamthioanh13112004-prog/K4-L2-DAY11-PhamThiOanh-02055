# Quan sát vạch ô đỗ

- Người làm: Oanh.
- Ảnh: `parking-lot-core.jpg`, kích thước ảnh gốc 960 × 720 px.
- Bản nhãn đang quan sát: [annotations.xml](annotations.xml), gồm 11 polyline `parking_line` và 8 polygon `free_space`.
- Bằng chứng: [ảnh chụp nhãn hiện tại](../screenshots/oanh-parking-current.png), đối chiếu với [ảnh gốc](../../assets/parking/parking-lot-core.jpg) và [quy tắc parking-line](../../docs/11-parking-lines-vi.md).

- **Hai vạch `parking_line` đã vẽ (mô tả vị trí trong ảnh):**
  1. Vạch trắng ở tiền cảnh, gần giữa cạnh dưới ảnh, chạy chéo từ khoảng `(409, 654)` đến `(528, 718)` trên ảnh gốc. Đây là đoạn sơn phân chia các ô đỗ trong dãy gần camera. Polyline bám theo phần sơn nhìn thấy, kết thúc gần mép dưới ảnh.
  2. Vạch trắng ở tiền cảnh phía bên phải, chạy chéo từ khoảng `(699, 623)` đến `(959, 685)`. Đây là một ranh chia ô khác trong cùng dãy đỗ; đường kết thúc sát cạnh phải, không suy diễn phần nằm ngoài ảnh.
  Các tọa độ trên lấy từ XML, không phải tọa độ của ảnh chụp màn hình đã được co giãn. Những vạch ngắn hơn ở dãy phía xa hơn cần được soát riêng theo phần sơn thực sự nhìn thấy.

- **Một vạch/dấu sơn hoặc biên không vẽ, và vì sao:**
  Biên phía xa giữa mặt bãi với hàng rào và hàng cây không được gán `parking_line`: đây là ranh giới của bãi, không phải đoạn sơn phân chia một ô đỗ riêng lẻ. Không gán nhãn biên xe đỏ, cột đèn hoặc đường bao cây như vạch đỗ. Các dấu sơn mờ ở xa chưa được đưa vào bản nhãn này; cần xem lại ảnh gốc nếu muốn bổ sung, chỉ vẽ đoạn xác định được vai trò chia ô và phần sơn nhìn thấy.

- **Polygon `free_space` dừng ở đâu; có phần bị che nào không:**
  Bản hiện tại có ba polygon trong dãy ô đỗ tiền cảnh và năm polygon trong dãy ô đỗ ở giữa ảnh. Các polygon dừng gần các vạch phân chia ô; một số polygon tiền cảnh chạm cạnh dưới hoặc cạnh phải vì vùng đó bị khung hình cắt. Trong những vùng đang khoanh không thấy xe hoặc vật cản che mặt bãi; xe đỏ nằm ở xa, ngoài các polygon này. Phần ngoài khung hình không được suy diễn là trống.
  **Điểm cần sửa:** các polygon hiện tại chủ yếu bao từng ô đỗ trống. Theo quy tắc của bài, `free_space` phải là phần mặt đường trống nhìn thấy của lối xe chạy. Cần sửa hoặc thay các polygon này bằng vùng lối xe chạy giữa hai dãy ô đỗ, giữ ranh giới theo phần nhìn thấy và dừng trước xe/vật cản. Ghi chú này mô tả bản hiện tại, chưa xác nhận nhãn `free_space` đã đúng yêu cầu.

- **Ca chưa chắc cần hỏi người soát:**
  1. Polyline dài từ khoảng `(2, 542)` đến `(960, 508)` nối ngang qua các đầu vạch của dãy giữa ảnh. Trên ảnh gốc không thấy một dải sơn liên tục đủ rõ dọc toàn bộ đường này. Cần người soát xác nhận đây có thật là vạch tạo ranh ô hay chỉ là đường nối suy diễn/biên mặt bãi; nếu không có sơn nhìn thấy hoặc không chia ô thì xóa, nếu chỉ có vài đoạn sơn thì tách và giữ đúng các đoạn đó.
  2. Nhờ người soát kiểm lại vùng lối xe chạy cần chọn cho `free_space`, đặc biệt ranh giới với hai dãy ô đỗ. Không dùng việc ô đỗ đang trống để mặc định nó là vùng lối xe chạy theo quy ước bài.

Sau khi sửa trong CVAT: Ctrl+S, export lại `CVAT for images 1.1`, chạy lại lệnh nhập parking và cập nhật ghi chú cùng ảnh minh chứng theo bản mới. Các quan sát ở trên chỉ phản ánh ảnh tĩnh, không xác nhận vùng xe tự hành có thể đi an toàn.
