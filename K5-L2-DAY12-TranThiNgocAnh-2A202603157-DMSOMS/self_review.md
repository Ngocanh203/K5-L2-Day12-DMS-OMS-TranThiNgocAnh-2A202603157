# Tự đánh giá Lab ngày 12 · DMS/OMS

**Trần Thị Ngọc Ánh · 2A202603157 · G07**

## 1. Phạm vi và kết quả kiểm tra

Bản nộp `export_final.zip` là bản CVAT đã chỉnh sửa sau review. Phạm vi gồm 16 ảnh OMS (S01–S08, mỗi cảnh có RGB và IR-sim) và 6 ảnh DMS (D01–D06, NIR thật). Cả 22 ảnh đều có `frame_meta`. ZIP export chứa `annotations.xml`.

| Bước kiểm | Phạm vi | Kết quả | Bằng chứng |
|---|---|---|---|
| Checkpoint A, kiểm hồi cứu | S01–S02, 4 ảnh | 4/4 có `frame_meta`, 0 lỗi, 0 cảnh báo | `check_cpA.txt` |
| Checkpoint B, kiểm hồi cứu | D01–D02, 2 ảnh | 2/2 có `frame_meta`, 0 lỗi, 1 cảnh báo ở D02 | `check_cpB.txt` |
| Kiểm toàn bộ sau chỉnh sửa | 22 ảnh | 22/22 có `frame_meta`, 0 lỗi, 3 cảnh báo | `check_final.txt` |

Ba lần kiểm dùng manifest OMS và cấu hình đã áp dụng cập nhật của Lab Coach cho `child_seat.occupied=yes` khi thấy rõ có người trong ghế.

## 2. Tự rà soát bốn khung hình

| Ảnh | Đối tượng | Nhận định từ bản gán | Xử lý hoặc việc cần xác nhận |
|---|---|---|---|
| `S01_rgb.png` | `child_seat`, `rear_middle` và `rear_right` | `rear_middle` ghi `occupied=yes` ở cả hai ảnh. `rear_right` ghi `unknown` ở RGB và `no` ở IR-sim. | Giữ giá trị trong export. Khi rà ảnh, xác định ghế theo hướng xe và xem riêng lòng từng ghế theo §4.4 và §4.8. |
| `S08_ir.png` | `child_seat`, `rear_right` | Cả RGB và IR-sim ghi `occupied=yes`. | Giữ giá trị trong export. Đối chiếu dấu hiệu thấy người ở từng ảnh theo §4.8. |
| `D02.png` | Mắt trái và bốn mốc `face13` | `eye_left=unknown`; cả bốn mốc chưa bật cờ. | Cảnh báo còn trong bản nộp. Kiểm lại khe mắt và khả năng định vị từng mốc theo §4.5–4.6. |
| `D04.png` | Hai mắt và các mốc `face13` | Mắt phải ghi `unknown`, cả bốn mốc mắt phải là `outside`. Mắt trái ghi `unknown`, cả bốn mốc mắt trái chưa bật cờ. | Đã sửa mắt phải sau đối chiếu. Cảnh báo mắt trái cần xác nhận riêng trên ảnh. |

## 3. Cảnh báo lặp lại và cách rà

- D02, mắt trái (§4.5–4.6). Bản gán ghi `unknown` và cả bốn mốc mắt trái có `occluded=0`, `outside=0`. Cần xem riêng độ rõ của khe mắt và từng mốc trên CVAT. Mắt phải có bốn mốc `occluded=1` và được ghi `unknown`.
- D04, mắt trái (§4.5–4.6). Bản gán ghi `unknown` và cả bốn mốc mắt trái có `occluded=0`, `outside=0`. Cần kiểm mắt trái riêng. Mắt phải có bốn mốc `outside=1` và đã được cập nhật thành `unknown` sau đối chiếu.
- D06, mắt phải (§4.5–4.6). Bản gán ghi `unknown` và cả bốn mốc mắt phải có `occluded=0`, `outside=0`. Cần kiểm trực tiếp khe mắt phải và khả năng định vị từng mốc trên CVAT.

Điểm lặp lại là thuộc tính mắt `unknown` đi cùng bốn mốc đều chưa bật cờ. Khi rà từng mắt, trước hết kiểm xem có thấy khe mắt mở hay thấy hai mí khép. Sau đó kiểm lần lượt hai khóe mắt và hai mốc mí. Với điểm bị che, dùng `occluded` nếu vẫn định vị được hoặc `outside` nếu không thể định vị. Với ảnh DMS xoay 90°, xác định trái và phải theo người, với mắt trái ở tọa độ y lớn hơn. Các ghi chú trên đây dựa trên XML. Trạng thái nhìn thấy trên ảnh và lý do cụ thể của ba cảnh báo còn cần xác nhận trên CVAT.

## 4. Bài học từ review chéo

Ở `D04.png`, bản của Lương Quốc Việt ghi `eye_right=unknown`. Trước chỉnh sửa, bản của Ánh ghi `open` trong khi cả bốn mốc mắt phải đều là `outside`. Đề xuất dùng `unknown` theo §4.5–4.6 đã được áp dụng. Lần kiểm cuối hết cảnh báo ở mắt phải D04. Khi gán lần sau, rà cùng lúc trạng thái mắt, khả năng định vị mốc và bằng chứng trực quan của từng mắt.

Nhật ký review ghi 83 dòng ở thời điểm đối chiếu, gồm 13 đề xuất kỹ thuật và 70 dòng cần rà thêm. Chạy lại phép so sánh trên bản nộp và cùng bản của Việt cho 82 điểm khác. Các đề xuất đang chờ xác nhận chung giữa hai học viên.

## 5. Quan sát RGB, IR-sim và NIR thật

`ir_log.csv` ghi năm quan sát từ export. Hai quan sát OMS dùng cặp RGB/IR-sim ở S01 và S07, gồm sự khác biệt về `occupied` và trường hợp giá trị `object.type` được giữ. Ba quan sát DMS dùng NIR thật ở D01, D02 và D04, tập trung vào trạng thái mắt và cờ vị trí mốc. Nguyên nhân trực quan như phản xạ hoặc vùng tối cần được xác nhận trên ảnh CVAT.

## 6. Tệp đi kèm

Bằng chứng gán nhãn và kiểm tra nằm trong `export_final.zip` và ba báo cáo `check_*.txt`. `disagreement_log.csv` và `TEAM.md` ghi đối chiếu với bạn review. `ir_log.csv` và `class_list_v0.md` lưu quan sát IR và danh sách lớp. `exit_ticket.md` và `prompts.md` lưu bài cuối buổi và khai báo dùng AI.
