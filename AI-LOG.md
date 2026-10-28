# AI-LOG.md — IA#2 Dynamic HTML

Mỗi phần giao cho assistant có một mục. Hai dòng quan trọng nhất là **Changed** và **Rejected**:
assistant làm sai gì, và dòng nào trong bảng *Done means* ([README.md](./README.md)) đã phát hiện ra.

---

## Part A — semantic HTML ([index.html](./index.html))

- **Tool:** OpenAI Codex (GPT-6) trong VS Code.
- **Request:** Prompt 1 trong [brief.md](./brief.md): thay các `<div>` cần thiết bằng thẻ đúng ý nghĩa, kể cả `<template>`;
  chỉ sửa [index.html](./index.html); giữ mọi `id`/`class`, nội dung sản phẩm, `data-id`/`data-price` và giao diện;
  nút sold-out dùng `disabled`; ô tìm kiếm nằm trong `<form>` có `<label>`; chưa làm B1–B4.
- **Changed (giữ lại):**
  - `.toolbar` → `<header>`, `.menu` → `<nav>`, `.page` → đúng một `<main>`, `.footer` → `<footer>`.
  - `.title` → `<h1>` duy nhất, `.name` → `<h2>` (cả trong `<template>`), không nhảy cấp heading.
  - `#catalogue` → `<ul>`, mỗi `.card` → `<li>` (cả trong `<template>`).
  - `.search` → `<form>`, `.search-label` → `<label for="q">`, nút Search → `<button type="submit">`.
  - Add / Load more → `<button type="button">`; nút Add của Tote bag (sold-out) thêm `disabled`, vẫn giữ class `button add disabled`.
  - `.brand`, `.price`, `.stock`, `#status` và `.more` vẫn là `<div>`; không đổi các phần này khi không cần thiết cho Part A.
  - Giữ nguyên mọi `id`/`class`, dữ liệu, nội dung sản phẩm và các tệp khác; không thêm thư viện, inline CSS hoặc `onclick`.
- **Rejected:** không có. Mình xác nhận assistant làm đúng ngay lần đầu, không cần sửa lại;
  không có dòng *Done means* nào được báo là thất bại cần sửa.
- **Mình đã kiểm tra những gì:**
  - Mình xác nhận kết quả Part A đúng và không có gì cần sửa.
  - Bằng chứng assistant đã thực hiện trong trình duyệt tích hợp:
    - Dòng 1: reload, đọc kết quả bộ tự kiểm tra `window.__selfCheck` → `8/8 passed` — ✅ pass.
    - Dòng 2: chụp ảnh toàn trang trước/sau ở cùng kích thước cửa sổ; dữ liệu ảnh giống hệt nhau → giao diện không đổi — ✅ pass tại kích thước đã thử.
    - Dòng 3: nhấn Tab qua Catalogue, Cart, ô tìm kiếm, Search, 7 nút Add (bỏ qua Tote bag), Load more;
      trạng thái focus có viền cam `#b4571a`, dày 3px — ✅ pass trong trình duyệt tích hợp.
    - Dòng 11: `git diff --stat` → chỉ [index.html](./index.html), 51 dòng thêm / 51 dòng xoá ở thời điểm kết thúc Part A;
      SHA-256 của [README.md](./README.md), [style.css](./style.css), [check.js](./check.js) và [app.js](./app.js) không đổi — ✅ pass.
    - Chẩn đoán trình soạn thảo cho [index.html](./index.html): không có lỗi.
  - Chưa có kiểm tra độc lập Console cho dòng 10 được ghi nhận; chẩn đoán trình soạn thảo không thay thế kiểm tra lỗi đỏ trong Console.
  - Assistant chưa thử thao tác bắt đầu từ thanh địa chỉ trên trình duyệt riêng của mình hoặc so ảnh ở kích thước màn hình khác.
- **Ghi chú:** sau Part A, nhấn Enter trong ô tìm kiếm vẫn có thể reload trang và thêm `?q=`.
  Đây là phần B3 sẽ xử lý, không thuộc Part A. B1–B4 chưa triển khai.
- **Commit:** mình đã commit `65074c1` — "feat: complete Part A semantic HTML".
  Commit gồm [index.html](./index.html) (51+/51−), [brief.md](./brief.md) (41+/0−)
  và [AI-LOG.md](./AI-LOG.md) (38+/0−); tổng 130 dòng thêm / 51 dòng xoá. Assistant không tự commit hoặc push.

---

## B1 — Add to cart, một listener ([app.js](./app.js))

- **Tool:** OpenAI Codex (GPT-6) trong VS Code.
- **Request:** Prompt 2 trong [brief.md](./brief.md): làm riêng TODO B1 và phần B1 trong `renderCart()`;
  chỉ sửa [app.js](./app.js); đúng một click listener trên catalogue; hỗ trợ click phần tử con bằng `closest()`;
  bỏ qua click ngoài Add và nút disabled; xử lý `cart[id]` chưa có giá trị; ghi bằng `textContent`;
  Add được sản phẩm mới sau Load more; chưa triển khai B2–B4.
- **Changed (giữ lại):**
  - `catalogue.addEventListener('click', …)`: một listener duy nhất trên danh sách, không gắn listener riêng vào từng Add.
  - `event.target.closest('.add')` tìm nút Add kể cả khi bấm vào phần tử con; `return` nếu không tìm được nút hoặc `button.disabled`.
  - `button.closest('.card')` tìm card, đọc `card.dataset.id`, rồi tăng `cart[id] = (cart[id] || 0) + 1` và gọi `renderCart()`.
  - `renderCart()` cộng `Object.values(cart)` bằng `reduce()` với giá trị ban đầu 0, ghi tổng vào `cartCount.textContent`.
  - Click truyền lên catalogue (event bubbling), nên các nút Add được Load more thêm vào cũng dùng chung listener.
  - Giữ nguyên phần Load more được cung cấp, các TODO B2–B4 và mọi tệp khác trong bước triển khai B1.
- **Rejected:** không có. Mình xác nhận mọi thứ hoàn thiện, không có lỗi, không cần sửa lại.
- **Mình đã kiểm tra những gì:**
  - Sau khi được hướng dẫn kiểm tra, mình xác nhận toàn bộ kết quả B1 đúng và không có lỗi:
    - Dòng 4: Add T-shirt hai lần, thử Add Tote bag → `Cart (2)`, sold-out không tăng — ✅ pass.
    - Dòng 5: Tab tới Add, nhấn Enter một lần → tăng đúng một món — ✅ pass.
    - Dòng 6: Load more, Add Belt một lần → tăng đúng một món — ✅ pass.
    - Click tên, giá hoặc vùng trống của card → giỏ hàng không tăng — ✅ pass.
    - Dòng 1: Part A vẫn `8/8 passed` — ✅ pass.
    - Dòng 10: Console không có lỗi đỏ — ✅ pass.
  - Assistant đã chạy 9 kiểm tra bằng Node với DOM mô phỏng: một listener trên catalogue, không có listener riêng trên Add,
    giỏ trống, Add T-shirt hai lần, bỏ qua disabled, bỏ qua click ngoài Add, click phần tử con,
    Add Belt sau Load more và số lượng từng sản phẩm; tất cả pass sau khi sửa.
  - `node --check` và chẩn đoán trình soạn thảo không báo lỗi; `git diff --check` không báo lỗi khoảng trắng.
  - Diff B1 chỉ thay đổi [app.js](./app.js); SHA-256 của [index.html](./index.html), [style.css](./style.css),
    [check.js](./check.js), [README.md](./README.md), [brief.md](./brief.md) và [AI-LOG.md](./AI-LOG.md)
    không đổi trong bước triển khai B1. Hai tệp ghi chép được cập nhật riêng sau khi mình xác nhận kết quả.
  - Assistant chưa kiểm tra trực tiếp B1 trong trình duyệt vì trang không được chia sẻ;
    các kết quả thao tác trình duyệt ở trên là xác nhận của mình, không phải kết quả chạy trình duyệt của assistant.
- **Ghi chú:** B2, B3 và B4 chưa triển khai. Search vẫn có thể reload trang khi submit; việc này thuộc B3.
- **Commit:** B1 chưa commit tại thời điểm cập nhật log; assistant không tự commit hoặc push.
