# Guideline patch

- **Rule mới đề xuất:** Thêm ví dụ cho R07: `ego_body` chỉ ôm phần cố định của xe/camera đang chụp. Nếu một phương tiện ở mép ảnh có viền tách khỏi tay lái, thân xe hoặc gương ego, không dùng `ego_body` để che nó; gán class theo phần nhìn thấy và dùng `truncated` khi bị cắt biên. Với vùng chưa phân định được, ghi ca cần QA thay vì mở rộng polygon.
- **Áp dụng cho:** `ignore_region.reason=ego_body`, sáu class động và vật ở mép ảnh fisheye; ví dụ frame `adasind_199770.jpg`, polygon `P4` bên phải.
- **Vì sao cần bổ sung:** R07 nêu phải vẽ ego body nhưng chưa có ví dụ phân biệt một xe khác áp sát mép ảnh với thân xe ego. Ở `P4`, polygon phủ lên phương tiện mà ảnh gốc cho thấy tách khỏi ego rider bên trái.
- **`rules_version` mới:** đề xuất `v1.1.0`; `docs/02-rules-vi.md` vẫn ở `v1.0.0` cho lượt đã khóa.
- **Hiệu lực từ:** lượt gán nhãn mới sau khi Lab Coach/nhóm phê duyệt, không áp dụng hồi tố cho XML đã khóa.
