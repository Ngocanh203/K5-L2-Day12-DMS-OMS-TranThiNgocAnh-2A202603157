# Danh sách lớp v0 của Trần Thị Ngọc Ánh

Mã bộ ảnh G07. Các dòng đề xuất mô tả tín hiệu đầu vào cho model. Chức năng cần diễn giải theo ngữ cảnh và theo chuỗi khung hình nếu phải đo thời gian.

## DMS

| Lớp hoặc thuộc tính | Giá trị | Để làm gì | Nhìn thấy được trên IR? |
|---|---|---|---|
| `person` ở ghế lái | `seat=driver` | Định vị tài xế để chọn đúng đối tượng theo dõi | Có nếu thân người còn trong khung |
| `face` | Vị trí mặt thấy được | Cắt vùng mặt cho bước nhận dạng mắt và hướng nhìn | Có khi mặt đủ rõ |
| `eye_left`, `eye_right` | `open`, `closed`, `unknown` | Đo độ mở và thời gian nhắm mắt trên chuỗi khung hình | Có điều kiện. Phản xạ và vật che có thể làm mất khe mắt |
| `face13` | 13 điểm và cờ từng điểm | Ước lượng tư thế đầu và định vị vùng mắt, mũi, miệng | Có điều kiện. Bỏ skeleton dưới ngưỡng mặt 60 px |
| `gaze_zone` | `road`, `mirror_l`, `mirror_r`, `mirror_c`, `cluster`, `center`, `lap`, `other` | Đo thời gian tài xế nhìn ra khỏi đường theo chuỗi khung hình | Có điều kiện. Cần thấy hướng mắt hoặc đầu |
| `glasses` | `none`, `clear`, `sun`, `unknown` | Đánh giá độ tin cậy của tín hiệu mắt khi tài xế đeo kính | Có điều kiện. Tròng kính râm có thể trông trong dưới NIR |
| `hand.on_wheel` | `yes`, `no`, `unknown` | Theo dõi tiếp xúc với vô lăng khi chức năng lái cần tín hiệu này | Có khi thấy điểm tiếp xúc giữa tay và vô lăng |
| `phone.state` | `held`, `mounted`, `lap` | Phân biệt điện thoại cầm tay, đặt trên giá và đặt trên đùi | Có khi thấy cạnh, góc hoặc màn hình |

## OMS

| Lớp hoặc thuộc tính | Giá trị | Để làm gì | Nhìn thấy được trên IR? |
|---|---|---|---|
| `person` ở hàng ghế sau | Box người lớn | Phát hiện hành khách trong cabin | Có nếu phần cơ thể còn thấy được |
| `seat` | `rear_left`, `rear_middle`, `rear_right` ở bộ G07 | Gắn cảnh báo đúng vị trí ghế theo hệ quy chiếu của xe | Có khi xác định được vị trí ghế |
| `person.seatbelt` | `worn_correct`, `worn_incorrect`, `not_worn`, `unknown` | Nhắc thắt dây theo ghế. Với SVIRO, chỉ lấy bằng chứng cho `not_worn` và `unknown` | Có điều kiện. Dải dây có thể chìm vào áo tối |
| `child_seat` | `occupied=yes`, `no`, `unknown` | Nhận biết thiết bị giữ trẻ và tình trạng sử dụng theo ghế | Thường thấy hình ghế. Lòng ghế có thể khuất |
| `infant_seat` | `facing=rear` hoặc `front` | Nhận biết nôi và hướng lắp theo ghế | Có điều kiện. Cần thấy đủ cấu trúc của nôi |
| `object.type` | `bag`, `box`, `cup`, `other` | Phân biệt đồ để trên ghế với hành khách | Có điều kiện. Dựa vào hình dạng, vị trí và ngữ cảnh |
| `frame_meta.camera_blocked` | `yes`, `no` | Phát hiện khi hình ảnh cabin bị che để đánh dấu độ tin cậy | Có thể nhận ra vùng nhìn bị che khi hình ảnh đủ rõ |

## Hai câu hỏi leo thang

1. **`S08_rgb.png`** — Khi người ngồi trong ghế trẻ em bị che một phần, cần thấy những dấu hiệu tối thiểu nào để chốt `occupied=yes`? Tạm dùng `yes` khi thấy rõ có người trong ghế và `unknown` khi phần nhìn thấy chưa đủ xác định.
2. **`D04.png`** — Nếu thấy một phần khe mắt đủ để nhận ra mắt mở nhưng cả bốn mốc viền mắt vẫn khó định vị, có thể giữ `eye_right=open` cùng các điểm `outside` không? Tạm áp tiêu chí khe mắt theo §4.5 và đánh cờ từng điểm theo §4.6. Nếu chỉ thấy vùng quanh mắt, dùng `unknown`.
