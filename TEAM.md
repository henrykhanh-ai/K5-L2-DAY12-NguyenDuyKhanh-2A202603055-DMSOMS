# TEAM — Ngày 12

Mã bộ ảnh: **G03** · Hình thức: **cá nhân** (coach ghép review chéo với bạn cùng mã)

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Nguyễn Duy Khánh | 2A202603055 | có (thêm 4 ảnh mở rộng S09–S10) | Loan (cùng mã G03) | 31/44 (còn 13 dòng `ambiguous`) |

Ca hai bạn vẫn không thống nhất và đã hỏi / cần hỏi coach (ghi tên ảnh + đối tượng):

- G03 S05, S06 · `infant_seat.facing`: mình giữ `rear`, Loan ghi `front`.
- G03 D03 · `face.eye_left`: mình thấy khe mắt trái (`open`), Loan ghi `unknown`.
- G03 D06 · cờ 4 điểm mắt phải trong `face13`: mình `outside`, Loan `occluded`.
- G03 S01, S04, S07 · `child_seat.occupied = yes` (coach cho thêm giá trị ngoài Guideline v1.0 ngày 21/11/2026).

## Cá nhân

### NguyenDuyKhanh-2A202603055
- Phần mình làm: gán đủ 22 ảnh + 4 ảnh mở rộng; chạy `cabin_check` ở checkpoint A, B, final, final_v2; review chéo 2 vòng với Loan (96 → 44 → 28 điểm khác), sửa bản v2 theo kết luận review.
- Điều mình học được hôm nay: ghế gọi theo xe chứ không theo ảnh, và trên ảnh xoay 90° phải kiểm trái/phải bằng trục y; khi không thấy thì ghi `unknown` / cờ `outside` thay vì đoán.
