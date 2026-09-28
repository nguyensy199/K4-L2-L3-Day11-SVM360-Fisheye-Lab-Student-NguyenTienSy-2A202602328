# Quan sát vạch ô đỗ

- Hai vạch `parking_line` đã vẽ (mô tả vị trí trong ảnh): Các vạch sơn trắng chéo phân chia các ô đỗ xe riêng biệt ở tiền cảnh (dãy ô đỗ phía dưới ảnh) và các vạch sơn vàng phân chia từng ô đỗ ở dãy đỗ xe giữa bãi.
- Một vạch/dấu sơn hoặc biên **không** vẽ, và vì sao: Các vạch sơn vàng chạy ngang phân chia hai hàng xe đấu đuôi nhau ở dãy giữa (đây là ranh giới luồng/dãy xe, không phải vạch chia ô cạnh nhau); và các vạch sơn mờ ở khoảng sân bê tông sáng phía xa gần chiếc xe đỏ vì quá xa và không rõ ô đỗ.
- Polygon `free_space` dừng ở đâu; có phần bị che nào không: Polygon `free_space` bao phủ lối xe chạy trống trải dài theo chiều ngang giữa dãy ô đỗ tiền cảnh và dãy ô đỗ vạch vàng; biên polygon dừng lại ngay sát mép đầu các vạch ô đỗ, không bị vật cản nào che khuất trên làn đường này.
- Ca chưa chắc cần hỏi người soát (nếu không có, ghi “không có”): không có
