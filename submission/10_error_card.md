# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B2 | MISSING | 8 |
| center | B2 | SPURIOUS | 12 |
| center | C0 | MISSING | 1 |
| center | C0 | SPURIOUS | 1 |
| edge | B2 | ATTRIBUTE | 1 |
| edge | B2 | MISSING | 1 |
| edge | B2 | SPURIOUS | 2 |
| mid | B2 | MISSING | 4 |
| mid | B2 | SPURIOUS | 3 |
| mid | C0 | MISSING | 2 |

## Top defects
- SPURIOUS: 18 (ví dụ frame adasind_019560.jpg)
- MISSING: 16 (ví dụ frame adasind_019560.jpg)
- ATTRIBUTE: 1 (ví dụ frame adasind_062370.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: Lỗi SPURIOUS và MISSING tập trung cao nhất ở zone center (8 MISSING, 12 SPURIOUS). Nguyên nhân MISSING chủ yếu do annotator bỏ sót các đối tượng nhỏ hoặc bị che khuất một phần trong bối cảnh đường phố phức tạp (E1_annotator_error). Trong khi đó, phần lớn SPURIOUS do model YOLO26m bị lệch miền dữ liệu fisheye (E4_model_domain), nhận diện nhầm bóng râm/biển hiệu thành xe/người, cộng thêm việc annotator ban đầu vẽ một số box nhỏ dưới ngưỡng chiều cao H=40px (R01).
- Cách sửa và ai nhận việc (`owner`): 
  + Annotator: Tuân thủ nghiêm ngặt công cụ đo chiều cao R01 (H >= 40px) và kiểm tra kỹ các phương tiện bị che khuất ở trung tâm ảnh.
  + AI Team: Cần tinh chỉnh model trên dữ liệu camera fisheye thực tế, áp dụng mask loại trừ vùng ego_body và lens_border để triệt tiêu các box hallucination.
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule): Finding `adasind_069450.jpg:L1` và `L2` (R01) thể hiện rõ box dưới ngưỡng 40px đã được sửa trong rework; ảnh minh chứng chi tiết lưu tại `submission/screenshots/error_evidence_1.png` và `submission/screenshots/error_evidence_2.png`.
