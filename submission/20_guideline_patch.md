# Guideline patch

- **Rule mới đề xuất:** R12 — Quy chuẩn đo chiều cao và phân loại phương tiện lai tại vùng méo rìa: Với các vật thể có chiều cao tiệm cận ngưỡng H=40px (38–42px) nằm tại vùng méo rìa (edge zone), annotator phải đo trực tiếp khoảng cách pixel thẳng đứng từ điểm cao nhất đến điểm thấp nhất nhìn thấy trên ảnh fisheye gốc trước khi gán nhãn; các xe tải nhỏ chở hàng có thùng hở phân loại nhất quán thành `Truck`, xe chở người dạng van gán `Car`.
- **Áp dụng cho:** Class `Car`, `Truck`, các đối tượng tại `edge` zone và kiểm soát ngưỡng R01.
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** Luật v1.0.0 chưa có chỉ dẫn đo đạc cụ thể cho các vật thể bị kéo giãn/nén do méo quang học fisheye ở rìa ảnh, dẫn tới bất đồng giữa annotator và reference ở các ca tiệm cận 40px.
- **`rules_version` mới:** v1.1.0
- **Hiệu lực từ:** Áp dụng từ vòng r3_diag và quy trình gán nhãn sản xuất SVM 4 camera.
