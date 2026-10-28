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
- **Commit:** chưa commit hoặc push, theo yêu cầu; không có mã commit Part A để ghi.
