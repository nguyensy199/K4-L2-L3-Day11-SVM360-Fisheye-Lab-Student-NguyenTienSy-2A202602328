# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| `adasind_062370.jpg` (Khu vực trung tâm & mép rìa) | 3 ca MISSING, 5 ca SPURIOUS model | Đây là cảnh có mật độ phương tiện cao, xuất hiện nhiều xe ThreeWheeler và Bike ở vùng mép quang học cong mạnh, dễ gây nhầm lẫn class và sót box. | XML annotations, ảnh overlay so sánh model YOLO26m, thông số tọa độ box trong `findings.csv`. |
| `adasind_069450.jpg` & `adasind_117120.jpg` (Vùng tiệm cận ngưỡng H=40px) | 3 ca SPURIOUS (L1, L2, L5) dưới ngưỡng 40px | Các vật thể nhỏ ở cự ly xa dễ bị vẽ thừa hoặc bỏ sót tùy cảm tính annotator, cần rà soát để chuẩn hóa tiêu chuẩn đo đạc R01. | Số đo chiều cao pixel trên CVAT, bảng so sánh đối chứng trước/sau trong `submission/rework/delta.md`. |

Giới hạn của kết luận từ ba frame ADASIND: Slice chỉ đại diện cho một camera fisheye góc nhìn đơn lẻ trong một điều kiện thời tiết ban ngày; không thể suy diễn phân bố lỗi này cho toàn bộ hệ thống SVM 4 camera bao gồm camera lùi và camera hai bên hông xe.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh như nhiều ca độc lập), và vì sao kế hoạch đó chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi:
- Khi lấy mẫu từ tập 50.000 frame, cần áp dụng quy tắc lấy mẫu cách quãng tối thiểu 5–10 giây hoặc chọn theo sự kiện (event-based trigger) để đảm bảo tính độc lập giữa các frame, tránh việc lấy nhiều frame liên tiếp trong cùng một pha dừng đèn đỏ hay cùng một góc cua.
- Tập 200 frame được thiết kế để phân tầng (stratified sampling) phát hiện các ca biên (hard cases, seam boundary, chói lóa đèn xe), đóng vai trò như một bộ kiểm tra tập trung (spot check) để rà soát lỗi nghiêm trọng chứ không thể thay thế cho tập validation thống kê lớn để đo lường độ chính xác tổng thể.
