# Lưới xám

Một sản phẩm web nhỏ: thế giới fantasy phản ứng lại đời thật của người dùng.

Repo: `luoi-xam` · Live: https://cungtu.github.io/luoi-xam/

---

## Sản phẩm này là gì

Người dùng mở ra thấy một lưới ô vuông xám, đều tăm tắp. Mỗi ngày họ viết **một điều họ đã làm theo ý mình** — dù nhỏ đến đâu. Một ô vỡ ra khỏi lưới, mất hình vuông, có màu, mọc mầm.

Sau ba mươi ngày, không có hai người nào có tấm bản đồ giống nhau.

Câu trên là toàn bộ sản phẩm. Mọi quyết định thiết kế đều phải phục vụ nó.

## Thế giới

**Thứ thiếu vắng: tự do.** Thế giới này đã đánh mất nó.

**Luật:** Khi người khác thấy bạn không suy nghĩ và hành động theo tiêu chí chung, một sợi xích xuất hiện trên người bạn — khiến bạn di chuyển khó hơn và suy nghĩ nặng nhọc hơn. Càng nhiều người cùng đánh giá bạn sai theo cùng một tiêu chí, sợi xích của tiêu chí đó càng lớn.

**Hình ảnh trung tâm:** Một quả cầu trôi trong bóng tối. Bên trong là thế giới nhỏ đang ngủ. Ở giữa, một sinh vật vừa ngẩng lên, và chỗ nó đứng màu sắc bắt đầu loang ra. **Không có ai bên ngoài nhìn vào. Quả cầu tự sáng lên từ bên trong.**

Câu cuối là ràng buộc đạo đức của cả sản phẩm: không có thực thể nào đứng trên người dùng để chấm điểm, hướng dẫn, hay chấp thuận họ.

## Luật cấm (quan trọng nhất trong file này)

Sản phẩm phê phán việc đánh giá con người bằng tiêu chí chung. Nên nó **không được phép** tự trở thành một hệ thống đánh giá.

Tuyệt đối không thêm, kể cả khi nghe có vẻ hữu ích, kể cả khi mục tiêu là tăng tỉ lệ quay lại:

- Điểm số, cấp độ, huy hiệu, thành tựu
- Chuỗi ngày liên tiếp (streak) — kể cả chỉ hiển thị số ngày
- Bảng xếp hạng, so sánh giữa người dùng
- Nút thích, tim, bình chọn
- Thông báo đẩy, email nhắc nhở, chấm đỏ, badge số
- Bất kỳ con số nào hiển thị cho người dùng: số ô đã mở, số ngày, phần trăm hoàn thành
- Danh sách việc đang chờ làm

Lý do chung: bất cứ thứ gì đếm được đều biến thành thứ phải dọn sạch, và lúc đó sản phẩm thành một app to-do — đúng cái lưới xám mà nó đang phê phán.

Nếu một tính năng nghe hợp lý nhưng vi phạm mục trên, **hãy nêu ra và hỏi lại**, đừng tự thêm.

## Trạng thái hiện tại

Một file `index.html` duy nhất, không framework, không build step, không backend. Kèm `manifest.json`, `sw.js` và bộ icon. Deploy bằng GitHub Pages.

- Lưới cố định 18 × 12 = 216 ô, tỉ lệ 3:2, co giãn theo màn hình
- Viết một câu rồi gửi (Enter hoặc nút mũi tên) → một ô vỡ ra
- **Đất mọc liền nhau**: ô đầu tiên ở giữa, mỗi ô sau chọn ngẫu nhiên trong các ô kề với vùng đã tự do. Điều này biến những mẩu rời rạc thành một hòn đảo. Đừng đổi thành random toàn cục.
- Ô tự do: bo góc ngẫu nhiên thành hình hữu cơ, xoay nhẹ, màu từ `PALETTE`, mầm SVG từ `SPROUTS`, thở rất chậm
- Chạm vào ô tự do → hiện lại câu đã viết, ngày viết, và nút "sửa" để chỉnh lại câu (không xoá được từng dòng — chỉ "xoá tất cả" ở góc màn hình)
- Ba ví dụ tầm thường hiện dưới ô nhập, hạ ngưỡng cho người viết lần đầu. Chạm vào điền thẳng vào ô nhập. Ẩn hẳn khi đã có từ một ghi chép trở lên
- **Rễ**: ghi chép tạo hơn `ROOT_DAYS` (mặc định 7) ngày trước và chưa từng "nhìn lại" thì nhìn lại được. Mỗi lần mở app, chọn ngẫu nhiên đúng một ghi chép đủ điều kiện, đánh dấu bằng chấm sáng rất nhỏ. Ba trạng thái hiển thị: mầm non (mới, <7 ngày) → có rễ (đã nhìn lại, đứng vững) → nghiêng dần (quá hạn chưa nhìn lại — không đổ, không mất). Sau câu đầu tiên, hiện một dòng một-lần-duy-nhất báo trước "N ngày nữa, điều này sẽ quay lại hỏi bạn". `?rootdays=0` ép mọi ghi chép đủ điều kiện ngay, dùng khi test
- Lưu bằng `localStorage`, key `luoixam:v1`
- Song ngữ Việt/Anh, tự nhận theo `navigator.language`. Ép bằng `?lang=vi` hoặc `?lang=en`
- `?demo` chạy kịch bản quay video: ô đầu chậm và rõ kèm câu thật, nhanh dần, rồi time-lapse. Không ghi vào localStorage, không gửi sự kiện đo lường
- Cài lên màn hình chính được (manifest + service worker). Gợi ý cài hiện sau câu thứ hai, chỉ một lần, bỏ qua được vĩnh viễn

### Điểm nhấn thị giác

Khoảnh khắc ô vỡ là thứ duy nhất được phép hoành tráng: ô phóng to giật, xoay lệch, vuông biến thành hình hữu cơ, vòng sáng lan ra, mầm tự vẽ, và **các ô xung quanh trong bán kính 3 giật lùi theo sóng lan**. Mọi thứ khác cố tình giữ im.

Nếu cần cắt bớt hiệu ứng ở đâu đó, đừng cắt ở đây. Đây cũng là công cụ phân phối: nó là thứ quay video được và khiến người lạ dừng tay.

### Đo lường

GoatCounter (`luoixam`), không cookie. Sự kiện:

- `quay-lai/ngay-N` — lần mở đầu tiên trong ngày, N là lần mở thứ mấy của thiết bị đó
- `cua-vao/cham-o-nhap` — lần đầu chạm vào ô nhập
- `viet/lan-N` — mốc câu thứ 1, 3, 7, 20
- `cai-dat/hien-goi-y`, `cai-dat/dong-y`, `cai-dat/tu-choi`
- `re/hien-loi-moi` — lời mời "nhìn lại" xuất hiện; `re/da-nhin-lai` — đã viết xong "nhìn lại". So hai số này để biết bao nhiêu người thấy lời mời rồi thật sự trả lời

**Nội dung người dùng viết không bao giờ rời khỏi máy họ.** Ràng buộc cứng. Điều này đã được hứa công khai với người dùng trên Reddit — không được vi phạm dù vì lý do gì.

Chỉ số duy nhất đáng nhìn: bao nhiêu người còn quay lại từ ngày thứ ba trở đi.

## Những gì đã học được từ người dùng thật

Đợt đăng đầu tiên trên r/SideProject, khoảng 14 thiết bị:

- 14 mở trang → 9 chạm ô nhập → 4 viết câu đầu
- Ít nhất **một người lạ quay lại đến ngày thứ ba** mà không có bất kỳ lời nhắc nào
- **Cơ chế tự giải thích được.** Người nói tiếng Anh mở ra, không ai hướng dẫn, vẫn hiểu phải làm gì và viết đúng format

**Lỗi đã sửa nhờ người dùng chỉ ra:** ô nhập không nằm trong `<form>` nên iOS hiện nút "xong" không kích hoạt được gửi (gần như mọi người dùng iPhone không viết được câu nào); không có cách sửa lại một câu đã viết sai, còn nút xoá tất cả thì để màu quá tối gần như tàng hình. Giải bằng nút "sửa" trên từng ô, không phải nút xoá riêng dòng — xoá từng dòng đi ngược triết lý "bản đồ không mất" của sản phẩm.

Bài học chung: **không bao giờ để hành động chính phụ thuộc vào một phím bàn phím**, và luôn thử trên điện thoại thật sau mỗi thay đổi giao diện.

**Yêu cầu duy nhất từ người dùng thật:** đưa lên màn hình chính. Nguyên văn lý do: chức năng giống hệt web, nhưng "tôi sẽ nhớ và ghi lại nhiều hơn nếu nó là app trên màn hình". Bookmark không cho cảm giác đó. Đã làm.

**Chỗ rò rỉ lớn nhất hiện nay:** hơn một nửa số người chạm vào ô nhập rồi không viết gì. Giả thuyết chưa kiểm chứng: họ không biết viết gì, vì câu hỏi "hôm nay bạn làm gì theo ý mình?" buộc người ta tự đánh giá xem việc mình làm có "đủ theo ý mình" không. Đó là rào cản tâm lý, không phải giao diện — và mỉa mai thay, nó chính là cái xích trong thế giới này. Hướng đang cân nhắc: đổi cách hỏi, hoặc cho thấy vài ví dụ thật ở màn hình đầu để hạ ngưỡng.

**Số liệu đang bẩn** vì thiết bị của người làm lẫn vào — thấy rõ qua việc `viet/lan-3` nhiều hơn `viet/lan-1`, điều bất khả về logic. Cần cơ chế `?notrack` để loại thiết bị của mình ra.

## Chưa làm — đừng tự làm

### Xích hiển thị

Xích hiện chỉ tồn tại trong lore, người dùng chưa bao giờ nhìn thấy. Ý tưởng: nhân vật của người dùng bắt đầu ở tư thế khom lưng, mỗi ô tự do làm họ đứng thẳng thêm một chút — người ta thấy sự thay đổi ở chính mình, không chỉ ở bản đồ. Cải thiện ấn tượng ban đầu, nhưng ấn tượng ban đầu đang ổn. Xếp sau rễ.

### Thăm nhau (xa)

Đi lạc vào bản đồ ngẫu nhiên của người lạ, không tên. Đọc được dòng "chuyện đó dẫn tới đâu" nếu chủ nhân chọn để lộ. Để lại một câu ngắn dưới gốc cây, ẩn danh.

Chi tiết bắt buộc: **cây có rễ và cây không rễ trông không khác nhau nhiều từ xa** — cây cao vống nhìn còn ấn tượng hơn. Người ghé thăm phải tự nhìn xuống gốc mà đoán. Không nhãn nào nói giúp họ ai đáng tin.

### Hỏi người quay lại

Sau khi ai đó mở đến lần thứ ba, hiện một dòng rất nhỏ, không ép: "bạn quay lại lần thứ ba rồi. Nếu muốn kể vì sao, mình đọc." Kèm ô nhập gửi thẳng cho người làm. Giải quyết chuyện hiện nay biết có người quay lại nhưng không hỏi được vì sao. Chỉ làm khi có đủ người đến ngày thứ ba.

### Backend

Chưa cần. Chỉ cần khi người dùng phải đăng nhập từ nhiều máy. Khi tới: Spring Boot + Postgres, một controller, một service, một repository. Bảng `entries` có `created_at`, `reflection` (null), `reflected_at` (null). Đừng dựng kiến trúc nhiều tầng cho sản phẩm chưa có người dùng.

## Quy ước code

- Giữ nguyên một file `index.html`. Chỉ tách khi nó thật sự cản trở việc sửa.
- Không thêm framework, không build step, không dependency.
- Không thư viện animation — CSS thuần đã đủ tốt.
- Tôn trọng `prefers-reduced-motion` (đã có).
- Giữ focus bàn phím nhìn thấy được, ô tự do phải chạm được bằng phím.
- Escape nội dung người dùng trước khi đưa vào `innerHTML` (đã có hàm `esc`).
- Đổi `CACHE` trong `sw.js` khi cần ép người dùng tải lại toàn bộ.

## Quy ước chữ nghĩa

Giao diện song ngữ Việt/Anh, mọi chuỗi đặt trong `STR`. Không hardcode chữ vào DOM.

Viết từ phía người dùng, không phải phía hệ thống. Gọi tên thứ người ta thấy, không gọi tên cách nó được xây. Câu ngắn, động từ thường.

Giọng của sản phẩm: trầm tĩnh, không cổ vũ, không reo hò. **Không bao giờ khen người dùng.** Không "Tuyệt vời!", không "Bạn đang làm rất tốt!". Bản đồ tự nói lên điều cần nói.

Màn hình trống là lời mời, không phải lời than.

## Bối cảnh người làm

Một người, lập trình viên Java 5 năm, làm ngoài giờ khoảng 10–15 tiếng một tuần. Mục tiêu là tác động xã hội, không phải doanh thu.

Hệ quả: ngân sách rất hẹp, rủi ro lớn nhất là làm quá nhiều thứ cùng lúc. Khi phân vân, chọn phương án nhỏ hơn. Khi một tính năng nghe hay, hỏi trước xem nó có phục vụ câu hỏi hiện tại không — **câu hỏi hiện tại là: làm sao để người đã chạm vào ô nhập thật sự viết được câu đầu tiên, và có lý do quay lại ngày mai.**
