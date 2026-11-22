# Khai báo dùng AI — Nguyễn Duy Khánh (2A202603055) · G03

Không đưa ảnh cabin hay ảnh tài xế (kể cả ảnh chụp màn hình) cho công cụ AI nào. Ảnh chỉ nằm trên máy và CVAT local; tôi tự chọn file ảnh khi tạo task. Claude chỉ đọc tài liệu repo, toạ độ/thuộc tính trong file export (`annotations.xml`) và gọi API CVAT local bằng chữ.

| # | Công cụ | Tôi hỏi gì (tóm tắt) | Tôi dùng kết quả thế nào | Có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | Claude | Đọc README/RULES/GUIDE/RUBRIC, tóm tắt điều cấm và các bước | Dùng làm checklist làm bài | Có — đối chiếu lại file gốc trong repo |
| 2 | Claude | Giải thích guideline: ghế theo xe, `facing`, ghế trống, em bé trong nôi, `occupied`, thuộc tính `face`/`hand` | Hiểu luật; tự quyết khi gán | Có — đối chiếu GUIDE §4, hỏi coach về `occupied = yes` |
| 3 | Claude | Tạo project `Day12` + nhãn từ `labels_cabin_v1.json` qua API CVAT local; export file CVAT 1.1 (không kèm ảnh) qua API; thêm giá trị `occupied = yes` sau khi coach cho phép | Thay thao tác bấm tay; ảnh do tôi tự chọn tải lên | Có — kiểm số ảnh (22) và nhãn trên CVAT |
| 4 | Claude | Viết công cụ phụ `tools/extra_qc.py` (soát modality, trái/phải theo trục y trên D##, ghế trống…) và `tools/cabin_check_coach.py` (cabin_check của repo + chấp nhận `occupied = yes`) | Soát lỗi trước khi nộp; không thay `scripts/cabin_check.py` | Có — chạy `scripts/cabin_check.py` chính thức cho mọi file check nộp |
| 5 | Claude | Chạy `cabin_check check/diff`, liệt kê lỗi theo toạ độ | Tôi tự sửa nhãn trên CVAT | Có — chạy lại check sau mỗi lần sửa |
| 6 | Claude | Điền sẵn verdict cho các dòng `disagreement_log` phân xử được bằng luật; soạn báo cáo review chéo gửi Loan | Dòng cần nhìn ảnh do tôi và Loan quyết | Có — tôi mở ảnh trên CVAT để quyết từng dòng |
| 7 | Claude | Soạn nháp `TEAM.md`, `ir_log.csv` (từ nhãn và mô tả của tôi), `class_list_v0.md`, `self_review.md` | Tôi đọc, sửa câu chữ và nội dung theo ý mình | Có — đối chiếu với nhãn trong `export_final_v2.zip` |

`exit_ticket.md`: tự làm, không dùng AI.
