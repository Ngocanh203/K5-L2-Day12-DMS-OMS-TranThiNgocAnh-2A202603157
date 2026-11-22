# Khai báo dùng AI — Trần Thị Ngọc Ánh

| # | Công cụ | Nội dung hỏi AI | Cách sử dụng kết quả | Cách kiểm tra lại |
|---|---|---|---|---|
| 1 | Codex | Đọc tài liệu Day 12, tóm tắt yêu cầu gán nhãn DMS và OMS, giải thích cách hiểu các thuộc tính và khi nào dùng `unknown`. | Dùng phần giải thích để tìm đúng mục trong guideline trước khi gán nhãn. Giá trị thuộc tính được chọn dựa trên chi tiết quan sát trực tiếp trong CVAT local. | Đối chiếu với `GUIDE.md` và quy định của từng nhãn. |
| 2 | Codex | Giải thích trình tự thực hiện bài, phạm vi ảnh của Checkpoint A và B, cùng danh sách tệp cần nộp. | Dùng hướng dẫn để sắp xếp các bước gán nhãn, tự kiểm và chuẩn bị hồ sơ nộp. | Đối chiếu phạm vi từng checkpoint với `CHECKPOINTS.md` và danh sách tệp với `SUBMISSION.md`. |
| 3 | Codex | Hướng dẫn thao tác trên CVAT local và cách xuất annotation theo định dạng `CVAT for images 1.1`. | Áp dụng hướng dẫn để tự thao tác trong CVAT và chọn chế độ xuất chỉ gồm annotation. | Kiểm tra tùy chọn `Save images` trước khi xuất và kiểm tra danh sách tệp trong ZIP. |
| 4 | Codex | Hướng dẫn chạy `cabin_check` và cách đọc thông báo lỗi, cảnh báo. | Dùng script của lab để tự kiểm bản export. Dựa vào tên ảnh, nhãn và thuộc tính trong báo cáo để xác định vị trí cần rà lại trên CVAT. | Đối chiếu thông báo của script với guideline và kiểm tra trực tiếp trên CVAT local. |
