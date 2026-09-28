# Escalation ticket

## Ticket 1

- **Frame:** `adasind_062370.jpg` (đối tượng R8 tại hậu cảnh)
- **Ảnh chụp:** `submission/screenshots/escalation_ticket_1.png`
- **Expected impact:** Ngăn ngừa sai số gán nhãn hệ thống và xung đột giữa annotator và gold standard khi đánh giá các phương tiện xa bị che khuất nặng, nâng cao chất lượng huấn luyện mô hình perception SVM.
- **Owner:** `guideline`
- **Recommendation:** Bổ sung hướng dẫn chi tiết quy định: đối với các phương tiện bị che khuất trên 70% hoặc nằm quá xa khiến các đặc trưng nhận diện class không còn rõ ràng, cho phép annotator bao quanh bằng `ignore_region` với `reason: unreadable` thay vì bắt buộc gán nhãn class động gây nhiễu dữ liệu.
