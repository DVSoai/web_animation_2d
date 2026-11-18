# Xưởng ghép nhân vật

Trang web ghép nhân vật 2D tách mảnh **đầu – thân – chân** theo kiểu Ninja School Online. Chạy hoàn toàn trên trình duyệt: ảnh không gửi lên máy chủ, dự án tự lưu trong trình duyệt.

## Dùng thế nào

1. **Thêm ảnh**
   - *Cắt tờ sprite…*: tải một tờ sprite nền xanh lá (hoặc nền đồng màu). Trang tự xoá nền, tách từng mảnh, đặt tên theo thứ tự tư thế (hàng 1 = đầu, hàng 2 = thân, các hàng dưới = chân). Ô *đầu cao (px)* để đưa cả tờ về đúng cỡ.
   - Hoặc thả các file PNG trong suốt. Tên file có `head`/`body`/`legs` sẽ được nhận loại tự động; tên có `run-0`, `walk-1`… sẽ được gán đúng khung.
2. **Ghép**: 14 khung mặc định (đứng 2, đi 4, chạy 4, nhảy 4). Bấm mảnh trong thư viện để gán vào lớp đang chọn, kéo mảnh trên khung để căn, phím mũi tên dời 1 px (Shift: 10 px), `[` `]` đổi khung, Space phát.
3. **Tự căn theo điểm neo**: chân đặt chạm đất ở điểm gốc; thân đặt sao cho tâm gấu áo trùng tâm cạp quần và đè xuống *n* px; đầu đặt sao cho tâm cằm trùng tâm cổ áo. Chấm màu trên khung: xanh dương = cạp quần, vàng = gấu áo, xanh lá = cổ áo, đỏ = cằm. Dòng trạng thái dưới khung báo độ lệch.
4. **Tải xuống**: `rig.json` (toạ độ), PNG khung đang xem, hoặc ZIP trọn bộ (`parts/`, `frames/`, `rig.json`, `sheet.png`). *Lưu dự án* tạo một file `.json` chứa cả ảnh để mở lại ở máy khác.

## Định dạng rig.json

- `canvas`, `root`: khung và điểm gốc (giữa hai bàn chân trên mặt đất).
- `order`: thứ tự vẽ, phần tử đầu ở sau cùng. Mặc định `legs → head → body` (thân đè chân cổ và cạp quần).
- Mỗi lớp: `x`, `y` là góc trên-trái của mảnh tính từ điểm gốc, sau khi nhân `scale`; `width`, `height` là kích thước đã nhân tỉ lệ.
- `anchors`: toạ độ các điểm neo đo được, để kiểm tra.
