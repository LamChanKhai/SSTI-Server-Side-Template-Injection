# SSTI-Server-Side-Template-Injection
## SSTI là gì?
Để hiểu được SSTI là gì, chúng ta cần biết template là gì? Mình sẽ giải thích qua một ví dụ:

Hãy giả sử bạn ứng tuyển vào một công ty và công ty đó có sẵn hàng loạt mẫu đơn tuyển dụng, ứng viên chỉ cần lấy và điền thông tin vào đơn. 

Họ và tên: __________

Email: __________

Vị trí ứng tuyển: __________

Giới thiệu bản thân (ghi trong khung): ______________________

Template giống như tờ đơn in sẵn: có khung, tiêu đề, chỗ điền; phần cố định do người soạn in sẵn, phần biến đổi là chỗ người dùng điền.

Trên web, template có thể là mã HTML, có các tiêu đề (mình sẽ gọi cái này là các yếu tố cố định trên template) và có placeholder (ví dụ bên dưới) để sau đó hệ thống điền dữ liệu để thay thế các placeholder này. 

```html
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>Ví dụ Template</title>
</head>
<body>
  <h1>Xin chào {{ name }}</h1>
  <p>Email của bạn là: {{ email }}</p>
  <p>Vị trí ứng tuyển: {{ position }}</p>
</body>
</html>
```

Để hệ thống thay các placeholder trong template bằng dữ liệu thì cần có một thứ gọi là engine. Engine này đóng vai trò tổng hợp các yếu tố cố định trên template với các dữ liệu được đưa vào tại thời điểm đó để render ra phiên bản web page tương ứng.

