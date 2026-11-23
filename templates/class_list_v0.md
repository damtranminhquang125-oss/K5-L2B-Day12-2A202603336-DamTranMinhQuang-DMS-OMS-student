# Danh sách lớp v0 — Đàm Trần Minh Quang · G11

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**
Xóa 2 dòng ví dụ trước khi nộp.

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` / `seat`, `seatbelt` | `seat`: driver, front_passenger, rear_left, rear_middle, rear_right; `seatbelt`: worn_correct, worn_incorrect, not_worn, unknown | Xác định vị trí tài xế và tình trạng thắt dây để cảnh báo khi cần | Thường nhận ra được người; dây có thể bị tối hoặc che khuất nên có thể là `unknown` |
| 2 | `face` / `eye_left`, `eye_right` | open, closed, unknown | Theo dõi trạng thái mắt; chuỗi nhiều khung hình có thể hỗ trợ phát hiện dấu hiệu buồn ngủ | Có thể thấy, nhưng phản xạ kính, kính râm hoặc góc mặt có thể làm mắt không rõ |
| 3 | `face` / `glasses` | unknown, none, clear, sun | Xử lý đúng trường hợp có kính để tránh nhầm kính với mắt hoặc đánh giá sai trạng thái mắt | Có thể thấy gọng/tròng, nhưng NIR có thể làm kính râm trông trong; không chắc thì `unknown` |
| 4 | `face` / `gaze_zone` | road, mirror_l, mirror_r, mirror_c, cluster, center, lap, other | Phát hiện hướng chú ý rời khỏi đường và nhận biết vùng tài xế đang nhìn | Thường ước lượng được từ mặt và mắt; hướng nhìn cụ thể có thể không rõ |
| 5 | `face13` | 13 điểm mặt; từng điểm có cờ `occluded` hoặc `outside` | Định vị mắt, mũi, miệng để hỗ trợ phân tích mặt và hướng nhìn | Có nếu mặt đủ lớn và đủ chi tiết; điểm bị che phải đánh dấu, không đoán |
| 6 | `hand` / `whose`, `side`, `on_wheel` | driver/passenger; left/right; yes/no/unknown | Xác định tay của ai, tay nào đang chạm vô lăng để hỗ trợ theo dõi thao tác tài xế | Thường thấy hình dáng bàn tay; điểm tiếp xúc vô lăng có thể khó phân biệt |
| 7 | `phone` / `state` | held, mounted, lap | Phát hiện điện thoại và phân biệt đang cầm, đặt trên giá hay trên đùi để cảnh báo mất tập trung | Có thể thấy nếu còn lộ cạnh, góc hoặc màn hình; vật bị che nhiều có thể không xác nhận được |

## OMS

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` / `seat` | driver, front_passenger, rear_left, rear_middle, rear_right | Đếm người và xác định ghế có người để quản lý chỗ ngồi | Thường thấy hình người và vị trí; gọi ghế theo xe, không theo phía ảnh |
| 2 | `person` / `seatbelt` | worn_correct, worn_incorrect, not_worn, unknown | Kiểm tra tình trạng dây an toàn của người ngồi | Có thể thấy dải dây, nhưng tối hoặc bị che thì phải ghi `unknown` |
| 3 | `face` | Hộp mặt theo vùng nhìn thấy | Định vị mặt người ngồi, bổ trợ xác nhận vị trí có người | Thường nhận ra hình dạng mặt; ảnh tối hoặc mặt bị che có thể hạn chế |
| 4 | `child_seat` / `occupied` | `seat`: các vị trí ghế; `occupied`: no, unknown | Nhận biết ghế trẻ em và tình trạng nhìn thấy bên trong để hỗ trợ nhắc kiểm tra ghế | Thường nhận ra hình dạng ghế; nếu không nhìn rõ bên trong thì `unknown` |
| 5 | `infant_seat` / `facing` | `seat`: các vị trí ghế; `facing`: rear, front | Nhận biết nôi xách em bé và hướng quay để hỗ trợ kiểm tra cách bố trí | Thường nhận ra hình dạng và hướng đặt; vùng bị che khuất có thể gây mơ hồ |
| 6 | `object` / `type` | `seat`: các vị trí ghế; `type`: bag, box, cup, other | Xác định loại và vị trí đồ vật trong cabin để hỗ trợ quản lý hành lý/vật dụng | Thường thấy hình dáng và vị trí; IR-sim không cho phép suy loại đồ vật bằng màu |

## 2 câu hỏi leo thang

1. Câu hỏi: Khi mắt không nhìn rõ và không xác định được hướng nhìn, có nên gán `eye_left`/`eye_right = unknown` đồng thời `gaze_zone = other` không? `other` có áp dụng cả khi không đủ bằng chứng về hướng nhìn, hay chỉ khi hướng nhìn rõ nhưng nằm ngoài các vùng đã liệt kê?  
Khung ví dụ: `D03.png`.
Bạn tạm gán thế nào và vì sao: Giữ `eye_left` và `eye_right` là `unknown` vì không phân biệt được trạng thái mắt; tạm chọn `gaze_zone = other` vì guideline cho phép dùng `other` khi không chắc hướng nhìn.

2. Câu hỏi: Khi hình dáng đồ vật trong IR-sim không đủ để phân biệt `bag`, `box` hay `cup`, guideline cho phép `other` khi không chắc, nhưng chưa nói nên ưu tiên `other` hay `unknown` nếu đồ vật có mặt nhưng loại không rõ.  
Khung ví dụ: `S01_ir.png`. 
Bạn tạm gán thế nào và vì sao: Nếu chắc chắn có đồ vật nhưng không nhận ra loại, gán `object` với `type = other`; nếu không chắc đó có phải đồ vật hay không, không đoán và hỏi coach.
