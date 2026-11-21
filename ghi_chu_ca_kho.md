# Ghi chú ca khó & ghế trống — Day12 · G03 · Nguyễn Duy Khánh (2A202603055)

Dùng để chép vào `self_review.md` / cuối `check_final.txt` khi nộp. Gọi ảnh bằng tên, không chụp màn hình (RULES §2).

## Ghế trống (không vẽ box — GUIDE §4.2, §4.8)

| Ảnh | Ghế trống (theo xe) | Ghi chú |
|---|---|---|
| S01_rgb | rear_middle | Không thấy vật (ảnh RGB tối/mờ); S01_ir thấy túi ở rear_middle → có box object trên IR |
| S02_rgb | rear_middle | 1 ghế trống, không gán |
| S02_ir  | rear_middle | 1 ghế trống, không gán |
| S06_rgb | rear_right, rear_middle | 2 ghế trống |
| S06_ir  | rear_right, rear_middle | 2 ghế trống |
| S07_rgb | rear_middle, rear_left | 2 ghế trống |
| S07_ir  | rear_middle, rear_left | 2 ghế trống |
| S08_rgb | rear_middle | 1 ghế trống |
| S08_ir  | rear_middle | 1 ghế trống |

(S03, S04, S05: cả 3 ghế đều có box — không có ghế trống. Ghi chú cũ "S03 trống" đã bỏ vì nhãn cuối có object bag ở rear_middle.)

## Thay đổi so với Guideline v1.0 (theo chỉ đạo coach)

- 21/11/2026: coach cho phép thêm `child_seat.occupied = yes`. `scripts/cabin_check.py` của repo chưa cập nhật nên báo ERROR cho giá trị này; không sửa script/XML (RULES §4). Bản đối chiếu: `tools/cabin_check_coach.py`.

## Ca khó / chờ coach trả lời

| Ảnh | Đối tượng | Vấn đề | Tạm gán | Trạng thái |
|---|---|---|---|---|
| D02 | face13 | Mặt quay đi, không đặt được điểm nào | Chỉ box `face` (eye/glasses theo thấy được), xoá `face13` (GUIDE §4.6: không đặt điểm "cho đủ") | đã xử lý |
| (điền) | infant_seat có em bé | `infant_seat` không có thuộc tính `occupied` | 1 box `infant_seat`, không vẽ `person` | chờ coach |
