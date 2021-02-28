by ErikHorus
date 27/02/2021
# Điều gì làm nên khác biệt giữa apt và apt-get

## I. Lời nói đầu

Trong quá trình sử dụng linux nói chung và các distro "nhà" Debian nói riêng thì việc nhập môn với chúng bắt đầu từ khoảnh khắc bạn update  lần đấu tiên và câu lệnh sơ khai mà các trang tutorial bắt bạn sử dụng là :

    $ sudo apt-get update -y 
Và rồi việc sử dụng chúng nhiều đến nỗi phát phiền (toi khuyên bạn nên thêm vào shell của bạn dòng sau đây 
`alias up="echo [root_passwpord] | sudo -S apt-get update -y | sudo apt-get upgrade -y"` )

Đôi khi bạn type có mỗi **apt** thay vì **apt-get**  mà nó vẫn chạy ngon lành, từ đó bạn mường tượng rằng chúng ắt hẳn là một  và không có gì đáng suy tư ở đây cả.
Tuy nhiên đằng sau sự khác bọt nhỏ nhoi này nó là cả "đống " tâm huyết từ đội ngũ phát triển của Debian. Băt đầu đi tản mạn nào .
## II. Nguồn gốc và sức mạnh của lệnh apt
### 1. APT, apt-get và apt-cache
Từ đầu ta phải phân biệt rõ ràng thế này **apt** chúng ta đang đề cấp đến khác vơi **[APT](https://vi.wikipedia.org/wiki/Advanced_Packaging_Tool)** (Advanced Packaging Tool). Về bản chất **APT** là một bộ công cụ (["APT is a set of tools"](https://en.admininfo.info/diferencia-entre-apt-y-apt-get-en-linux)) đảm nhiệm **quản lý** mọi tác vụ liên quan đến **gói ứng dụng** (package) cho **[Debian](https://en.wikipedia.org/wiki/Debian)** và các thế hệ **[OS](https://en.wikipedia.org/wiki/Operating_system)** con cháu của nó như **Ubuntu**, **Mint** . . .
Có thể thấy bộ tool này cũng khá đa dạng nhưng đó cũng là một hạn chế vì cái gì nhiều quá cũng không tốt (chém thôi chứ tính năng nó thế rồi người ta cũng không thêm gì thừa thãi cả ) tuy nhiên điều này dẫn đến tình trạng không thân thiện với người dùng mới hoặc dân chơi làng lướt tọc mạch cho vui.

![](https://i.imgur.com/Y7ZndpR.png)
##### H1.1.Lệnh apt-get và apt-cache

Điểm qua cũng kha khá về số lượng các lệnh với hai đối tượng apt-get và apt-cache

![](https://i.imgur.com/9Xry3ND.png)
##### H1.2.Lệnh apt-get và apt-cache trong các trường hợp cụ thể
> Bạn thấy đấy, những lệnh này chúng có rất nhiều chức năng mà có lẽ
> người dùng Linux trung bình chưa bao giờ sử dụng. Mặt khác, các lệnh
> quản lý gói được sử dụng phổ biến nhất nằm rải rác trên **apt-get** và
> **apt-cache**.
### 2. Command-line apt 
![](https://i.imgur.com/8ZXXIJh.png)
##### H1.3.Linux Mint forums

Quay về quá khứ,  Từ việc triển khai một **[Python wrapper](https://www.geeksforgeeks.org/function-wrappers-in-python/)** tên gọi **apt** với chức năng được tích hợp từ hai lệnh cơ bản là **apt-get** và **apt-cache** đồng thời các tùy chọn chọn thân thiện hơn rất nhiều sao với hai lệnh cũ mà từ này đã được sử dụng rộng rãi trong cộng đồng Linux Mint. Tuy nhiên,  wrapper vs cái tên sơ khai này có cùng một tính năng với apt hiện tại nhưng bản chất của chúng thì lại không giống nhau. Tại sao ư ? Hãy đọc thêm về **[Function wrapper and python decorator](https://amaral.northwestern.edu/blog/function-wrapper-and-python-decorator)**

![](https://i.imgur.com/qWQ24RQ.png)
##### H1.4.Cap vui vui thôi 
Như bạn thấy đấy apt hiện tại chạy đâu cần có Python đâu, ngày mà nó mới xuất hiện nó là một wrapper python nên phụ thuộc vào Python để chạy là điều dễ hiểu.

![](https://i.imgur.com/x7vgqc0.png)
##### H1.5.Sinh nhật của apt command the [wiki](https://en.wikipedia.org/wiki/Ubuntu_version_history#:~:text=Ubuntu%2016.04%20LTS%20%28Xenial%20Xerus%29,-Ubuntu%2016.04%20LTS&text=Shuttleworth%20announced%20on%2021%20October,released%20on%2021%20April%202016.)

Ở hiện tại, **apt**(loại không phải dùng caps lock ấy) là một lệnh (command) trong hệ thống lệnh của hệ điều hành nhân linux họ Debian và chỉ xuất hiện chính thức năm 2016. Mô tả cụ thể của nó đây :

> `apt` is a command-line utility for installing, updating, removing,
> and otherwise managing deb packages on Ubuntu, Debian, and related
> Linux distributions
> 
Nếu khả năng dịch của bạn cũng sương sương thì hiểu đơn giản thôi còn nếu cần dùng Google Translate thì thôi "Khỏi" ngắn gọn sẽ là một lệnh cho cài đặt, cập nhật, xóa và quản lý các gói .**[**deb**](https://vi.wikipedia.org/wiki/Deb)** trên các distro Debian, Ubuntu . . .
> 
> Túm cái váy lại,  lệnh apt có thể thực hiện các chức năng thiết yếu và
> tập hợp thành một câu lệnh với chác option ngắn gọn và thân thiện chứ
> không rải rác chức năng trên hai lệnh apt-get và apt-cache nữa.
>  **_apt=most common used command options from apt-get and apt-cache._**
>  
Và tất nhiên là nó còn một số tính năng hay ho mà ta sẽ tìm hiểu ngay sau đây .
### 3. Khác bọt giữ apt và apt-get
+ Bạn có thể xem thanh tiến trình trong khi cài đặt hoặc gỡ bỏ một chương trình trong apt.

![](https://i.imgur.com/Rb5lmFL.png)
##### H1.6.Thanh tiến trình khi sử dụng apt

+ apt cũng nhắc bạn về số lượng gói có thể được nâng cấp khi bạn cập nhật cơ sở dữ liệu kho lưu trữ.

![](https://i.imgur.com/GWpn4d3.png)
##### H1.7.Thông tin các gói upgrade
> Mặc dù apt có một số tùy chọn lệnh tương tự như apt-get, nhưng nó
> không tương thích ngược với apt-get. Điều đó có nghĩa là nó sẽ không
> hẳn hoạt động nếu bạn chỉ thay thế phần apt-get của lệnh apt-get bằng
> apt.
> 
Hãy xem lệnh apt nào thay thế các tùy chọn lệnh apt-get và apt-cache nào.

![](https://i.imgur.com/ZGErWrf.png)
##### H1.8.Bảng thống kê lệnh giữa apt và apt-get theo itsfoss

apt cũng có một số lệnh của riêng nó.

![](https://i.imgur.com/AOdcOuz.png)
##### H1.9.Bảng thống kê lệnh  riêng của apt theo itsfoss

## III. Kết luận 

Khi Debian nói "pleasant for end users", nó thực sự có nghĩa là như vậy không giống "WindowN". Lệnh apt có ít tùy chọn hơn nhưng đầy đủ theo cách có tổ chức hơn. Trên hết, nó cho phép một số tùy chọn theo mặc định thực sự hữu ích cho người dùng cuối. apt sinh ra trong một thế giới kỳ lạ - miền đất cộng sản của thế giới công nghệ với cái tên  **open source**  nơi phong trào Free software khởi phát mạnh mẽ, cũng là thiên đường cho tự do vì sự phát triển chung của cộng đồng mà không bị giàng buộc bởi giá trị lợi ích **thương mại** nào.

Do tính tiện dụng của nó nên các distro dần học hỏi nhau và đưa nó vào hệ thống lệnh của mình. Giờ đây các distro  nền tảng từ Debian đều đã cập nhật nó như một phần không thể thiếu. Tuy nhiên apt-get và các tool còn lại vẫn tiếp tục vòng đời của mình vì tính hữu dụng, sự phổ biến của **apt** không có nghĩa là cái chết cho chúng.

![](https://i.imgur.com/FiB3Jb5.jpg)
##### H1.10. My idol Richard Stallman
### Reference :
- **[Itfoss](https://itsfoss.com/apt-vs-apt-get-difference/)**
- **[Linux Mint forums](https://forums.linuxmint.com/viewtopic.php?t=259891)** 
- **[Wikipedia](https://vi.wikipedia.org/wiki/Wikipedia)**
- **[Geekfogeeks](https://www.geeksforgeeks.org/function-wrappers-in-python/)**
- **[Linuxize](https://linuxize.com/post/how-to-use-apt-command/)**
