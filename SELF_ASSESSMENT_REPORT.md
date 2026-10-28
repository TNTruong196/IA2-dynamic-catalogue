# SELF-ASSESSMENT REPORT — IA#2 Dynamic HTML

Ngày đánh giá: 28/10/2026. Môn học: CSC13008.

Bài làm gồm Part A và B1–B4. Tôi sử dụng OpenAI Codex trong VS Code;
các yêu cầu gửi assistant và nhật ký được lưu trong [brief.md](./brief.md)
và [AI-LOG.md](./AI-LOG.md).

## 1. Điểm tự đánh giá theo rubric

| # | Tiêu chí | Điểm tối đa | Điểm tự chấm | Bằng chứng và lý do |
|---|---|---:|---:|---|
| 1 | The page behaves as specified (B1–B4) | 45 | 45 | [index.html](./index.html) hoàn thành Part A; [app.js](./app.js) triển khai B1–B4. Lượt review cuối của assistant đạt 23/23 kiểm tra chức năng, self-check 8/8; kết quả đối chiếu Done means được ghi tại mục 2 bên dưới. T-shirt × 2 + Belt × 1 cho 3 món, 500.000 đ. Sau khi được hướng dẫn kiểm tra toàn bộ Done means và B4, tôi xác nhận “tôi test tất cả đều hoạt động đúng”; xem mục xác nhận kiểm thử cuối trong [AI-LOG.md](./AI-LOG.md). |
| 2 | Scope: only index.html and app.js changed | 10 | 10 | Commit gốc `a6e3ff2` khớp cả năm tệp trong ZIP starter được cung cấp. So với commit này, chỉ [index.html](./index.html) và [app.js](./app.js) thay đổi trong các tệp starter; [style.css](./style.css), [check.js](./check.js), [README.md](./README.md) giữ nguyên. Mọi id/class, data-id/data-price được bảo toàn; phần Load more được cung cấp không đổi. Các tài liệu bổ sung là hồ sơ theo yêu cầu nộp bài. |
| 3 | The brief | 15 | 15 | [brief.md](./brief.md), Prompt 1–5, ghi yêu cầu theo thứ tự A, B1, B2, B3, B4. Các prompt quy định giữ id/class, không sửa CSS/bộ kiểm tra, một click listener trên catalogue, dùng textContent, ngăn reload và cách kiểm tra theo Done means. Có lưu trao đổi sau Prompt 3 về Enter làm reload. Các prompt được bổ sung qua commit từng phần và commit tài liệu `3aad26d`. |
| 4 | AI-LOG.md | 20 | 18 | [AI-LOG.md](./AI-LOG.md) có mục riêng A, B1, B2, B3, B4, gồm Tool, Request, Changed, Rejected, các dòng kiểm thử và commit; phân biệt kiểm thử của assistant với xác nhận của tôi. Tuy nhiên mục B1 ghi không cần sửa lại, trong khi phần kiểm thử Node ghi “tất cả pass sau khi sửa” mà chưa chỉ rõ sửa mã hay sửa cách kiểm thử. Chưa có bằng chứng xác định để giải thích câu này. Chọn 18 trong khung 17–20 vì nhật ký chi tiết nhưng còn điểm mơ hồ, không mặc định đủ 20 chỉ vì chức năng chạy đúng. Ghi chú “Nothing went wrong” của rubric cho phép không có lỗi; bản thân việc không có lỗi không phải lý do trừ điểm. |
| 5 | Commit history | 10 | 10 | Lịch sử bắt đầu bằng starter nguyên bản `a6e3ff2`, sau đó có commit riêng cho A, B1, B2, B3, B4; xem mục 3. Thông điệp mô tả thay đổi và diff phù hợp từng phần. Có thêm commit `3aad26d` lưu prompt/nhật ký B4. Thư mục Git đang tồn tại trong bài làm; khi nộp phải giữ cả thư mục ẩn này trong ZIP. |

**Tổng điểm tự chấm: 98/100 = 45 + 10 + 15 + 18 + 10.** Đây là mức tự đánh giá
theo bằng chứng hiện có và xác nhận tự kiểm thử bản cuối, không phải điểm đã được
giảng viên xác nhận. Rubric đưa ra khoảng điểm cho một số tiêu chí; mức 18/20
cho nhật ký là đánh giá thận trọng về độ rõ của bằng chứng, không phải một quy tắc
trừ 2 điểm được ghi trong đề.

### Đối chiếu điều kiện chấm điểm

| Tiêu chí | Điều kiện đã kiểm chứng | Nhận định |
|---|---|---|
| Behaviour | Self-check 8/8; một listener Add; sold-out; Tab/Enter; Belt mới thêm; scarf/SCARF; chuỗi HTML hiển thị nguyên văn; Enter/Search không reload; tổng tiền gồm Belt và card bị ẩn; không lỗi trong lượt thử. Ảnh và phạm vi đã được đối chiếu riêng. | Đáp ứng các mô tả khung 40–45; chưa phát hiện chức năng thiếu nên tự chấm 45. |
| Scope | Hash nội dung của cả năm tệp trong commit đầu khớp ZIP starter; CSS, bộ kiểm tra, README không thay đổi; id/class và phần Load more giữ nguyên. | Khớp mức 10. Tài liệu mới là hồ sơ bắt buộc, không phải sửa tệp starter ngoài phạm vi. |
| Brief | Prompt 1–5 có giữ id/class, cấm sửa CSS/check, một listener trên list, textContent, chặn reload, các thao tác và kết quả Done means. Git cho thấy brief được bổ sung theo từng phần. | Khớp khung 13–15; không thiếu ràng buộc được rubric liệt kê nên tự chấm 15. Không thể dùng Git để chứng minh độc lập từng câu đã được gửi trong hội thoại cũ. |
| AI-LOG | Có mục riêng, tool/request, Changed cụ thể, Rejected, dòng kiểm thử và commit; không bịa lỗi. Còn câu “pass sau khi sửa” ở B1 chưa giải thích. | Không quy việc “không có lỗi” thành vi phạm, nhưng chưa đủ rõ để tự nhận mức tối đa; chọn 18. |
| History | Starter đầu tiên, commit riêng A/B1/B2/B3/B4 với diff và thông điệp tương ứng; thêm commit hồ sơ B4. | Khớp khung 9–10; tự chấm 10. Cần giữ thư mục Git trong ZIP nộp. |

## 2. Bằng chứng đối chiếu bảng Done means

Nguồn tiêu chí: bảng **Done means** trong [README.md](./README.md).
Lượt review cuối do assistant thực hiện trên trình duyệt tích hợp ngày 28/10/2026;
bảng dưới ghi các quan sát kỹ thuật từ lượt review đó. Sau hướng dẫn kiểm tra
toàn bộ Done means và B4, tôi xác nhận nguyên văn: “tôi test tất cả đều hoạt động đúng”.
Xác nhận này được lưu riêng trong [AI-LOG.md](./AI-LOG.md), không gán các số đo
tự động của assistant thành số đo do tôi thu thập.

| Dòng | Kiểm tra và kết quả quan sát | Nguồn bằng chứng |
|---|---|---|
| 1 | Reload: self-check báo **8/8 passed**. | Console và `window.__selfCheck`; cấu trúc trong [index.html](./index.html), gồm template. |
| 2 | So giao diện ban đầu của bài hiện tại với HTML/CSS dựng lại từ ZIP starter: ảnh PNG giống từng pixel, vị trí và nội dung 54 phần tử có class giống nhau tại viewport 1003 × 523. | Lượt review cuối của assistant; đây là so sánh dựng lại. Nhật ký Part A trong [AI-LOG.md](./AI-LOG.md) cũng ghi kiểm tra trước/sau ở thời điểm thực hiện Part A. |
| 3 | Tab trong trang đi qua Search và đủ bảy Add đang hoạt động, bỏ qua Tote bag; viền focus cam `rgb(180, 87, 26)`, dày 3px. Assistant chưa tái kiểm tra từ thanh địa chỉ; hướng dẫn tự kiểm thử cho tôi có bước này và tôi xác nhận tất cả hoạt động đúng. | Lượt review cuối và xác nhận kiểm thử cuối trong [AI-LOG.md](./AI-LOG.md); HTML button/disabled trong [index.html](./index.html), quy tắc focus trong [style.css](./style.css). |
| 4 | Add T-shirt hai lần, thử bấm Add Tote bag: giỏ vẫn 2 món, 360.000 đ. Click tên hoặc giá không tăng giỏ. | B1 trong [app.js](./app.js), listener trên catalogue; nhật ký B1/B4 và lượt review cuối. |
| 5 | Focus Search, nhấn Tab đến Add T-shirt rồi Enter: số lượng tăng đúng một, từ 2 lên 3; tiền từ 360.000 lên 540.000 đ. | Button thật trong [index.html](./index.html); lượt review cuối. |
| 6 | Load more rồi Add Belt: số lượng tăng một, tiền tăng 140.000 đ; danh sách có 12 card và Load more được ẩn. | B1 và phần Load more trong [app.js](./app.js); commit `fe1b3d5`; lượt review cuối. |
| 7 | Sau Load more, `scarf` và `SCARF` đều chỉ hiện Scarf, status là `Showing 1 of 12 products`. Xóa ô tìm kiếm hiện lại 12 card và status rỗng. Thử thêm chữ hoa/thường xen kẽ và khoảng trắng cũng đúng. | `applyFilter()` trong [app.js](./app.js); commit `4cd940b`; lượt review cuối. |
| 8 | Nhập `<img src=x onerror=alert(1)>`: status là `No products match "<img src=x onerror=alert(1)>"`, không có alert, không tạo ảnh hoặc phần tử con trong status. | Ghi thông báo bằng `textContent` trong [app.js](./app.js); nhật ký B2/B3/B4 và lượt review cuối. |
| 9 | Gõ `cap`, Enter và bấm Search: URL, `performance.timeOrigin`, số lượng và tiền trong giỏ giữ nguyên; chỉ hiện Cap. | Listener `submit` và `preventDefault()` trong [app.js](./app.js); commit `ae43b8a`; lượt review cuối. |
| 10 | Không ghi nhận lỗi JavaScript hoặc Console error trong lượt kiểm thử chức năng 23/23. | Theo dõi sự kiện `pageerror` và Console error trên trang bài làm; kiểm tra cú pháp và chẩn đoán trình soạn thảo cũng không báo lỗi. |
| 11 | So với `a6e3ff2`: chỉ hai tệp mã nguồn cho phép thay đổi; CSS, bộ kiểm tra và README giữ nguyên. Commit starter khớp ZIP gốc. | Git diff, đối chiếu nội dung tệp và lịch sử; các lệnh tái kiểm tra tại mục 3. |

**B4:** lượt review cuối xác nhận T-shirt × 2 + Belt × 1 →
`Cart (3) · 500.000 đ`. Một lượt khác thêm Cap khi T-shirt/Belt bị ẩn
vẫn tính đủ tiền các sản phẩm đã mua. Nhật ký B4 trong [AI-LOG.md](./AI-LOG.md)
ghi phép thử 3 món, 500.000 đ rồi thêm Cap thành 4 món, 595.000 đ.
Giá được lấy từ `data-price`, chuyển bằng `Number()` và định dạng `vi-VN`.

Ngoài các dòng trên, assistant kiểm tra tìm `belt` trước Load more rồi nạp thêm:
Belt xuất hiện ngay với `Showing 1 of 12 products`; từ khóa toàn khoảng trắng
hiện lại mọi card và xóa status. Lượt review đầu: **23/23 đạt**.
Theo yêu cầu kiểm tra lại cách chấm, assistant chạy lại một lượt **16/16 đạt**
cho các nhóm HTML, bàn phím, Add/sold-out, Belt, tìm kiếm, XSS, Enter/Search,
tổng tiền và lỗi Console. Hai lượt có cách nhóm phép thử khác nhau; 16 không
phải số lượng kiểm tra bị giảm do có lỗi. Mã nguồn không thay đổi giữa hai lượt.

## 3. Bằng chứng lịch sử Git và phạm vi

| Commit | Nội dung |
|---|---|
| `a6e3ff2` | `starter`: năm tệp starter nguyên bản, trước thay đổi Part A. |
| `65074c1` | `feat: complete Part A semantic HTML`: HTML ngữ nghĩa; thêm brief và nhật ký. |
| `fe1b3d5` | `feat: implement B1 cart event delegation`: một listener cho Add và cộng số lượng. |
| `4cd940b` | `feat: implement B2 safe live search`: lọc khi gõ và thông báo bằng textContent. |
| `ae43b8a` | `fix: prevent B3 search form reload`: chặn submit mặc định. |
| `d56c1a3` | `feat: implement B4 cart total`: thêm tính tổng tiền. |
| `3aad26d` | `docs: record B4 prompt and verification`: bổ sung hồ sơ B4. |

Các lệnh có thể chạy tại thư mục bài làm để đối chiếu:

```bash
git log --oneline --reverse
git show --stat a6e3ff2
git diff a6e3ff2 --stat
git diff a6e3ff2 -- index.html app.js
git diff a6e3ff2 -- style.css check.js README.md
git status --short
```

Lệnh diff cho ba tệp được giữ nguyên không có nội dung thay đổi.
Diff toàn bộ có thêm các tài liệu bắt buộc bên cạnh hai tệp mã nguồn được phép sửa.
Báo cáo này được lập sau commit `3aad26d`; không giả định nó đã được commit hoặc
đã có trong bản trên GitHub tại thời điểm tạo.

## 4. Những gì tôi chưa hoàn thành hoặc chưa kiểm chứng đầy đủ

- Sau khi tự kiểm thử, tôi chưa báo có chức năng bắt buộc nào không hoàn thành.
  Xác nhận cuối là lời báo kết quả trong hội thoại; chưa bổ sung ảnh hoặc video
  riêng cho từng thao tác thủ công. Các số đo kỹ thuật trong mục 2 do assistant
  thu thập, không phải số đo tôi tự cung cấp.
- Tab tích hợp đang ẩn nên click tự động dùng tùy chọn `force`; Tab/Enter trong
  trang đã được kiểm tra, nhưng chưa tái kiểm tra từ thanh địa chỉ hoặc trên
  trình duyệt khác. So sánh ảnh trong lượt review cuối chỉ ở một kích thước.
- Không có tình huống lỗi triển khai của assistant được ghi nhận là đã yêu cầu
  sửa lại. Enter reload ở giai đoạn B2 là hành vi B3 chưa triển khai, không được
  trình bày thành lỗi của B2 để tạo bằng chứng Rejected.
- Mục B1 của nhật ký còn câu “tất cả pass sau khi sửa” nhưng chưa nói sửa gì.
  Chưa xác định đó là chỉnh mã hay chỉnh bộ mô phỏng kiểm thử, nên giữ nguyên
  ghi chép lịch sử và nêu giới hạn này thay vì tự dựng một lời giải thích.
- Mẫu báo cáo trên Classroom chưa được cung cấp trong thư mục bài làm;
  báo cáo sử dụng các thành phần rubric yêu cầu: năm tiêu chí, điểm, bằng chứng,
  tổng điểm và phần chưa làm được. Chưa kiểm chứng gói ZIP cuối và việc nộp bài.

## 5. Thông tin đóng gói

Với tổng tự chấm hiện tại, tên gói nộp là `<StudentID>_98.zip`;
thay `<StudentID>` bằng MSSV thật. Nếu thay đổi điểm tự chấm, phải đổi số trong
tên ZIP cho khớp tổng ở mục 1.

Gói nộp cần chứa thư mục bài làm, thư mục ẩn Git, [brief.md](./brief.md),
[AI-LOG.md](./AI-LOG.md) và [SELF_ASSESSMENT_REPORT.md](./SELF_ASSESSMENT_REPORT.md)
ở cấp cao nhất của thư mục bài làm. Nộp bằng tài khoản Google sinh viên theo đề.
