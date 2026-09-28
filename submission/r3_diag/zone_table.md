# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 13 | 2 | 1 | 6 | 7 | MISSING (2) |
| mid | 5 | 1 | 0 | 2 | 3 | MISSING (1) |
| edge | 2 | 0 | 0 | 1 | 2 | — |

## Nhận xét

- Zone nào người (L) và model (M) gãy nhiều nhất, dẫn số ở bảng trên: Vùng center là nơi phát sinh nhiều lỗi nhất về số lượng tuyệt đối cho cả người (L missing 2, L spurious 1 trên 13 đối tượng tham chiếu) và model (M missing 6, M spurious 7). Vùng mid người có 1 missing, trong khi vùng edge người đạt kết quả chuẩn xác (0 missing, 0 spurious). Model (M) gãy nặng ở cả 3 zone (tổng cộng 9 missing và 12 thừa trên toàn bộ slice).
- Giả thuyết vì sao (méo fisheye, box lỏng, thiếu `ego_body`, ...) và giới hạn của slice ba frame: Vùng center có mật độ đối tượng cao, nhiều vật thể xa và bị che khuất cục bộ dẫn tới annotator bỏ sót các box nhỏ; trong khi model YOLO thuần túy chưa thích ứng với miền ảnh fisheye nên liên tục hallucinate box giả ở nền và bỏ sót vật bị che. Vùng edge dù méo quang học lớn nhưng annotator đã bám sát viền vật thể thực tế nên không bị lỗi hình học. Giới hạn: Slice chỉ gồm 3 frame trong cùng một điều kiện ban ngày nên chưa phản ánh đủ các ca khó như chói lóa, ban đêm hay thời tiết xấu trong hệ thống SVM 4 camera.
