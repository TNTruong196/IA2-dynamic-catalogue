# brief.md — IA#2 Dynamic HTML

## Prompt 1 — Part A: semantic catalogue

Hãy hoàn thành Part A của bài Session 4 — semantic catalogue.

Trước khi sửa, đọc README.md, index.html, style.css và check.js để hiểu
cấu trúc, giao diện và các kiểm tra.

Phạm vi và ràng buộc:
- Chỉ sửa index.html.
- Giữ nguyên mọi id và class, kể cả trong template; không bỏ hoặc đổi tên.
- Không sửa style.css, check.js, README.md hoặc app.js.
- Giữ nguyên nội dung sản phẩm, data-id, data-price và giao diện hiện tại.
- Không thêm thư viện, framework, inline CSS hoặc onclick nội tuyến.
- Không triển khai chức năng B1–B4 trong bước này.

Yêu cầu:
- Dùng header, nav, đúng một main và footer đúng vị trí.
- Có đúng một h1 cho tiêu đề Catalogue.
- Tên sản phẩm là heading có cấp phù hợp, không nhảy cấp.
- Catalogue là danh sách ul; mỗi card là li.
- Áp dụng cấu trúc tương tự cho card trong template.
- Ô tìm kiếm có label liên kết và thuộc một form.
- Search, Add và Load more là button thật.
- Nút Add của sản phẩm Sold out có thuộc tính disabled,
  đồng thời giữ nguyên các class.
- Chỉ đổi những div cần có ý nghĩa ngữ nghĩa; giữ div cho bố cục khi phù hợp.
- Đặt type cho các button phù hợp với vai trò của chúng.

Tiêu chí hoàn thành theo bảng Done means trong README.md:
1. Reload: Console báo Session 4 self-check: 8/8 passed.
2. So ảnh trước và sau: giao diện không thay đổi.
3. Dùng Tab: focus đến được các nút hoạt động, bỏ qua Add bị disabled,
   và có viền focus màu cam.

Sau khi sửa:
- Giải thích từng nhóm thay đổi bằng ngôn ngữ dễ hiểu.
- Hướng dẫn tôi tự chạy ba kiểm tra trên.
- Phân biệt rõ kiểm tra bạn đã thực hiện và kiểm tra chưa thực hiện.
- Không tự commit hoặc push; dừng để tôi kiểm tra.

---

## Prompt 2 — B1: Add to cart, một listener

Hãy triển khai riêng B1 theo TODO trong app.js và bảng Done means
trong README.md. Part A đã hoàn thành.

Ràng buộc:
- Chỉ sửa app.js; giữ nguyên mọi id và class trong starter.
- Không sửa index.html, style.css, check.js hoặc README.md.
- Không thay đổi phần Load more được cung cấp.
- Không thêm thư viện, framework hoặc onclick nội tuyến.
- Chỉ có MỘT listener click trên catalogue để xử lý tất cả nút Add.
  Không gắn listener riêng lên từng nút Add.
- Ghi nội dung vào DOM bằng textContent.
- Chưa triển khai B2, B3 hoặc B4.

Yêu cầu:
- Xác định nút .add được bấm bằng closest để hỗ trợ cả click
  vào phần tử con bên trong nút.
- Bỏ qua click không thuộc nút Add và nút Add bị disabled.
- Tìm card tương ứng, đọc data-id, tăng cart[id] một đơn vị.
- Xử lý đúng lần đầu cart[id] chưa có giá trị.
- renderCart cộng tổng số lượng của mọi sản phẩm và cập nhật cartCount.
- Sản phẩm được thêm sau bằng Load more cũng phải Add được.

Tiêu chí hoàn thành:
- Done means dòng 4: Add T-shirt hai lần, thử Add Tote bag:
  Cart (2), sản phẩm Sold out không tăng số lượng.
- Dòng 5: Tab đến Add, nhấn Enter: tăng đúng một món.
- Dòng 6: Load more, rồi Add Belt: tăng đúng một món.
- Click tên, giá hoặc vùng trống của card không tăng giỏ hàng.
- Không tạo lỗi đỏ trong Console; Part A vẫn đạt 8/8.

Sau khi sửa:
- Giải thích event bubbling và vì sao một listener hỗ trợ sản phẩm mới.
- Hướng dẫn tôi kiểm tra từng trường hợp.
- Nêu rõ kiểm tra nào đã thực hiện, kiểm tra nào chưa.
- Không tự commit hoặc push.

---

## Prompt 3 — B2: Filter as you type

Hãy triển khai riêng B2 theo TODO trong app.js và bảng Done means
trong README.md. Giữ nguyên hoạt động của Part A và B1.

Ràng buộc:
- Chỉ sửa app.js; giữ nguyên mọi id và class.
- Không sửa index.html, style.css, check.js hoặc README.md.
- Không thay đổi phần Load more được cung cấp.
- Giữ một listener click trên catalogue cho Add; không thêm listener
  riêng vào các nút Add.
- Mọi dữ liệu người dùng hiển thị trong DOM phải dùng textContent,
  tuyệt đối không dùng innerHTML.
- Chưa triển khai B3 hoặc B4.

Yêu cầu:
- Hoàn thành applyFilter và gọi nó trên sự kiện input của ô tìm kiếm.
- Giữ chuỗi gốc người dùng nhập để dùng trong thông báo không có kết quả.
- Dùng giá trị đã trim và chuyển chữ thường để so khớp.
- So khớp theo tên sản phẩm có chứa từ khóa, không phân biệt hoa thường.
- Dùng card.hidden để ẩn hoặc hiện sản phẩm.
- Mỗi lần lọc phải xét tất cả card hiện có trong catalogue,
  gồm sản phẩm đã được thêm bằng Load more.
- Không lọc hoặc tính card nằm trong template chưa được thêm.
- Không thay đổi dữ liệu giỏ hàng khi lọc.

Thông báo phải đúng:
- Từ khóa rỗng hoặc chỉ có khoảng trắng: hiện mọi card, status là ''.
- Có kết quả: Showing X of Y products.
- Không có kết quả: No products match "<nguyên văn người dùng nhập>".
- Chỉ cập nhật một dòng status, không nối thêm thông báo sau mỗi lần gõ.

Tiêu chí hoàn thành:
- Done means dòng 7: sau Load more, scarf và SCARF đều hiện một card
  và Showing 1 of 12 products.
- Trước Load more, mẫu số phải là 8.
- Xóa từ khóa: mọi card hiện lại, status rỗng.
- Dòng 8: nhập <img src=x onerror=alert(1)>:
  không alert, không tạo ảnh; status hiển thị nguyên văn chuỗi đó.
- Nếu tìm belt trước khi Load more, sau Load more phải hiện Belt
  và cập nhật số kết quả đúng.
- B1 và self-check 8/8 vẫn hoạt động; không có lỗi đỏ trong Console.

Sau khi sửa:
- Giải thích vì sao textContent an toàn cho dữ liệu người dùng.
- Hướng dẫn tôi kiểm tra từng trường hợp.
- Nêu rõ kiểm tra nào đã thực hiện và chưa thực hiện.
- Không tự commit hoặc push.

### Trao đổi sau Prompt 3

- **Mình hỏi:** tại sao khi nhập tìm kiếm xong bấm enter thì mọi thứ reload lại hết và giỏ hàng về 0 lại
- **Assistant giải thích:** Enter gửi form theo hành vi mặc định của trình duyệt, làm trang reload và thêm `?q=...` vào URL.
  JavaScript chạy lại từ `const cart = {}`, nên giỏ về 0. B3 sẽ nghe sự kiện `submit`, gọi `event.preventDefault()`
  rồi `applyFilter()`; B3 chưa được triển khai trong phạm vi Prompt 3.
- **Mình phản hồi:** oke rồi thế thì cập nhật AI-LOG và brief đi

---

## Prompt 4 — B3: Search form không reload trang

Hãy triển khai riêng B3 theo TODO trong app.js và bảng Done means
trong README.md. Giữ nguyên hoạt động của Part A, B1 và B2.

Ràng buộc:
- Chỉ sửa app.js; giữ nguyên mọi id và class.
- Không sửa index.html, style.css, check.js hoặc README.md.
- Không thay đổi phần Load more được cung cấp.
- Giữ một listener click trên catalogue cho Add.
- Tiếp tục dùng textContent cho dữ liệu hiển thị.
- Chưa triển khai B4.

Yêu cầu:
- Lấy form qua searchInput.form.
- Lắng nghe sự kiện submit trên form.
- Gọi event.preventDefault() để ngăn điều hướng và reload.
- Sau đó gọi applyFilter().
- Xử lý ở submit của form để cả nhấn Enter và bấm Search đều hoạt động.
- Không thay thế bằng cách chỉ chặn phím Enter.
- Không dùng localStorage để che việc trang bị reload.

Tiêu chí hoàn thành:
- Done means dòng 9: thêm sản phẩm vào giỏ, gõ cap rồi nhấn Enter:
  URL không thêm ?q=cap, trang không reload, số lượng giỏ còn nguyên,
  kết quả tìm kiếm đúng.
- Bấm nút Search cũng không reload và không làm mất giỏ hàng.
- B1, B2, self-check 8/8 vẫn đúng; không có lỗi đỏ trong Console.

Sau khi sửa:
- Giải thích submit và preventDefault().
- Hướng dẫn tôi kiểm tra.
- Nêu rõ kiểm tra nào đã thực hiện và chưa thực hiện.
- Không tự commit hoặc push.

---

## Prompt 5 — B4: tổng tiền trong giỏ

Hãy triển khai B4 theo gợi ý trong renderCart của app.js.
Giữ nguyên hoạt động của Part A và B1–B3.

Ràng buộc:
- Chỉ sửa app.js; giữ nguyên mọi id và class.
- Không sửa index.html, style.css, check.js hoặc README.md.
- Không thay đổi phần Load more được cung cấp.
- Giữ một listener click trên catalogue cho Add.
- Cập nhật nội dung bằng textContent.
- Không thêm thư viện hoặc chức năng ngoài yêu cầu.

Yêu cầu:
- Tính tổng tiền bằng tổng của số lượng từng sản phẩm nhân đơn giá.
- Đọc đơn giá từ data-price trên card; chuyển chuỗi thành số bằng Number().
- Tính đúng cả sản phẩm thêm sau bằng Load more, đặc biệt Belt.
- Sản phẩm bị ẩn do tìm kiếm vẫn được tính nếu đã thêm vào giỏ.
- Giữ cartCount là tổng số món.
- Ghi phần tổng tiền vào cartTotal theo dạng:
  ' · ' + total.toLocaleString('vi-VN') + ' đ'.
- Không sửa giá hiển thị hoặc dữ liệu sản phẩm.

Tiêu chí hoàn thành:
- Reload rồi Add T-shirt hai lần: Cart (2) · 360.000 đ.
- Load more rồi Add Belt một lần: Cart (3) · 500.000 đ.
- Thử Add Tote bag: số lượng và tổng tiền không đổi.
- Tìm cap để ẩn các sản phẩm đã mua: giỏ vẫn 3 món, 500.000 đ.
- Nhấn Enter hoặc bấm Search: giỏ và tổng tiền còn nguyên.
- B1–B3 và self-check 8/8 vẫn đúng; không có lỗi đỏ trong Console.

Sau khi sửa:
- Giải thích cách tính tổng và vì sao cần Number().
- Hướng dẫn tôi kiểm tra.
- Nêu rõ kiểm tra nào đã thực hiện và chưa thực hiện.
- Không tự commit hoặc push.
