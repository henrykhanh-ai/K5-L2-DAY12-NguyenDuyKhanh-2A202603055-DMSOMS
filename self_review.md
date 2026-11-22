# Tự đánh giá — Nguyễn Duy Khánh · G03

## 1. Tự rà soát 4 cảnh

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_rgb | infant_seat | seat_flip | Để nguyên `seat = driver` (giá trị CVAT điền sẵn) thay vì `rear_left` | Có (bản final) |
| S02_rgb | frame_meta | guess | Copy tag từ ảnh IR sang ảnh RGB, quên đổi `modality = rgb` | Có (bản final) |
| D02 | face / face13 | extra | Mặt quay đi, không thấy mắt lẫn mũi mà vẫn vẽ box `face` (§4.5) | Có (bản v2, sau review chéo) |
| D03 | face13 | flag | Điểm mắt phải bật cùng lúc `occluded` và `outside`; có lúc bật cờ nhầm sang mắt trái dù `eye_left = open` | Có (bản v2) |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: không đổi giá trị mặc định CVAT tự điền — `seat = driver` trên cả 10 box ở lần kiểm đầu, và cờ điểm `face13` bật thừa.

Vì sao mình mắc: vẽ box xong chuyển sang box khác ngay, không mở DETAILS kiểm lại từng thuộc tính; copy shape/tag giữa ảnh RGB và IR mà không soát lại.

Lần sau tránh bằng cách: vẽ xong mỗi box mở DETAILS chọn lại `seat` ngay; sau khi dán từ ảnh khác thì soát `modality` và từng cờ điểm; chạy `cabin_check` + công cụ soát sau mỗi 2 cảnh thay vì đợi cuối buổi.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai: D02 `face` — Loan không vẽ box mặt vì tài xế quay đi; mình vẽ dù chính mình ghi chú là không đặt được điểm nào. Mình học được: "không thấy cả mắt lẫn mũi thì không vẽ box" áp dụng cho cả box `face`, không chỉ cho `face13`.

## 4. Thay đổi so với Guideline v1.0

- `child_seat.occupied = yes` được coach cho phép ngày 21/11/2026; `scripts/cabin_check.py` chưa cập nhật nên báo 6 ERROR — đã giải thích cuối `check_final_v2.txt`, không sửa script/XML.
