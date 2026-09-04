# Lưới xám

Một sản phẩm web nhỏ: thế giới fantasy phản ứng lại đời thật của người dùng.

Repo: `luoi-xam` · Live: https://cungtu.github.io/luoi-xam/

---

## Sản phẩm này là gì

Người dùng mở ra thấy một lưới ô vuông xám, đều tăm tắp. Mỗi ngày họ viết **một điều họ đã làm theo ý mình** — dù nhỏ đến đâu. Một ô vỡ ra khỏi lưới, mất hình vuông, có màu, mọc mầm.

Sau ba mươi ngày, không có hai người nào có tấm bản đồ giống nhau.

Câu trên là toàn bộ sản phẩm. Mọi quyết định thiết kế đều phải phục vụ nó.

## Thế giới

Ba điều nền tảng, không thay đổi:

**Thứ thiếu vắng: tự do.** Thế giới này đã đánh mất nó.

**Luật:** Khi người khác thấy bạn không suy nghĩ và hành động theo tiêu chí chung, một sợi xích xuất hiện trên người bạn — khiến bạn di chuyển khó hơn và suy nghĩ nặng nhọc hơn. Càng nhiều người cùng đánh giá bạn sai theo cùng một tiêu chí, sợi xích của tiêu chí đó càng lớn.

**Hình ảnh trung tâm:** Một quả cầu trôi trong bóng tối. Bên trong là thế giới nhỏ đang ngủ — cây xám, nước đứng yên, những sinh vật cúi đầu. Ở giữa, một sinh vật vừa ngẩng lên, và chỗ nó đứng màu sắc bắt đầu loang ra. **Không có ai bên ngoài nhìn vào. Quả cầu tự sáng lên từ bên trong.**

Điều cuối cùng đó là ràng buộc đạo đức của cả sản phẩm: không có thực thể nào đứng trên người dùng để chấm điểm, hướng dẫn, hay chấp thuận họ.

## Luật cấm (quan trọng nhất trong file này)

Sản phẩm phê phán việc đánh giá con người bằng tiêu chí chung. Nên nó **không được phép** tự trở thành một hệ thống đánh giá.

Tuyệt đối không thêm, kể cả khi nghe có vẻ hữu ích:

- Điểm số, cấp độ, huy hiệu, thành tựu
- Chuỗi ngày liên tiếp (streak) — kể cả hiển thị số ngày
- Bảng xếp hạng, so sánh giữa người dùng
- Nút thích, tim, bình chọn
- Thông báo đẩy, email nhắc nhở, chấm đỏ, badge số
- Bất kỳ con số nào hiển thị cho người dùng: số ô đã mở, số ngày, phần trăm hoàn thành
- Danh sách việc đang chờ làm

Lý do chung: bất cứ thứ gì đếm được đều biến thành thứ phải dọn sạch, và lúc đó sản phẩm thành một app to-do — đúng cái lưới xám mà nó đang phê phán.

Nếu một tính năng nghe hợp lý nhưng vi phạm mục trên, **hãy nêu ra và hỏi lại**, đừng tự thêm.

## Trạng thái hiện tại — v1

Một file `index.html` duy nhất. Không framework, không build step, không backend. Deploy bằng GitHub Pages.

- Lưới cố định 18 × 12 = 216 ô, tỉ lệ 3:2, co giãn theo màn hình
- Gõ câu vào ô nhập, nhấn Enter → một ô vỡ ra
- **Đất mọc liền nhau**: ô đầu tiên ở giữa, mỗi ô sau chọn ngẫu nhiên trong các ô kề với vùng đã tự do. Điều này biến những mẩu rời rạc thành một hòn đảo. Đừng đổi thành random toàn cục.
- Ô tự do: bo góc ngẫu nhiên thành hình hữu cơ, xoay nhẹ, màu lấy từ `PALETTE`, có mầm SVG từ `SPROUTS`, thở rất chậm
- Chạm vào ô tự do → hiện lại câu đã viết và ngày viết
- Lưu bằng `localStorage`, key `luoixam:v1`

### Điểm nhấn thị giác

Khoảnh khắc ô vỡ là thứ duy nhất được phép hoành tráng: ô phóng to giật, xoay lệch, vuông biến thành hình hữu cơ, một vòng sáng lan ra, mầm tự vẽ, và **các ô xung quanh trong bán kính 3 giật lùi theo sóng lan**. Mọi thứ khác cố tình giữ im.

Nếu cần cắt bớt hiệu ứng ở đâu đó, đừng cắt ở đây.

### Đo lường

GoatCounter, không cookie. Sự kiện gửi đi:

- `quay-lai/ngay-N` — lần mở đầu tiên trong ngày, N là lần mở thứ mấy của người đó
- `viet/lan-N` — mốc câu thứ 1, 3, 7, 20

**Nội dung người dùng viết không bao giờ rời khỏi máy họ.** Ràng buộc cứng, không được vi phạm dù vì lý do gì.

Chỉ số duy nhất đáng nhìn: bao nhiêu người còn quay lại từ ngày thứ ba trở đi.

## Chưa làm — đừng tự làm

### Rễ (tháng thứ hai, chỉ khi v1 giữ được người)

Cơ chế đã thiết kế xong nhưng **chưa được code**:

Người dùng có hai hành động ở hai tốc độ khác nhau.

*Hành động* — viết một điều tự do hôm nay. Làm được mỗi ngày. Phá một sợi xích, một ô vỡ ra, mọc mầm.

*Nhìn lại* — mở lại một ghi chép cũ và viết chuyện đó dẫn tới đâu. Chỉ làm được với ghi chép đã tạo **hơn 7 ngày trước** và chưa từng nhìn lại. Mỗi ghi chép chỉ nhìn lại một lần. Việc này làm **rễ** mọc dưới ô đất đó.

Ô có rễ thì cây đứng vững. Ô không rễ vẫn mọc — mọc nhanh và cao hơn — rồi nghiêng dần và ngừng lớn. **Không đổ, không mất, không lây sang ô khác.** Cơ chế trừng phạt tạo cảm giác tội lỗi, và tội lỗi khiến người ta bỏ app. Ngày nào người dùng quay lại viết, rễ mọc, cây đứng thẳng lên.

Ý nghĩa: tự do cần hiểu biết, mà hiểu biết không mua được bằng nỗ lực — chỉ có thể chờ và để ý.

Không được làm danh sách các ghi chép đang chờ nhìn lại. Mỗi lần vào app, lấy **ngẫu nhiên một** ghi chép đủ điều kiện và chỉ hiện đúng cái đó. Không đếm được thì không có gì để dọn.

Con số 7 ngày là phỏng đoán, phải để thành biến cấu hình.

### Thăm nhau (tháng thứ sáu, hoặc không bao giờ)

Đi lạc vào bản đồ ngẫu nhiên của người lạ, không tên. Đọc được dòng "chuyện đó dẫn tới đâu" nếu chủ nhân chọn để lộ. Để lại một câu ngắn dưới gốc cây, ẩn danh.

Chi tiết bắt buộc: **cây có rễ và cây không rễ trông không khác nhau nhiều từ xa** — cây cao vống nhìn còn ấn tượng hơn. Người ghé thăm phải tự nhìn xuống gốc mà đoán. Không có nhãn nào nói giúp họ ai đáng tin.

### Backend

Chưa cần. Chỉ cần khi người dùng phải đăng nhập từ nhiều máy. Chưa tới lúc đó.

Khi tới: Spring Boot + Postgres, một controller, một service, một repository. Bảng `entries` có `created_at`, `reflection` (null), `reflected_at` (null). Đừng dựng kiến trúc nhiều tầng cho một sản phẩm chưa có người dùng.

## Quy ước code

- Giữ nguyên một file `index.html`. Chỉ tách file khi nó thật sự cản trở việc sửa.
- Không thêm framework, không thêm build step, không thêm dependency.
- Không dùng thư viện animation — CSS thuần là đủ và đã đủ tốt.
- Tôn trọng `prefers-reduced-motion` (đã có).
- Giữ focus bàn phím nhìn thấy được, ô tự do phải chạm được bằng phím.

## Quy ước chữ nghĩa

Toàn bộ giao diện bằng tiếng Việt.

Viết từ phía người dùng, không phải phía hệ thống. Gọi tên thứ người ta thấy, không gọi tên cách nó được xây. Câu ngắn, động từ thường, viết hoa như câu bình thường.

Giọng của sản phẩm: trầm tĩnh, không cổ vũ, không reo hò. **Không bao giờ khen người dùng.** Không "Tuyệt vời!", không "Bạn đang làm rất tốt!". Bản đồ tự nói lên điều cần nói.

Màn hình trống là lời mời, không phải lời than.

## Bối cảnh người làm

Một người, lập trình viên Java, làm ngoài giờ khoảng 10–15 tiếng một tuần. Mục tiêu là tác động xã hội, không phải doanh thu.

Hệ quả: ngân sách rất hẹp, và rủi ro lớn nhất là làm quá nhiều thứ cùng lúc. Khi phân vân, chọn phương án nhỏ hơn. Khi một tính năng nghe hay, hỏi trước xem nó có phục vụ câu hỏi hiện tại không — **câu hỏi hiện tại là: có ai quay lại vào ngày thứ ba không.**
