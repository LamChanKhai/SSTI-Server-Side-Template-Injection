### Phần 2: Triển khai tấn công SSTI
Nối tiếp phần 1, bài này sẽ tiếp tục với ```SSTI```
## Các bước triển khai tấn công SSTI.
Dựa vào ```portswigger```, mình sẽ chia phần này thành 3 giai đoạn, __detect__(_Phát hiện_), __identify__(_Xác định_) và __exploit__(_Khai thác_).
<p align="center">
  <img src="https://dummytip.com/wp-content/uploads/2022/08/1-SSTI-attack-steps.png" width="300"> 
</p>

# Detect

<p align="left">
  <img src="./images/iknow-whatkind.gif" width="150"> 
</p>

~~"_Tôi biết trang web đang bị __SSTI__ nhưng không thể chứng minh_"~~

Như bất kì lỗ hỏng nào khác, để khai thác được ```SSTI``` ta cần phát hiện ra nó. Phương pháp được dùng nhiều là ```fuzzing```. Với các dữ liệu từ người dùng như:
- Các trường trong __header__ của request( ví dụ: ```User-Agent```, ```Referer```,...).
- Tham số từ ```url request```( /?thamso1= ,...).
- Các trường dữ liệu được gửi qua form.
Ta thử thêm chuỗi các ký tự đặc biệt thường được sử dụng trong các biểu thức __template__, chẳng hạn như ```$ {{<%[%'"}}%```. Nếu xảy ra ```exception```, điều này cho thấy cú pháp __template__ được chèn vào đã được server diễn giải. Đây là một dấu hiệu cho thấy ```SSTI``` có thể tồn tại.

Nếu bạn đang làm 1 bài CTF whitebox thì mọi chuyện sẽ đơn giản hơn, khi đọc source code nếu phát hiện ```untrusted data``` được nối chuỗi trực tiếp vào __template__ thì đó chính xác là nơi mà chúng ta sẽ khai thác.

# Identify

Sau  khi xác định được web dính ```SSTI```, vẫn còn 1 bước cần làm trước khi khai thác là xác định xem trang web đang dùng ```template engine``` nào. Với các ngôn ngữ khác nhau lại có ```template engine``` khác nhau nên số lượng ```template engine``` khá lớn, và mỗi ```template engine``` lại có __syntax__ khác nhau nên ta cần xác định đúng ```template engine```, nhưng nhìn chung tụi nó lại khá tương đồng về mặt __syntax__.



