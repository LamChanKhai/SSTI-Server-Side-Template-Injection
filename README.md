# SSTI-Server-Side-Template-Injection
## SSTI là gì?
Để hiểu được SSTI là gì, chúng ta cần biết template là gì? Mình sẽ giải thích qua một ví dụ:

Hãy giả sử bạn ứng tuyển vào một công ty và công ty đó có sẵn hàng loạt mẫu đơn tuyển dụng, ứng viên chỉ cần lấy và điền thông tin vào đơn. 

<p align="center">
  <img src="./donmau" width="700">
</p>
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

Để hệ thống thay các placeholder trong template bằng dữ liệu thì cần có một thứ gọi là **Engine**. **Engine** này đóng vai trò tổng hợp các yếu tố cố định trên template với các dữ liệu được đưa vào tại thời điểm đó để render ra phiên bản web page tương ứng. Ở ngoài kia có rất nhiều **Template Engine** tùy thuộc vào ngôn ngữ mà web sử dụng ví dụ như ``` Jinja2 (Python), Twig (PHP), Velocity (Java) ```.
Vậy SSTI là gì? Như cái tên của nó, đây là một lỗi ```Injection```, chúng ta sẽ tiêm payload độc hại và nó sẽ được xữ lý ở ~~Server-Side~~ phía server và sau khi engine render template có thể sinh ra những kết quả không mong muốn. Trong đa số trường hợp xảy ra lỗ hổng **SSTI** đều mang lại các hậu quả to lớn cho server, bởi các payload SSTI được thực thi trực tiếp tại server và thường dẫn tới tấn công thực thi mã nguồn tùy ý từ xa ```(RCE - Remote Code Execution)```.

