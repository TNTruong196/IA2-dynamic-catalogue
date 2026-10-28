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
