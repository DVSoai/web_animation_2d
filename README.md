# Xưởng ghép nhân vật

Trang web ghép nhân vật 2D tách mảnh **đầu – thân – chân** theo kiểu Ninja School Online. Chạy hoàn toàn trên trình duyệt: ảnh không gửi lên máy chủ, dự án tự lưu trong trình duyệt.

## Dùng thế nào

1. **Thêm ảnh**
   - *Cắt tờ sprite…*: tải một tờ sprite nền xanh lá (hoặc nền đồng màu). Trang tự xoá nền, tách từng mảnh, đặt tên theo thứ tự tư thế (hàng 1 = đầu, hàng 2 = thân, các hàng dưới = chân). Ô *đầu cao (px)* để đưa cả tờ về đúng cỡ.
   - Hoặc thả các file PNG trong suốt. Tên file có `head`/`body`/`legs` sẽ được nhận loại tự động; tên có `run-0`, `walk-1`… sẽ được gán đúng khung.
2. **Ghép**: 11 khung mặc định theo NSO (đứng 2, chạy 5, nhảy 4). NSO không có trạng thái đi bộ (Char.java chỉ có đứng, chạy, nhảy, rơi), nên không có nhóm đi; vẫn thêm được bằng + Khung với mã walk-0…. Bấm mảnh trong thư viện để gán vào lớp đang chọn, kéo mảnh trên khung để căn, phím mũi tên dời 1 px (Shift: 10 px), `[` `]` đổi khung, Space phát.
3. **Tự căn theo điểm neo**: chân đặt chạm đất ở điểm gốc; thân đặt sao cho tâm gấu áo trùng tâm cạp quần và đè xuống *n* px; đầu đặt sao cho tâm cằm trùng tâm cổ áo. Chấm màu trên khung: xanh dương = cạp quần, vàng = gấu áo, xanh lá = cổ áo, đỏ = cằm. Dòng trạng thái dưới khung báo độ lệch.
4. **Tải xuống**: `rig.json` (toạ độ), PNG khung đang xem, hoặc ZIP trọn bộ (`parts/`, `frames/`, `rig.json`, `sheet.png`). *Lưu dự án* tạo một file `.json` chứa cả ảnh để mở lại ở máy khác.

## Định dạng rig.json

- `canvas`, `root`: khung và điểm gốc (giữa hai bàn chân trên mặt đất).
- `order`: thứ tự vẽ, phần tử đầu ở sau cùng. Mặc định `legs → head → body` (thân đè chân cổ và cạp quần).
- Mỗi lớp: `x`, `y` là góc trên-trái của mảnh tính từ điểm gốc, sau khi nhân `scale`; `width`, `height` là kích thước đã nhân tỉ lệ.
- `anchors`: toạ độ các điểm neo đo được, để kiểm tra.


## Tổng quan (dashboard)

Mở web sẽ vào trang **Tổng quan**:

- **Dự án**: mọi nhân vật lưu trong trình duyệt, kèm ảnh nhỏ, số khung, số mảnh. Mở, nhân bản, xóa ngay tại thẻ.
- **Số liệu**: số khung, số mảnh theo loại, số khung có cảnh báo lệch, số mảnh chưa dùng.
- **Hoạt ảnh**: mỗi nhóm (idle, walk, run, jump…) tự phát xem trước. Có nút Lật, Dừng, Tải sheet của nhóm.
- **Khung hình**: bảng mọi khung. Đổi mảnh đầu/thân/chân ngay trong bảng, sửa ms. Cột Hông và Cổ hiện độ lệch đo theo điểm neo, kèm nhãn "khớp" hoặc cảnh báo.
- **Thư viện mảnh**: chia theo Đầu / Thân / Chân, ghi rõ mảnh dùng ở bao nhiêu khung.

Trang **Ghép khung** là trình chỉnh từng pixel như trước.

## Cách nối đầu với thân như NSO

Đã đo từ dữ liệu mảnh thật của game cùng kiểu NSO:

- Mảnh đầu **không có cổ**, kết thúc ở cằm. Mặt sau là tóc đen phủ tới cằm.
- Mép trên của mảnh thân là đường viền tối rộng khoảng nửa bề ngang đầu, ngay dưới là vai. Khi đặt đầu lên, cằm che giữa đường này, hai đầu thừa thành bóng dưới quai hàm.
- **Đầu vẽ sau thân**. Cằm chồng xuống thân khoảng **12% chiều cao đầu** (2 px trên đầu 16 px).
- Thân đè chân 2 px, có dải tối làm đường cạp ngay phía trên.

Web mặc định dùng đúng quy tắc này (mục "Cách nối đầu với thân" trên trang Tổng quan).
