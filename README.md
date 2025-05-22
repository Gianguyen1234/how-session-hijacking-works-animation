# Session Hijacking – Hiểu và nhận biết tấn công chiếm quyền phiên làm việc

## Tutorial: https://youtu.be/NY60Ddwn1RA
## Document: https://harrypage.hashnode.dev/
## Session là gì?

Khi bạn đăng nhập vào một website (ví dụ: Facebook, Gmail), hệ thống sẽ tạo ra một **phiên làm việc** (gọi là *session*) để ghi nhớ bạn là ai. Thay vì bắt bạn nhập mật khẩu ở mỗi trang, website sẽ gán cho trình duyệt của bạn một **Session ID** – giống như một chiếc thẻ ra vào.

Miễn là bạn còn giữ thẻ đó, bạn được xem như người dùng đã xác thực.

## Vậy Session Hijacking là gì?

**Session Hijacking** là cách mà kẻ xấu chiếm lấy "thẻ ra vào" của bạn – tức là Session ID – rồi dùng nó để truy cập vào tài khoản của bạn, mà không cần biết mật khẩu.

Nói đơn giản: bạn login, hacker lấy được session, và giờ hắn trở thành "bạn" trong mắt hệ thống.

## Hacker lấy Session ID bằng cách nào?

Có nhiều cách khác nhau, nhưng đây là một số kiểu phổ biến:

### 1. **Nghe trộm (Session Sniffing)**  
Nếu bạn dùng mạng Wi-Fi công cộng (không an toàn), hacker có thể bắt gói tin và xem được dữ liệu chưa mã hóa, bao gồm cả Session ID.

### 2. **Chèn mã độc (XSS)**  
Hacker chèn mã JavaScript vào trang web bạn truy cập (nếu web bị lỗi bảo mật). Mã này có thể lấy cookie chứa Session ID và gửi về cho hacker.

### 3. **Gài trước Session (Session Fixation)**  
Hacker tạo sẵn một Session ID và dụ bạn đăng nhập bằng session đó (thường qua link). Sau khi bạn đăng nhập, hacker đã có session đó trong tay.

### 4. **Chặn giữa đường (Man-in-the-Middle)**  
Hacker chen ngang giữa bạn và server. Nếu kết nối không được mã hóa (không dùng HTTPS), mọi thứ gửi đi có thể bị chặn lại và đọc được.

## Chuyện gì xảy ra sau đó?

1. Bạn đăng nhập → trình duyệt nhận Session ID.
2. Hacker lấy được Session ID.
3. Hacker gửi request tới website, đính kèm Session ID đó.
4. Website tưởng hacker là bạn → cho phép truy cập.

Hacker giờ có thể:
- Đọc tin nhắn, email.
- Gửi yêu cầu thay đổi mật khẩu.
- Truy cập thông tin nhạy cảm.
- Nếu là tài khoản admin: phá hoại toàn hệ thống.

## Làm sao để phòng tránh?

Đây là những cách giúp bảo vệ bạn và hệ thống khỏi Session Hijacking:

- **Luôn dùng HTTPS.** Đừng bao giờ đăng nhập trên website không có ổ khóa (🔒).
- **Cookie an toàn.** Website nên gắn cờ `HttpOnly`, `Secure` cho cookie.
- **Tự động đăng xuất sau thời gian không hoạt động.**
- **Thay đổi Session ID sau khi đăng nhập.**
- **Phát hiện hoạt động lạ**, ví dụ: nếu Session ID cũ mà IP hoặc trình duyệt đổi đột ngột → nên chặn.

## Animation này giúp bạn thấy rõ:

- Cách session được tạo ra.
- Hacker đánh cắp session bằng kỹ thuật cụ thể.
- Hacker đăng nhập thành công mà không cần mật khẩu.

> Đây là kiến thức nền tảng trong bảo mật web – nếu bạn làm web, học bảo mật, hoặc đơn giản chỉ muốn bảo vệ tài khoản cá nhân, hãy hiểu rõ cách session hoạt động và cách nó bị tấn công.
