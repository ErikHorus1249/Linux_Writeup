9/5/2021
# Tìm hiểu và sử dụng Proxychains và Tor network

**Lời nói đầu**
Nếu bạn là người không thích bị soi mói mỗi khi lượn lờ đâu đó trên mạng . Đặc biệt nếu bạn là một người thích vọoc tấn công hoặc kiểm thử thì sử dụng VPN hay proxy là điều kiện tiên quyết. Bài viết này sẽ trình bày cách ẩn danh khá ổn khi bạn làm những điều mờ ám. 
## I. Proxy chaining là ?
**Web proxy chaining** là một cấu hình mà ở đó một proxy server (được gọi là **downstream proxy server**) được cấu hình để chuyển tiếp các yêu cầu đến một proxy server khác (được gọi là **upstream proxy server**) thay vì lấy lại các nội dung trực tiếp từ Internet. Nó giống như mội chuỗi các mắt xích liên kết với nhau tạo ra một kết nối trung gian giữa máy client và server.

![](https://i.imgur.com/x1YE6bw.png)

Để thực nghiệm bài hướng dẫn này tác giả sử dụng ứng dụng có sẵn trong kho lưu trữ của Ubuntu hoặc Debian là **Proxychains**

![](https://i.imgur.com/rOtwDQB.png)
Một công cụ mã nguồn mở được cộng đồng đông đảo đóng góp phát triển. 
## II. Tor network
**Tor network** là một mạng lưới được phát triển bởi hải quân Mỹ. Còn bây giờ thì nó trở thành một tổ chức phi lợi nhuận chuyên nghiên cứu các công nghệ bảo mật. Nó giúp che giấu danh tính của người dùng bằng cách hướng tất cả các truy cập của họ qua các hệ thống máy chủ. Tại đây dữ liệu sẽ được mã hoá hoàn toàn và không thể dịch ngược. Qua đó sẽ không thể lần ngược lại dấu vết của người dùng.
![](https://i.imgur.com/ifY8Tqp.png)

## III. Hướng dẫn sử dụng trước khi dùng
- **Khuyến cáo:** hướng dẫn này nhằm mục đích học tập không phải cho mục đích cổ xúy tấn công bất hợp pháp.
- **Đối tượng :** dành cho tất cả những ai có đam mê mạnh mẽ với ẩn thân chi thuật tuy nhiên tốc độ khi truy cập sẽ khá chậm so với việc sử dụng VPN nguyên nhân rất đơn giản vì Tor sử dụng các node kết nốt với nhau khá lớn và phức tạp dẫn đến tốc độ vận chuyển gói tin của bạn sẽ bị hạn chế và đặc biệt khi bạn sử dụng phương pháp này thì các dịch vụ stream sẽ bị ảnh hưởng lướn hoặc không thể cung cấp.
- **Chuẩn bị :**
	- Máy tính chạy hệ điều hành Linux (tất nhiên rồi vì đây là linux write up)
	- Đảm bảo nhà mạng của bạn cung cấp dịch vụ tốt vì nếu mạng bạn sẵn đã chậm thì không nên dùng **proxy** hay **VPN** làm gì đặc biệt khi nó dính đến **TOR**.
- Thực nghiệm:
**Bước 1 : Cập nhật và cài đặt Proxychains** 
Update toàn bộ các kho ứng dụng cũng như cài đặt tất cả những gì còn tồn dư trên máy.

>     $ sudo apt update -y
>     $ sudo apt upgrade -y

Bạn có hai tùy chọn là cài đặt qua source code tại github hoặc cài đặt gói sẵn trong kho. Tác giả sẽ thực hiện các dễ dàng hơn.
chạy lệnh sau để cài :

> `$ sudo apt install proxychains tor -y`

![](https://i.imgur.com/glc2M39.jpg)

**Bước 2 : Cấu hình**
Tại bước này cần thực hiện thay đổi các tùy chọn trong file config của Proxychains.

    

> `$ sudo vim /etc/proxychains.conf`

![](https://i.imgur.com/DkKK1B5.jpg)
- Bỏ phần comment của **dynamic_chain**, mỗi kết nối sẽ được thực hiện qua chuỗi proxies, các proxies sẽ được kết nối theo thứ tự trong file config. Cần ít nhất 1 proxy online với config này, và các proxy lỗi sẽ được bỏ qua.
- Comment lại phần **strict_chain** nếu không vô hiệu hóa nó thì khi chạy sẽ gây lỗi bởi vì tuỳ chọn này bắt buộc tất cả proxies trong danh sách phải online. Tức là một proxy không hoạt động thì chain sẽ đứt và không thể kết nối tới mục tiêu.

![](https://i.imgur.com/U5vAqan.jpg)
Ngoài ra có thể thêm dòng 

> Socks5 127.0.0.1 9095

 để có thể sử dụng cả giao thức UDP cho giao tiếp vì Socks4 chỉ hỗ trợ TCP.
## Bước 3 : Chạy và nghiệm thu
Dùng lệnh **systemctl** để chạy dịch vụ Tor 

> `$ sudo systemctl start tor.service`

![](https://i.imgur.com/BLyY1en.jpg)

Dùng lệnh sau để chạy **Proxychains** với mọi lệnh trên terminal.

> `$ proxychains <nameoftool>`

Ví dụ chạy **firefox** với proxychains:

> `$ proxychains firefox google.com`

Vị trí truy cập của tác giải khi kiểm tra tại whatismyip.com khi chưa dùng proxy.

![](https://i.imgur.com/yNyiFoK.jpg)

Kết quả sau khi dùng proxychains + Tor.

![](https://i.imgur.com/tH6sMGf.jpg)

## Kết luận
Còn rất nhiều phương thức và phương pháp ẩn danh khi ở trong không gian mạng nhưng đây chỉ là một trong những phương pháp đó, còn nhiều điều cần phải học hỏi và tìm hiểu thêm. Chúc bạn lao động và học tập hiệu quả.
## reference
**[Quản trị mạng](https://quantrimang.com/cau-hinh-web-proxy-chaining-trong-forefront-tmg-2010-%E2%80%93-phan-1-70884)**
**[Sbin.xyz](https://sbin.xyz/2017/12/20/chay-ung-dung-qua-nhieu-proxy-hoac-tor-voi-proxychain/)**
[**HackerSploit**](https://hackersploit.org/)
