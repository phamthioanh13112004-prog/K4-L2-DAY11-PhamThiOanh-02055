# Sensor context

- Theo ba ảnh `B3-edge`, camera nhìn về phía trước từ một xe hai bánh đang chạy; tay/người lái và phần xe xuất hiện ở góc trái dưới. Đây là suy luận từ ảnh, không phải thông số rig hay vị trí lắp đã được ADASIND công bố.
- Phần `ego_body` thấy rõ chủ yếu ở góc trái dưới: tay áo, tay lái/gương và thân xe gần camera. Ở `adasind_199770.jpg`, phương tiện tối bên phải tách khỏi phần ego nhìn thấy nên không nên mặc định là `ego_body`.
- Vòng kính fisheye gần chiếm hết chiều rộng ảnh 1080 px; cung trên quanh y≈160–200 và cung dưới quanh y≈1770–1840 tùy frame. Vùng đen ngoài cung là `lens_border`; cần soát polygon import theo từng ảnh gốc, không suy vòng tròn hoàn hảo từ kích thước khung.
