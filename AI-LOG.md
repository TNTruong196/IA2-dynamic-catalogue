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
- **Commit:** mình đã commit `fe1b3d5` — "feat: implement B1 cart event delegation".
  Commit gồm [app.js](./app.js), [brief.md](./brief.md) và [AI-LOG.md](./AI-LOG.md), tổng 91 dòng thêm / 3 dòng xoá.
  Assistant không tự commit hoặc push.

---

## B2 — Filter as you type ([app.js](./app.js))

- **Tool:** OpenAI Codex (GPT-6) trong VS Code.
- **Request:** Prompt 3 trong [brief.md](./brief.md): hoàn thành `applyFilter()` và listener `input`;
  chỉ sửa [app.js](./app.js); giữ nguyên Part A, B1 và phần Load more; so khớp tên bằng chuỗi đã trim/chuyển chữ thường;
  giữ nguyên văn dữ liệu nhập cho thông báo không có kết quả; dùng `card.hidden` và `textContent`; chưa làm B3/B4.
- **Changed (giữ lại):**
  - Giữ `originalQuery = searchInput.value`, dùng `originalQuery.trim().toLowerCase()` để so khớp.
  - Mỗi lần lọc gọi lại `catalogue.querySelectorAll('.card')`, nên xét cả sản phẩm mới sau Load more;
    không lấy hoặc tính card chưa được thêm trong template.
  - Đọc tên qua `.name.textContent.toLowerCase()`, so khớp bằng `includes(query)`, đặt `card.hidden` và đếm số card hiện.
  - Ghi đè một dòng `statusBox.textContent`: `''` khi từ khóa rỗng/toàn khoảng trắng;
    `Showing X of Y products` khi có kết quả; `No products match "<nguyên văn>"` khi không có kết quả.
  - `searchInput.addEventListener('input', applyFilter)` lọc mỗi khi nội dung ô nhập thay đổi.
  - Không thay đổi giỏ hàng, listener Add, phần Load more, B3/B4 hoặc tệp khác trong bước triển khai B2.
- **Rejected:** không có thay đổi B2 nào bị yêu cầu sửa lại.
  Mình hỏi về Enter làm reload và giỏ về 0; sau khi được giải thích đây là B3 chưa triển khai, mình đồng ý giữ phạm vi B2.
- **Mình đã kiểm tra những gì:**
  - Mình quan sát nhấn Enter sau tìm kiếm làm trang reload, URL có `?q=T-shirt` và giỏ trở về 0.
    Đây là hành vi thuộc dòng 9, sẽ sửa ở B3; không ghi dòng này là pass trong B2.
  - Assistant đã kiểm tra trực tiếp trong trình duyệt tích hợp:
    - Trước Load more, nhập `  ScArF  ` → chỉ Scarf, `Showing 1 of 8 products` — ✅ pass.
    - Tìm `belt` trước Load more → không có kết quả; bấm Load more → chỉ Belt, `Showing 1 of 12 products` — ✅ pass.
    - Dòng 7: sau Load more, `scarf` và `SCARF` đều chỉ Scarf, `Showing 1 of 12 products` — ✅ pass.
    - Xoá từ khóa hoặc nhập toàn khoảng trắng → hiện đủ 12 card, status rỗng — ✅ pass.
    - Dòng 8: nhập `  <img src=x onerror=alert(1)>  ` → status giữ nguyên chuỗi, kể cả khoảng trắng;
      không có alert, không tạo phần tử ảnh hoặc thẻ con trong status — ✅ pass với chuỗi thử có thêm khoảng trắng.
    - So khớp chuỗi con: `pack` → Backpack, `Showing 1 of 12 products` — ✅ pass.
    - B1: Add T-shirt hai lần rồi lọc nhiều lượt → số vẫn là 2; Add Belt sau Load more → 3;
      click tên/giá không tăng; Tab tới Add rồi Enter → 4. Dữ liệu cuối là `{"tshirt":3,"belt":1}` — ✅ pass.
    - Card trong template không bị thay đổi trạng thái ẩn — ✅ pass.
    - Dòng 1: kết quả self-check vẫn `8/8 passed` — ✅ pass.
    - Dòng 10: không ghi nhận lỗi JavaScript hoặc Console error trong lượt thử — ✅ pass.
  - `node --check`, chẩn đoán trình soạn thảo và `git diff --check` không báo lỗi.
  - Diff B2 chỉ thay đổi [app.js](./app.js) (19+/9−); SHA-256 của các tệp cần giữ nguyên, kể cả hai tệp ghi chép,
    không đổi trong bước triển khai. Hai tệp ghi chép được cập nhật riêng sau đó.
  - Chưa kiểm tra trên các trình duyệt khác; không coi kiểm tra của assistant là thao tác mình đã tự chạy.
- **Ghi chú:** `textContent` hiển thị chuỗi như văn bản, không phân tích thành thẻ HTML hoặc mã xử lý sự kiện.
  Enter hoặc nút Search vẫn submit form theo mặc định vì B3 chưa làm, khiến trang tải lại và khởi tạo lại `cart = {}`.
  B3 sẽ dùng `submit` + `event.preventDefault()` rồi gọi `applyFilter()`; B4 cũng chưa triển khai.
- **Commit:** mình đã commit `4cd940b` — "feat: implement B2 safe live search".
  Commit gồm [app.js](./app.js), [brief.md](./brief.md) và [AI-LOG.md](./AI-LOG.md).
  Assistant không tự commit hoặc push.

---

## B3 — Search form không reload trang ([app.js](./app.js))

- **Tool:** OpenAI Codex (GPT-6) trong VS Code.
- **Request:** Prompt 4 trong [brief.md](./brief.md): lấy form qua `searchInput.form`, nghe `submit`,
  gọi `event.preventDefault()` rồi `applyFilter()`; chỉ sửa [app.js](./app.js);
  giữ nguyên Part A, B1, B2 và phần Load more; không chặn riêng phím Enter, không dùng localStorage; chưa làm B4.
- **Changed (giữ lại):**
  - `searchInput.form.addEventListener('submit', …)` xử lý cả Enter trong ô nhập và bấm Search.
  - `event.preventDefault()` ngăn hành vi gửi form mặc định, nên không điều hướng hoặc reload trang.
  - Gọi `applyFilter()` ngay sau đó để cập nhật kết quả và status theo nội dung ô tìm kiếm.
  - Giữ nguyên listener Add, bộ lọc B2, phần Load more, mọi id/class và các tệp khác; không thêm lưu trữ giỏ hàng.
- **Rejected:** không có. Mình xác nhận mọi thứ triển khai đúng, không có lỗi và không cần sửa lại.
- **Mình đã kiểm tra những gì:**
  - Sau khi được hướng dẫn kiểm tra, mình xác nhận kết quả B3 đúng và không có lỗi:
    - Dòng 9: Add T-shirt hai lần, gõ `cap`, nhấn Enter → chỉ Cap, URL không thêm `?q=cap`, giỏ vẫn `Cart (2)` — ✅ pass.
    - Bấm Search cũng không reload hoặc mất giỏ hàng — ✅ pass.
    - B1, B2, self-check `8/8` vẫn đúng, Console không có lỗi đỏ — ✅ pass.
  - Assistant đã chạy kiểm tra trong trình duyệt tích hợp:
    - Enter và Search giữ nguyên URL và `performance.timeOrigin`; không ghi nhận điều hướng, giỏ vẫn 2 và kết quả `Showing 1 of 8 products`.
    - Add Cap sau submit → giỏ 3; tìm `belt` không có kết quả vẫn giữ giỏ.
    - Load more khi đang tìm `belt` → hiện Belt, `Showing 1 of 12 products`; Add Belt rồi Search → giỏ vẫn 4.
    - `scarf` và `SCARF` rồi Enter đều hiện Scarf, `Showing 1 of 12 products`.
    - Nhập `<img src=x onerror=alert(1)>` rồi Search → thông báo nguyên văn, không ảnh hoặc alert.
    - Từ khóa toàn khoảng trắng rồi Enter → hiện đủ 12 card, status rỗng, giỏ vẫn 4.
    - Self-check đạt `8/8`; không ghi nhận lỗi JavaScript hoặc Console error trong lượt thử.
  - Tab trình duyệt đang ẩn khiến click thông thường timeout; assistant dùng click với tùy chọn `force` để kiểm tra xử lý sự kiện.
    Đây là giới hạn của thao tác tự động, không phải lỗi mã B3. Chưa thử trên trình duyệt khác.
  - `node --check`, chẩn đoán trình soạn thảo và `git diff --check` không báo lỗi.
  - Diff B3 chỉ thay đổi [app.js](./app.js) (4+/1−); SHA-256 của các tệp khác, gồm hai tệp ghi chép, không đổi
    trong bước triển khai. Hai tệp ghi chép được cập nhật riêng sau khi mình xác nhận kết quả.
- **Ghi chú:** `submit` là sự kiện gửi form; `preventDefault()` huỷ hành vi gửi mặc định mà vẫn cho phép chạy bộ lọc.
  B3 giữ giỏ khi tìm kiếm bằng Enter/Search; tải lại trang bằng F5 vẫn khởi tạo giỏ về 0 vì chưa có lưu trữ lâu dài.
  B4 chưa triển khai.
- **Commit:** mình đã commit `ae43b8a` — "fix: prevent B3 search form reload".
  Assistant không tự commit hoặc push.

---

## B4 (stretch) — tổng tiền trong giỏ ([app.js](./app.js))

- **Tool:** OpenAI Codex (GPT-6) trong VS Code.
- **Request:** Prompt 5 trong [brief.md](./brief.md): bổ sung tổng tiền trong `renderCart()`;
  chỉ sửa [app.js](./app.js); đọc `data-price` bằng `Number()`, nhân số lượng và định dạng `vi-VN`;
  tính cả sản phẩm mới sau Load more và sản phẩm bị ẩn; giữ nguyên Part A, B1–B3 và phần Load more.
- **Changed (giữ lại):**
  - Khởi tạo `total = 0`, duyệt `Object.entries(cart)` để lấy từng `[id, quantity]`.
  - Tìm card bằng ``catalogue.querySelector(`.card[data-id="${id}"]`)``; truy vấn gồm cả card đang ẩn và card mới được thêm.
  - Cộng `quantity * Number(card.dataset.price)` vào tổng tiền; `Number()` chuyển dữ liệu chuỗi thành số để tính toán.
  - Ghi `' · ' + total.toLocaleString('vi-VN') + ' đ'` vào `cartTotal.textContent`.
  - Giữ nguyên cách cộng số món trong `cartCount`, listener Add, B2, B3, Load more, giá hiển thị và dữ liệu sản phẩm.
- **Rejected:** không có thay đổi B4 nào bị yêu cầu sửa lại trước khi cập nhật log.
- **Mình đã kiểm tra những gì:**
  - Mình yêu cầu cập nhật ghi chép sau khi assistant báo kết quả; chưa có xác nhận riêng từng thao tác kiểm tra thủ công của mình.
  - Assistant đã chạy kiểm tra trong trình duyệt tích hợp:
    - Reload → `Cart (0)`; Add T-shirt hai lần → `Cart (2) · 360.000 đ` — ✅ pass.
    - Load more rồi Add Belt → `Cart (3) · 500.000 đ` — ✅ pass.
    - Thử Add Tote bag (disabled) → số lượng và tiền không đổi — ✅ pass.
    - Tìm `cap` để ẩn sản phẩm đã mua → giỏ vẫn 3 món, 500.000 đ — ✅ pass.
    - Nhấn Enter rồi bấm Search → giỏ và tiền giữ nguyên; URL và `performance.timeOrigin` không đổi, không có điều hướng — ✅ pass.
    - Add Cap khi T-shirt và Belt đang ẩn → `Cart (4) · 595.000 đ`, chứng minh lần tính lại vẫn gồm sản phẩm bị ẩn — ✅ pass.
    - B2: `scarf`/`SCARF` → `Showing 1 of 12 products`; chuỗi `<img src=x onerror=alert(1)>` giữ nguyên văn,
      không tạo ảnh/alert; xoá từ khóa → 12 card, status rỗng — ✅ pass.
    - Tab tới Add rồi Enter → `Cart (5) · 775.000 đ`, tăng đúng một T-shirt — ✅ pass.
    - Self-check vẫn `8/8`; không ghi nhận lỗi JavaScript hoặc Console error — ✅ pass.
    - Đơn giá `data-price` và giá hiển thị của tám sản phẩm ban đầu không đổi — ✅ pass.
  - Tab đang ẩn nên click tự động dùng `force`; chưa thử trên các trình duyệt khác.
  - `node --check`, chẩn đoán trình soạn thảo và `git diff --check` không báo lỗi.
  - Diff triển khai B4 chỉ thêm 6 dòng trong [app.js](./app.js); SHA-256 của các tệp khác, kể cả hai tệp ghi chép,
    không đổi trong bước triển khai. Hai tệp ghi chép được cập nhật riêng sau đó.
- **Ghi chú:** tổng tiền lấy từ các mục trong giỏ, không phụ thuộc card có đang hiển thị hay không.
  Mã hiện tại giả định card của sản phẩm đã mua vẫn tồn tại trong catalogue; starter chỉ ẩn hoặc thêm card, không xoá card.
- **Commit:** mình đã commit `d56c1a3` — "feat: implement B4 cart total".
  Assistant không tự commit hoặc push.
