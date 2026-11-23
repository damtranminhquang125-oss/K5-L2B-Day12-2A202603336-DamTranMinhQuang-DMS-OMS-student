# Tự đánh giá — <Họ tên> · <Gxx>

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_ir.png | `frame_meta` | ok | Checkpoint A: part_A có 16/16 ảnh có `frame_meta`, 0 lỗi và 0 cảnh báo; kết quả script không thay thế việc tự nhìn lại ảnh. | Không |
| S02_rgb.png | `frame_meta` | ok | Checkpoint A: part_A có 16/16 ảnh có `frame_meta`, 0 lỗi và 0 cảnh báo; kết quả script không xác nhận độ chính xác hình học của box. | Không |
| D03.png | `eye' | guess | `eye_left/right=open` nhưng cả 4 điểm tương ứng đều bị đánh occluded. | Đổi hai mắt sang `unknown`. |
| D06.png | `frame_meta` | missing | Lần kiểm đầu thiếu tag | Đã bổ sung tag. |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Những ảnh OMS có trẻ em không gán gì nhưng quên thêm frame_meta

Vì sao mình mắc: Không đọc kĩ guideline

Lần sau tránh bằng cách: Ưu tiên việc làm đầu tiên trước khi annotation

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai. Mình học được gì từ dòng đó: Bạn của em đúng khi nói cả mặt bị che chỉ lộ mỗi cái mũi thì vẫn vẽ skeleton mũi còn lại để outside, em sai ở chỗ nghĩ là không cần vẽ. Em học được là cần phải vẽ hết những gì mình nhìn thấy và đọc kĩ guideline.