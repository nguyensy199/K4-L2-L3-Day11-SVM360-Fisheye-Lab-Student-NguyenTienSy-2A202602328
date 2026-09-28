# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling đã nằm trong file tương ứng nên không hỏi lại ở đây.

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy tắc riêng? Vì sao? 
Đây KHÔNG phải là lỗi `DUPLICATE` mà là hiện tượng vật lý bình thường của hệ thống camera SVM quanh xe và cần một quy tắc (cross-camera policy) riêng. Hai camera đặt ở hai vị trí khác nhau có góc nhìn và ma trận quang học khác nhau, do đó một vật thể nằm trong vùng nhìn chồng lấn (overlap seam) sẽ tạo ra hai hình chiếu quang học 2D độc lập và hoàn toàn hợp lệ trên hai mặt phẳng cảm biến. Ở tầng gán nhãn 2D raw fisheye, mỗi camera phải phản ánh trung thực phần hình ảnh thu được; chỉ ở tầng perception fusion (không gian 3D/BEV) mới tiến hành hợp nhất hai box thành một đối tượng thực.

2. Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera. 
- Trên cùng 1 camera: Giữ cùng Track ID khi vật thể di chuyển liên tục và duy trì nhận diện danh tính (identity); tạo thêm keyframe khi vật đổi hướng đột ngột, tăng/giảm tốc độ hoặc biến dạng hình học đáng kể; gán trạng thái Outside khi vật thể tạm thời rời khỏi khung hình hoặc bị chướng ngại vật lớn che khuất hoàn toàn rồi sau đó quay lại.
- Bằng chứng bắt buộc để nối track qua hai camera: (1) Timestamp được đồng bộ cấp phần cứng (hardware genlock sync) giữa hai luồng video; (2) Ma trận hiệu chuẩn ngoại suy (extrinsics calibration) chính xác giữa hai camera; (3) Tính liên tục của quỹ đạo chuyển động 3D trong không gian tọa độ thế giới (BEV trajectory continuity).

3. Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`), bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm? 
Tại frame `adasind_069450.jpg` đối tượng L1 (ô tô con ở hậu cảnh xa có chiều cao đo được 25px): Ban đầu annotator nhận biết rõ ràng đó là một phương tiện giao thông nên đã vẽ box. Tuy nhiên, theo luật R01 của khóa học, các vật thể dưới ngưỡng H=40px không bắt buộc gán nhãn nhằm tránh sinh ra các box không ổn định. Trong pha QA review và rework, tôi đã tôn trọng tiêu chuẩn guideline và tiến hành xóa box này trong bản rework annotations-v2.xml, đồng thời ghi log vào `decision_log.csv`. Nếu làm lại slice này, tôi sẽ bật chế độ đo chiều cao pixel ngay từ bước đầu để sàng lọc chuẩn xác các vật thể tiệm cận ngưỡng 40px trước khi vẽ.
