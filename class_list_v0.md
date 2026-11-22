# Danh sách lớp v0 — Nguyễn Duy Khánh · G03

Viết tiếp từ slide 54. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | eye_left / eye_right | open / closed / unknown | Đo thời gian nhắm mắt (PERCLOS) để cảnh báo buồn ngủ; gán riêng từng mắt vì một mắt có thể bị che | Có, trừ khi kính phản xạ hoặc mặt quay đi (D01, D03, D06: mắt phải unknown) |
| 2 | gaze_zone | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Phát hiện mất tập trung: nhìn ra ngoài vùng `road` quá lâu thì cảnh báo | Một phần — cần thấy mắt và hướng đầu; không chắc thì `other` |
| 3 | phone | held / mounted / lap | Phát hiện dùng điện thoại khi lái (cầm tay, áp tai, nhìn xuống đùi) | Có nếu thấy cạnh/góc máy; vật tối áp tai mà không thấy hình máy thì không gán |
| 4 | hand.on_wheel | yes / no / unknown | Kiểm tra tài xế còn sẵn sàng lấy lại lái (takeover) ở xe có chế độ tự lái | Có — hình dạng tay và vô lăng không cần màu |
| 5 | person.seatbelt | worn_correct / worn_incorrect / not_worn / unknown | Nhắc thắt dây, phát hiện thắt sai (dưới nách, sau lưng) | Một phần — dây tối trên áo tối có thể chìm, khi đó `unknown` |
| 6 | glasses | none / clear / sun / unknown | Biết khi nào kết quả mắt kém tin cậy (kính phản xạ, kính râm) để giảm độ tin của cảnh báo buồn ngủ | Khó — kính râm trên NIR có thể trông trong suốt; không chắc thì `unknown` |
| 7 | face13 (13 điểm mặt) | điểm + cờ occluded / outside | Tính độ mở mắt, hướng đầu, ngáp từ toạ độ điểm thay vì chỉ một nhãn | Có với mặt ≥ 60 px; điểm bị che phải có cờ |

## OMS

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person + seat | driver / front_passenger / rear_left / rear_middle / rear_right | Đếm và định vị người theo ghế để nhắc dây an toàn, chỉnh túi khí theo ghế | Có (hình dạng); ghế gọi theo xe, không theo ảnh |
| 2 | infant_seat + facing | rear / front | Nôi quay về sau ở ghế trước thì phải tắt túi khí; nhắc quên trẻ trong xe | Có (hình dạng vỏ nôi, quai xách) |
| 3 | child_seat + occupied | no / unknown (+ yes theo coach) | Biết ghế trẻ em có trẻ hay trống để cảnh báo quên trẻ khi khoá xe | Có hình dạng ghế; bên trong ghế có thể tối → `unknown` |
| 4 | object + type | bag / box / cup / other | Nhắc quên đồ khi rời xe; phân biệt vật với người để không bật túi khí cho túi xách | Có — trên S01 túi còn rõ hơn ở ảnh IR-sim so với RGB tối |
| 5 | seatbelt (OMS) | not_worn / unknown | Nhắc hành khách ghế sau thắt dây | Hạn chế; SVIRO không có ai thắt dây nên chưa dạy được `worn_correct` |
| 6 | frame_meta.modality / light / camera_blocked | rgb / ir · day / night / unknown · yes / no | Cho model biết loại ảnh và khi nào camera bị che để không đưa ra kết luận sai | Không phải vật thể — thuộc tính cả khung |

## 2 câu hỏi leo thang

1. Câu hỏi: Hệ thống OMS thật cần biết ghế trẻ em **có trẻ hay trống** để nhắc quên trẻ. Guideline v1.0 bỏ `child_seat.occupied = yes`, coach cho thêm trong buổi học. Bản 1.x có chính thức thêm `yes` không, và `cabin_check` có cập nhật theo không?
   Khung ví dụ: G03 S01_rgb / S01_ir, S04_rgb / S04_ir, S07_rgb / S07_ir (ghế trẻ em có trẻ ngồi).
   Tôi tạm gán thế nào và vì sao: `occupied = yes` theo chỉ đạo coach ngày 21/11; giữ lỗi ERROR của `cabin_check` và ghi giải thích cuối `check_final_v2.txt`, không sửa script.

2. Câu hỏi: `infant_seat` không có thuộc tính `occupied` (không ghi được nôi có em bé), và `facing` không có giá trị `unknown`. Khi không đọc chắc được hướng nôi thì chọn gì, và có thêm `occupied` cho `infant_seat` không?
   Khung ví dụ: G03 S05_rgb / S05_ir, S06_rgb / S06_ir — tôi và bạn review chéo gán `facing` ngược nhau (`rear` / `front`).
   Tôi tạm gán thế nào và vì sao: `facing = rear` vì lòng nôi quay ra phía sau xe; ghi ca này vào ghi chú ca khó và chờ coach phân xử.
