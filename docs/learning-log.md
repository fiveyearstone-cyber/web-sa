# Nhật ký học tập

## Trạng thái hiện tại

- **Giai đoạn**: 0 — Bức tranh toàn cảnh (đang học)
- **Bài hiện tại**: Bài 2 — REST & thiết kế API, tổng quan kiến trúc phần mềm, phân tích nghiệp vụ thương mại điện tử (bắt đầu 2026-11-16). Phần A: đã giảng xong; người học chủ động chuyển tiếp, **còn nợ** 5 câu kiểm tra Phần A 2/2, bảng BT3 đầy đủ, tóm tắt R1 (phải nộp trước khi đóng Bài 2). Phần B: đã giảng 2026-11-16, chờ câu hỏi kiểm tra + bài tập + tóm tắt R2. Phần C chưa bắt đầu
- **Bài đã đóng**: Bài 1 (2026-11-16)
- **Môi trường**: .NET SDK 11.0.100 đã cài (2026-11-13). PostgreSQL: hướng dẫn cài ở Giai đoạn 4.

## Điểm yếu cần củng cố

- **Idempotent** (Bài 1 → Bài 2): ⚠️ **đã tiến bộ rõ** (đúng 6/6 câu phân loại ở Bài 2); câu 7 đạt một phần: nhận ra bài toán đồng thời nhưng chưa tách được nó khỏi chuyện gửi lại request → đã giảng bảng hai bài toán; kiểm tra lại khi sửa bảng BT3 (dòng 5 đổi giá, dòng 6 đặt hàng). Trước đó ở Bài 2, người học chưa hiểu "trạng thái server" là gì; nhầm idempotent với "server vẫn chạy đúng logic"; không phân loại được PATCH giá trị tuyệt đối và PATCH tăng 10%. Đã giảng lại: trạng thái = dữ liệu server lưu mà request sau quan sát được; idempotent ≠ không thay đổi; f(f(x)) = f(x); ví dụ nút gọi thang máy, công tắc bật/tắt. Ở Bài 1: Người học đề xuất dùng ConcurrencyStamp (biết từ dự án thực tế) để chống gửi lại request. Cần củng cố: phân biệt rõ hai bài toán (request trùng lặp và nhiều người sửa đồng thời); kiểm tra lại ở Bài 2 khi thiết kế API.
- **Middleware là các lớp bọc lồng nhau** (Bài 1, câu 6): ✅ đã nắm qua câu bổ sung 3. Người học tự đặt câu hỏi về short-circuit. Cần chỉnh: Authentication không chặn request, Authorization mới chặn.
- **Trạng thái dùng chung & race condition** (Bài 1, câu 2): ✅ đã nhận ra race condition. Người học hỏi Singleton có giải quyết được không; đã giải thích Singleton chính là trạng thái dùng chung, và giới thiệu các hướng xử lý. Học sâu ở GĐ 2 (thread-safety) và GĐ 4 (concurrency trong DB).
- **Testing**: chưa viết test bao giờ → học từ đầu, bắt đầu ở GĐ 2 với bài tập console (logic giỏ hàng, tính giá thuần, rất dễ test).
- **Mô hình biên dịch** (Bài 1, câu 1): tưởng package NuGet đã được JIT sẵn. Đúng: package cũng là IL, JIT chạy trên server lúc ứng dụng chạy.

## Kỹ năng đọc tài liệu

Quy trình: xem CLAUDE.md mục 5.3. Áp dụng từ Bài 2.

| Bài | Tài liệu | Ngày nộp | Kết quả | Ghi chú |
|---|---|---|---|---|
| 2 | R1 — Web API design best practices (Microsoft) — giao 2026-11-16 | | | |
| 2 | R2 — Common web application architectures (Microsoft) — giao 2026-11-16 | | | |

## Chủ đề hoãn lại / cần quay lại

- **Bài 1 — BT1, phỏng đoán vì sao có nhiều runtime** (NETCore.App / AspNetCore.App / WindowsDesktop.App): chưa nộp → hỏi lại ở Giai đoạn 1 (chủ đề runtime, shared framework).
- **Bài 1 — 3 câu hỏi kiểm tra về cookie** (localStorage có tự gửi lên server không; vì sao cần `HttpOnly`; form ẩn từ trang lạ gửi tới shopee.vn → CSRF): chưa nộp → hỏi lại khi học Authentication ở Giai đoạn 7.
- **Bài 1 — BT2, thực nghiệm ④⑤** (bấm "thêm vào giỏ" 2 lần; thao tác thất bại trả status gì): không bắt buộc, chưa làm → dùng làm ví dụ ở Bài 2 Phần A.

---

## Bài 2 — REST & thiết kế API, tổng quan kiến trúc, phân tích nghiệp vụ (đang học)

**Mục tiêu**
- Thiết kế được URI, method, status code cho API theo phong cách REST; biết khi nào RPC hợp lý hơn.
- Xử lý được các hành động không phải CRUD (huỷ đơn, hoàn tiền, đổi giá) và lỗi (ProblemDetails, tổng quan).
- Hiểu vì sao cần kiến trúc; phân biệt các kiểu kiến trúc chính ở mức bản đồ.
- Phân tích nghiệp vụ thương mại điện tử: actor, use case, module.

**Kế hoạch** (dự kiến 2–3 buổi)

| Phần | Nội dung | Bài đọc bắt buộc (sau khi giảng) |
|---|---|---|
| A | REST & thiết kế API: resource, URI, method, status code, RPC và REST, hành động không phải CRUD, idempotency trong thiết kế API, versioning/pagination/lỗi (tổng quan). **Chữa BT3 của Bài 1.** | R1 — [Web API design best practices](https://learn.microsoft.com/en-us/azure/architecture/best-practices/api-design): đọc từ đầu tới **hết mục *Implement asynchronous methods*** (đã kiểm tra cấu trúc trang 2026-11-16: bản cập nhật 2025-03, khoảng 2.500 từ trong phạm vi). Bỏ qua từ *Implement data pagination and filtering* trở đi. |
| B | Tổng quan kiến trúc phần mềm: vì sao cần kiến trúc, monolith, layered, clean/onion/hexagonal, modular monolith, microservices (bản đồ) | R2 — [Common web application architectures](https://learn.microsoft.com/en-us/dotnet/architecture/modern-web-apps-azure/common-web-application-architectures): đọc từ đầu tới hết mục *Clean architecture* (không cần đọc *Organizing code in Clean Architecture*). Bỏ qua phần Docker (ngoài phạm vi). |
| C | Phân tích nghiệp vụ thương mại điện tử: actor, use case, module, các luồng chính (đặt hàng, thanh toán, tồn kho) | — |

**Đầu vào từ Bài 1**
- BT3: người học đã liệt kê 12 hành động (thêm/sửa/xoá sản phẩm, nhập kho, đổi giá, mua, thêm vào giỏ, cập nhật địa chỉ, cập nhật thông tin đơn hàng, huỷ đơn, refund). Người học báo đã hoàn thành bài tập, nhưng AI **chưa nhận được** phần method/URL/status code → đầu Phần A: người học gửi bảng (nếu đã làm) hoặc điền ngay trước khi giảng.
- **BT3 đã nộp (2026-11-16)**: bảng 11 hành động có method/URL/body/status. Nhận xét sơ bộ: dòng 1–3 chuẩn (danh từ số nhiều, 201/204); có tư duy nghiệp vụ tốt (đã bán thì chỉ vô hiệu hoá; 409 khi giá đã bị sửa trước, liên hệ ConcurrencyStamp; không gửi giá khi đặt hàng). Cần chữa: động từ hoặc danh động từ trong URL (`stock-in`, `purchasing`, `cancel`, `refund`); trả 200 cho hành động tạo bản ghi (nhập kho, hoàn tiền), chưa nghĩ tới 202 cho xử lý bất đồng bộ; PATCH "thêm số lượng" vào giỏ là thay đổi tương đối (lặp lại điểm yếu Bài 1); PUT cả đơn hàng (client có thể sửa trạng thái/tổng tiền); lạm dụng 400/401, chưa phân biệt 400/409/422; gửi id trong body dù đã có trên path; tên số ít/số nhiều không nhất quán (`/order` và `/products`). Đã đặt câu hỏi gợi mở a–f, chờ trả lời cùng Việc 2.
- **Việc 2 (dự đoán 5 câu) đã nộp (2026-11-16)**: (1) động từ trong URL thừa vì method đã mang nghĩa: đúng một phần, còn thiếu ý "URL là danh từ, method là hành động; tránh bùng nổ số động từ", và POST không đồng nghĩa với "add"; (2) versioning để chuyển đổi dần dần: đúng; (3) 200 vẫn ổn: chấp nhận được nhưng thiếu lý do (phụ thuộc vào việc có tạo resource mới có URI riêng không); (4) 2 sản phẩm, không idempotent: đúng; (5) luôn trả 200 thì lãng phí quy ước của HTTP: đúng, thiếu ý hạ tầng (monitoring, proxy, retry, thư viện client) dựa vào status code, và thiếu ý cần cả status code lẫn mã lỗi nghiệp vụ trong body. Câu a–f chưa trả lời → lồng vào bài giảng và câu hỏi kiểm tra.
- BT2: các câu hỏi mở cho Phần A: động từ trong URL (`add_to_cart`, kiểu RPC) và REST; versioning trong URL (`/api/v4`); POST trả 200 hay 201; `add_to_cart` có idempotent không; API luôn trả 200 và để mã lỗi trong body.

**Câu hỏi kiểm tra phần 1/2 (2026-11-16)**
- Câu 1 (path/query): ✅ phần định danh; ❌ nghĩ bỏ query string thì ra resource khác hoặc URL lỗi. Đã chữa, kèm sắc thái: về kỹ thuật URI đầy đủ (gồm query) là một khoá cache riêng.
- Câu 2–3 (idempotent): ❌ chưa hiểu "trạng thái server" → giảng lại, giao 7 câu phân loại.
- Câu hỏi người học tự đặt (tốt): "Nếu PUT mà body là 'tăng 10%' thì sao?" → đã giảng: idempotent của method là **lời hứa (hợp đồng) của đặc tả**, framework không tự đảm bảo; PUT "+10%" là phá hợp đồng (lỗi thiết kế), nguy hiểm vì client/proxy được phép tự gửi lại request idempotent; PATCH thì không hứa idempotent; lệnh tương đối nên dùng POST. Giao thêm câu 8.
- **7 câu phân loại idempotent (2026-11-16)**: câu 1–6 ✅ **đúng cả 6**, lập luận theo trạng thái server; câu 4 nhận ra PATCH vẫn có thể idempotent và response 409 không ảnh hưởng (tốt). Nhắc: "giữ lời hứa của method" không phải lý do (lập luận vòng tròn), lý do thật là thay đổi tuyệt đối; "trạng thái không đổi" phải nói chính xác là "không đổi THÊM sau lần đầu". Câu 7: ⚠️ đạt một phần. Nhận ra đây là bài toán đồng thời ("race condition"), nhưng không trả lời PUT có còn idempotent không (có), và chưa thấy việc gửi lại không phải nguyên nhân (không có retry vẫn mất dữ liệu nếu A sửa dựa trên dữ liệu cũ). Đã giảng: lost update = race kiểu read-modify-write (giống `x++` ở Bài 1); bảng hai bài toán (request trùng lặp → idempotent/idempotency key; sửa đồng thời → optimistic concurrency/ETag + If-Match → 412); ConcurrencyStamp không giải quyết được POST tạo đơn trùng. Người học chọn 409 cho lần huỷ thứ 2 (để báo đã huỷ trước đó) → hợp lệ; đã đặt kịch bản phản biện (response lần 1 bị mất, client tự gửi lại thì nhận 409 và báo "huỷ thất bại" sai), Người học **tự suy ra idempotency key** ✅ và tự nêu vấn đề vòng đời key phía client (giữ key cũ khi gửi lại, sinh key mới khi có ý định mới) ⭐. Đã giảng bổ sung (tổng quan): key = một ý định của người dùng; server lưu key + dấu vân tay request + response rồi phát lại response cũ; cùng key khác body thì báo lỗi; key đang xử lý; phạm vi theo user; TTL; lưu key và thực hiện hành động phải nguyên tử (atomic). Header `Idempotency-Key` (bản nháp IETF, Stripe phổ biến). Học sâu ở GĐ 7. Hướng 1 (mã lỗi nghiệp vụ trong body) để dành cho ProblemDetails ở phần 2/2. Câu 8: ⚠️ đạt một phần, ý đúng nhưng chung chung → đã bổ sung: mất cache (CDN/trình duyệt), mất khả năng tự retry an toàn, mất hành vi trình duyệt (bookmark, back, crawler), khó giám sát/rate limit theo method.
- Câu 4 (trường server tự quản lý): đạt một phần (ID đúng; mã/SKU tuỳ nghiệp vụ). Bổ sung: thời điểm tạo/sửa, người tạo, **số lượng tồn** (phải đi qua luồng nhập kho), lượt bán, điểm đánh giá, version/ConcurrencyStamp.
- Câu 5 (resource ≠ bảng): đạt. Bổ sung: resource tính toán, không có bảng.

**Phần A 2/2 (giảng 2026-11-16)**: người học tự tổng kết safe/idempotent đúng (chỉnh: PATCH là "không đảm bảo", không phải "không"). Đã giảng: nhóm status code; 200/201/202/204; cây quyết định 4xx (400/401/403/404/409/412/422/428/429); 5xx; 4 cách xử lý hành động không phải CRUD (đổi trường trạng thái / danh từ hoá / custom action / RPC); RPC và REST, gRPC, GraphQL; ETag + If-Match; versioning, phân trang (offset và cursor), ProblemDetails (RFC 9457); quy ước dữ liệu (camelCase, ISO 8601 UTC, tiền tệ).

**Bài tập**
- **BT1 — Sửa lại bảng BT3** theo kiến thức Phần A (tiêu chí: xem tin nhắn giảng Phần A 2/2): chưa nộp bảng đầy đủ. Đã gửi nhận xét trước (2026-11-16): ✅ hoàn tiền dùng 202, hoặc 201 với Location tới resource hoàn tiền. ❌ 201 kèm Location tới chi tiết đơn hàng (Location phải trỏ tới resource MỚI tạo). ⚠️ **Lại nhầm hai bài toán**: xếp nhập kho và hoàn tiền vào lost-update (thực ra là tạo mới → bài toán gửi lại); bỏ sót đặt hàng và hoàn tiền ở bài toán gửi lại (nguy hiểm nhất). Đã dạy phép thử: "tạo mới hay sửa cái đã có dựa trên bản đã đọc?"
- **BT2 — Câu hỏi kiểm tra Phần A 2/2** (5 câu): chưa nộp.
- **Bài đọc R1**: đã giao 2026-11-16, chưa nộp.
- ⏸ Người học nói "đã ok kiến thức phần này" và chuyển sang Phần B khi chưa nộp các mục trên → ghi nợ; hỏi lại trước khi đóng Bài 2. Lưu ý: ngay trước đó vẫn nhầm hai bài toán (gửi lại / lost update) → kiểm tra lại khi chấm bảng BT3.

**Phần B (giảng 2026-11-16)**: kiến trúc là gì và cái giá; coupling/cohesion; hai trục độc lập (tổ chức code: all-in-one / layered / clean-onion-hexagonal / vertical slice; triển khai: monolith / modular monolith / microservices); Dependency Inversion là bản lề; cây thư mục solution Clean Architecture; khi nào KHÔNG dùng; Conway's Law; "monolith first"; lộ trình kiến trúc của khoá.
- **BT3 (Phần B) — Xếp chỗ 12 thành phần vào 4 project + sơ đồ phụ thuộc**: chưa nộp.
- **Câu hỏi kiểm tra Phần B** (5 câu): chưa nộp.
- **Bài đọc R2**: đã giao 2026-11-16 (phạm vi: từ đầu đến hết mục *Clean architecture*, dừng trước *Organizing code in Clean Architecture*; bài ~4.200 từ, phạm vi ~1.800 từ; nội dung 2021, ví dụ MVC/Azure), chưa nộp.

**Kết quả**: _(cập nhật khi đóng bài)_

---

## Bài 1 — Hệ sinh thái .NET, HTTP, hành trình của một request (đã đóng 2026-11-16)

- **Câu hỏi kiểm tra**: ✅ đã trả lời và chữa xong (cả 3 câu bổ sung).
- **BT1 (Cài đặt và quan sát môi trường)**: ✅ đã cài SDK 11.0.100, gửi ghi chép phiên bản SDK và danh sách runtime. Đã giảng thêm: số phiên bản SDK (feature band 1xx) khác runtime, cài song song nhiều phiên bản (side-by-side), các runtime cũ đã hết hỗ trợ. ⏸ Phần phỏng đoán chưa nộp → xem "Chủ đề hoãn lại".
- **BT2 (Soi API của một trang thật)**: ✅ 3 request trên một trang thương mại điện tử lớn (GET itemcard/set/elements?set_ids=2 → 200; POST cart/add_to_cart → 200; POST /api/v4/web/subcart kèm toàn bộ request header) và câu hỏi về cookie, bộ nhớ trình duyệt. Đã giảng: cơ chế Set-Cookie/Cookie, thuộc tính cookie, session ID và JWT, cookie/localStorage/sessionStorage/IndexedDB, XSS và CSRF (tổng quan), các header lạ (pseudo-header HTTP/2, sec-fetch-*, header chống bot). ⚠️ Người học dán cả cookie phiên đăng nhập thật, nhưng đã chủ động đăng xuất trước khi gửi (ý thức bảo mật tốt). Đã nhắc nguyên tắc không dán cookie/token vào bất kỳ đâu.
- **BT3 (Tự thiết kế thử)**: ⏸ có danh sách hành động, chưa có method/URL/status → chuyển sang đầu Bài 2 Phần A.

---

## Lịch sử buổi học

### 2026-11-13 — Thiết lập dự án
- Thống nhất mục tiêu, vai trò AI, quy tắc không viết code, phương pháp học.
- Chốt: .NET mới nhất (.NET 11), e-commerce Web API, PostgreSQL cài trên máy, không dùng Docker.
- Tạo `CLAUDE.md`, `docs/knowledge-map.md`, `docs/learning-log.md`.

### 2026-11-13 — Bài 1: Bức tranh toàn cảnh (phần 1)
- Đã giảng: các thành phần của hệ sinh thái .NET (so sánh với JS/PHP), lịch sử .NET Framework → .NET, LTS/STS, cách C# được biên dịch và chạy (tổng quan), mô hình process chạy liên tục của ASP.NET Core khác PHP thế nào, HTTP (request/response, method, safe/idempotent, status code, header, stateless), hành trình của một request qua ASP.NET Core.
- Câu hỏi kiểm tra: đúng 1, 3, 5; thiếu ý ở câu 2; sai khái niệm ở câu 4, 6 → đã chữa.
- Câu hỏi bổ sung: câu 2 và câu 3 đúng; câu 1 còn sai ở (b) (PATCH thay đổi tương đối).
- Câu hỏi người học tự đặt (dấu hiệu tốt): giải quyết tranh chấp đồng thời thế nào, Singleton có giải quyết được không; middleware có thể chặn request và trả response luôn không (short-circuit).
- Đã giảng thêm: vì sao `x++` không atomic; các hướng xử lý (atomic, lock, không chia sẻ trạng thái, đẩy xuống database); Singleton pattern và Singleton lifetime trong DI; short-circuit; Authentication khác Authorization.
- Câu hỏi chốt về idempotent: người học đề xuất ConcurrencyStamp (optimistic concurrency) → đúng. Đã giảng thêm: 2 bài toán khác nhau (request trùng lặp và sửa đồng thời), idempotency key, đổi thiết kế thành tạo bản ghi có ID do client cấp + unique constraint, ETag/If-Match, sổ cái tồn kho (ledger, tổng quan).
- Người học có kinh nghiệm thực tế với ConcurrencyStamp → tận dụng khi dạy optimistic concurrency ở GĐ 4.

### 2026-11-13 — Chữa bài tập Bài 1
- BT1, BT2: xem section Bài 1. Giảng thêm về cookie và bộ nhớ trình duyệt (đã thêm 2 chủ đề vào knowledge-map, Giai đoạn 7).

### 2026-11-16 — Đóng Bài 1, chuẩn bị Bài 2
- Người học báo hoàn thành Bài 1. Các phần chưa nộp được ghi vào "Chủ đề hoãn lại"; BT3 chuyển sang đầu Bài 2.
- Người học đề nghị: từ Bài 2, mỗi bài giao tài liệu chính thống để đọc và nộp tóm tắt → đã thêm quy trình vào CLAUDE.md mục 5.3.
- Tạo section Bài 2 (kế hoạch 3 phần, 2 bài đọc bắt buộc).

### 2026-11-16 — Định hướng học trong thời kỳ AI
- Người học hỏi: có AI rồi thì còn cần học lập trình theo lộ trình này không. Đã phân tích: AI làm rẻ việc gõ code, nhưng việc hiểu, đánh giá và chịu trách nhiệm thì không rẻ đi; muốn review code AI viết thì phải hiểu sâu hơn người viết ra nó.
- **Người học chốt**: vẫn hướng tới tự code được. Không ngại syntax; thấy cái khó là luồng code, kiến trúc, design pattern được áp dụng và vì sao. Chưa viết test bao giờ → cần hướng dẫn từ đầu. Coi việc sửa lỗi trong code do AI sinh ra là kỹ năng cần có.
- Điều chỉnh: thêm mục "Kỹ năng xuyên suốt" vào knowledge-map (đọc luồng code, debugging, testing từ GĐ 2, review code AI, mini-ADR); chi tiết hoá phần testing ở GĐ 5; cập nhật hồ sơ người học trong CLAUDE.md.
- **Đã chốt** nguồn code cho bài tập review: mặc định người học tự lấy code từ công cụ AI khác (A); thỉnh thoảng AI viết đoạn code có cài sẵn lỗi để luyện đúng một loại lỗi (B). Đã ghi ngoại lệ vào CLAUDE.md mục 3.

### 2026-11-16 — Bài 2, Phần A (1/2)
- Người học nộp BT3 (bảng 11 hành động) và Việc 2 (dự đoán 5 câu). Chưa trả lời câu gợi mở a–f → lồng vào bài giảng.
- Đã giảng: REST là phong cách kiến trúc (Fielding, các ràng buộc), Richardson Maturity Model (mục tiêu Level 2), resource ≠ bảng DB, representation, quy tắc URI (số nhiều, nhất quán, lồng không quá sâu, kebab-case, singleton `/me/cart`, BOLA/IDOR), path parameter và query string, ngữ nghĩa method theo RFC 9110, idempotent do thiết kế (tuyệt đối/tương đối), JSON Merge Patch và JSON Patch, PUT và mass assignment (liên hệ `$fillable`, DTO), ai cấp ID.
- Câu hỏi kiểm tra: câu 1 sai nửa sau, câu 2–3 chưa hiểu "trạng thái server", câu 4–5 đạt → đã giảng lại idempotent, kèm câu hỏi người học tự đặt về PUT "+10%" (idempotent là lời hứa của spec).
- 7 câu phân loại + câu 8: đã nộp và chấm (câu 1–6 đúng hết; câu 7, 8 đạt một phần). Người học tự suy ra idempotency key khi thảo luận chuyện huỷ lần 2 trả 409.
- Đã giảng Phần A 2/2 và giao R1, bài tập sửa bảng BT3, 5 câu kiểm tra. Người học chỉ gửi nhận xét một phần về bảng (lại nhầm hai bài toán) rồi chủ động chuyển sang Phần B → ghi nợ.
- Đã giảng Phần B (tổng quan kiến trúc), giao R2, bài tập xếp chỗ 12 thành phần, 5 câu kiểm tra. Người học phản hồi "phần này thú vị", hẹn hôm sau.
- Người học góp ý: khi nhắc lại câu hỏi cũ phải ghi kèm nội dung, không chỉ ghi nhãn (đã lưu vào memory).
- **Buổi sau (bắt đầu từ đây)**: nhận bài Phần B (5 câu, R2, bài tập xếp chỗ) → nhắc các phần còn nợ của Phần A (5 câu kiểm tra, bảng BT3 đầy đủ, tóm tắt R1) → Phần C (phân tích nghiệp vụ).

