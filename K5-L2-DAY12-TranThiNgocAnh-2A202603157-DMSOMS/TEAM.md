# Review chéo Lab ngày 12

Nộp cá nhân, bộ ảnh **G07**.

| Học viên | MSSV | Bạn review chéo | MSSV bạn review | Phạm vi |
|---|---|---|---|---|
| Trần Thị Ngọc Ánh | 2A202603157 | Lương Quốc Việt | 2A202603127 | 22 ảnh chung |

## Cách ghi nhật ký

`disagreement_log.csv` ghi lần đối chiếu trước khi áp dụng chỉnh sửa. Cột `mine` là giá trị của Ánh lúc review, cột `peer` là giá trị của Việt. Nhật ký ghi 83 dòng, gồm 12 đề xuất giữ bản Ánh, 1 đề xuất theo bản Việt và 70 dòng đánh dấu `ambiguous` để đối chiếu thêm. Các nhận định là đề xuất kỹ thuật dựa trên XML. Hai học viên chưa xác nhận chung các kết luận.

## Chỉnh sửa đã áp dụng

Ở `D04.png`, mắt phải được cập nhật thành `unknown` vì bốn mốc tương ứng đều được đánh dấu `outside`. Khi đối chiếu lại với cùng bản của Việt, script báo 82 điểm khác trên 22 ảnh chung. Dòng D04 vẫn có trong nhật ký để ghi lại căn cứ sửa.

## Ca cần đối chiếu trên CVAT

- **DMS:** D02 mắt trái, D04 mắt trái và D06 mắt phải có trạng thái `unknown` trong khi bốn mốc tương ứng chưa bật cờ. Kiểm trạng thái mắt và khả năng định vị từng mốc theo §4.5–4.6.
- **OMS:** Kiểm riêng dấu hiệu có người trong ghế ở S01 và S08 trên từng ảnh RGB và IR-sim theo §4.8. Tại ghế `rear_right` của S01, hồ sơ ghi `unknown` ở RGB và `no` ở IR-sim.
