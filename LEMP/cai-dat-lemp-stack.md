##Hướng dẫn cài đặt LEMP Stack trên Ubuntu 20

> LEMP là viết tắt của Linux, Nginx (Engine x), MySQL và PHP, và đây là một trong những biến thể của web server.

> Lưu ý: Bài viết chỉ giúp mọi người cài đặt và chạy được với PHP,  sẽ không giải thích sâu vào từng thành phần của LEMP. Nếu các bạn muốn mình viết sâu hơn về phần này thì hãy comment để cho mình biết và thực hiện sớm nhất.

> Trước khi làm các bạn có thể đọc trước về các sử dụng command phổ biến cho linux hoặc ubuntu, các sử dụng nano editor hoặc vim.

#####Bước 1: Cập nhật và nâng cấp các gói có sẵn và đã cũ trong hệ thống bằng câu lệnh sau:
> sudo apt-get update && sudo apt-get upgrade -y

Câu lệnh trên giúp chúng ta cập nhật các gói(package) có sãn trong hệ thống nằm trong file có đường dẫn: `/etc/scources.list`, `-y` ở cuối câu dùng chấp nhận các package cần thiết khi update và nâng cấp được đề xuất.
**Lưu ý**: Phải chạy câu lệnh update trước câu lệnh nâng cấp upgrade vì update được sử dụng để đồng bộ hoá lại các index file từ các nguồn từ `/etc/scources.list`.
#####Bước 2: Cài đặt Nginx.
- Nginx hiện tại là một máy chủ được sử dùng từ web nhỏ cho tới web siêu lớn vì hiệu năng mà nó mang lại.

Sau cập nhật và năng cấp các gói trong hệ thống ta bắt đầu chạy câu lệnh cài đặt Nginx:
> sudo apt-get install nginx -y

**Lưu ý:** Nếu hệ thống yêu cầu nhập mật khẩu thì bạn hãy nhập mật khâu, và mật khẩu khi nhập ở màn hình command sẽ không hiện `******` chỉ cẩn nhập xong là nhất Enter.
Sau khi cài đặt xong chạy tiếp câu lệnh:
> sudo nginx -v
nginx version: nginx/1.18.0 (Ubuntu)

Nếu hiện dòng `nginx version: nginx/1.18.0 (Ubuntu)` thì bạn đã cài đặt thành công với `1.18.0` là phiên bản bạn đang sử dụng.

Tiếp theo sẽ là cấu hình tường lửa:

Cài đặt tường lửa để đảm bảo tính bảo mật và cho phép lưu lượng truy cập qua các cổng mặc định, thông thường các web sẽ sử dụng 2 giao thức HTTP & HTTPS tương đương với cổng 80 & 443.

Chạy 2 câu lệnh sau:

>sudo ufw allow http
sudo ufw allow https

![image-ufw](https://lh3.googleusercontent.com/nnc4sKmCMbNhT1KJLcjsg-QJtbj0Iz7vzh7phbHfeSeJnosNSWlKxlcRWRBO7bPoMf0VAl9AoSRH4oK87NheMYtLRy2GlmAhBNZNWdneXzxZPZilzSpLnV_V4X4Ss3UwyGWiJ2FeYSHGHl5TsEMlWQcZUrjFP8neP_pCBQqSEuDRBKNxuYRQv1PRHokNXE1Yvh7uy9-ant6T8hf46T1vw__rgmu0tTM64shB9nMO0B4BVtrIAJsmRsE8brNFXF3mcZ7lQBqNoKx2Hy36wi1Sy0Rp96Ni5GwFfYaU3iuBT6dKyWOAkVe1FXhfqg7jI4oKQcxyR6_y3LjvvYqUmUp76WLJdiDtu_z4UULpqMXdGBExxf9IMnE1CYzKeLUO7GtQn-4ADU8O5_jrrxCMBZlTGkgknF4cFfWd1KfyC4zFmZig4rswG6yHKYzzee8651E8gBbM8rviY8LBkDAD0J4V68OOicPIt8InSKTsyoNKegYSCGSQQB1fEPYh-8JExc58hHhtMz6bSWLxu511aItK83mB6Q-MMZEmimpgPQaV9NFbv7SqI9mF35GalXMBcvMIYIBI02_E5IafnotPCjVwlIUi9O4nBwKcxLu0VyJEvmBGRBSGEcByVNRVRJml_Cds09c3EKWhVT64G1d5aQ5D-rq3n8ZZ8KOP8Os_uqFlTMxzr-FqVjtkmqosrJ_ElPCPNYzl2QnViGgRtQuFnCLNgX-V=w1450-h288-no?authuser=1)

Chạy câu lệnh:
> sudo systemctl status nginx.service

![status nginx done](https://lh3.googleusercontent.com/pw/AM-JKLXeWPV9PMM57-7bZ0XiMM04e2zbMDgfm45Nd9Ens5IRP3N94XU3UEOAFxRTviPjxXSB8AOo1Ojh5n02jdbFovyKqv_vrpcth7PNliLDjfw_UTRS83ejFvnhHgGioUEKezvtIUpwoG2-_1U74sON9nGv=w1480-h627-no?authuser=0)

Dòng `Active: active (running)` là đã chạy.

Nếu bạn chạy câu lệnh trên màn hình command hiện như sau:
![status-nginx-fail](https://lh3.googleusercontent.com/7Mva8KpzCY88ywHaFtY4gK1hrniBozzEsRGG492XqH69DH60SHiy6gMzZbr5Wo_NWdD4tLf7symLPzKg_xQTm_GOAp2aop4RfYS8J21FnVf9jhPjPilhn1MceZoDYqi0GLu7AiIaUXSSe3XQuTKKkKvCCOoc8Bh4QzrrRMbyPKOf0SsAdnGxzUHjoVYSasnpMegpOZ2pZm6pDnoHh2RmW-bfmh5wsCAvbijhSuf8ehbzlpGYtMYXAIXS5ctlR1ECEUZbfxHSWTAIwfuYcU6k8orz_0D4RGsmL4J_HXN6YJM2UWYXudXEbhbEZgxmv2rjD3gxVrLAuShcDDhXwNBMlRPybeK9mfyYHTjFsSvjUU_7UzQUAk_G-ISPVCeZXtJpOTQdh4wuHLkGJrdkQsD5nmGfSCLPZGA3E-0u5_4xMosPjYu0YAqpMMFyllp9Exwybhach8rM8IxEEX9Bl5KQ0xLqhefXwqEn8Q9EXIK9gXtdt4jSsbLgmyr9YPxzvg5Sfx_POx7ylZ61U_lwvUzJMPpSWkHP7krtEc7JMm7vS5nYONpEAjiHCxYeDsKXrsBubLqw96fX8_N9JnTIK5yZzUXTWmBNIDVZhNaFAjsanTjxjrOrtdCKUTpxS4DkEdAXdlmf38rAKS4QzMDPuSzLCTRhMKEDTbiA8xOG-_CrD68JXXesSbr7mVuIWgBXW_fHAXbNoY5nOEt_HICThHrP49ZA=w1471-h490-no?authuser=1)
Dòng `Active: active (dead)` là chưa chạy.
Như vậy là Nginx chưa được chạy.
Bạn hãy chạy câu lệnh:
> sudo systemctl star nginx.service

Sau đó chạy tiếp câu lệnh:
> sudo systemctl enable nginx.service

Cho phép Nginx khởi động cùng hệ thống.
![status nginx](https://lh3.googleusercontent.com/7jBRQ0nmLupvXKQUCe7zAEqQzO3F_-LQ0nh2QnSD07Kn-5ZXsCLoCoaqbG-bXwfl23ULSMh4yDoTJO3_0SRXlpTCntygL7hc_7zUgF5PT7w2E_zZnkkO8xNL6RlXtHl_8RwW6inTozyN50br7l_JQCn28_FVBnH9h8iNaBr4yaB6-0ZRHLy_NoUb4YjwacVOK8lAvzpv9BUHqKTuGKSf-dJIs5FXXQvZV-adXCL9pg3RuIJX4VDN1vBKu7L-p6nCDM2f5t2bSHBCau-6FWwBJQl6jh1mVGc3jl3EknTAVKqw6eSZiRIvRVYIqa-v8Q2memDtE4CSzaNJsa9xjeV8uZ85VO6KJNtYlXVfdUnLhqgTBpEGFnMJAL6BcjzYpDaoj1T4uHzR6343z0TxIS7-b0b97Zoe6Qdw8fmuNjFPUfS6IHt8f8rzcoFFFD3iV2b2y7DOONSgx-zpjggqnhv7FlIKvXwGv9RGbzeecbZ3Y33smHxh8F1N9WOlrfuYkAI5GPNTxw221giiGyp1BWMPJDbHicHd2kXIOWYqvuw65cpgHne6StgoQIgCkVMFx9FlvDHsvcGDDNk6yNj0rAsqt6PaVRbr3y_TT7egQLqAU04cQGRlp40ZXRX54pZm2xjz-cczUGkkhF7dHfp82PEcEsAHoNH9kF8hLwX6Q_XJ5IwydSaACG7Tatw5tzSOXdWjQwxjQvkvM8n9kGUHNyzK98dh=w1462-h170-no?authuser=1)

Giờ bạn mở trình duyệt lên và gõ [http://locahost](http://locahost)


![image-localhost](https://lh3.googleusercontent.com/qvJ1gb52lwBylHzAW-XR_SGwwxyi8RxTnb5hQLRHkn7RGTs9QkvlKJ9AfA1DwAp6cc1udAjXgwZwGPUZoIVmzuM2tyr1etANeyL4kEtTUSOdVjHQNtFLk4sA54KInnSY7OmgmlpoS1FgkdzG1krHRySt6j9wD1iEU6a8LHWREcQnTgIGaXwkHX-79czJ0vbI_b5QntpHqgax0hQdJYAD_bBeP85DAiZXUdFohbVymIK5rqO13u_Br0rMkHFqrEfGZZC4e-zZ664NgVKw6BWgtfHOINKABtEqZbyKPXy6SFiCOR9EusEXUc8vsnWE42aip9GToDRCnCuGJrzUqdBckJuBXU00uma_YkSNDfUBWqFYafaE1S94DPayYnWVYCxuSnJwanOE_7S2gTMuarq2dNXnY7l7p6mlTbhgnl50_mJduqlPUdclHc71_65HVqRC7jCVucFJ7dDccf6AMC9l7QDBN0E9fZ8Ow5mtxaCkUmXPsYjqdmI09EZf6cFDpGX00XF408sa8L2ccRB7xfGluz1lqcCnHBDZdovTXBQZpHZ2Dqzybz8zNg0g3NvBBWZkykjtnlwN1Lb9xOr9DOzzEt7EUlv32a-mAXmIERmgPUe8vGjzVtvAP5uE7LIPh7XY8CQgazbOmz9co8DlvJ14BZFsUVxUUCYLUuEnVxPY4RhnlphOG5TXODZg4QISON3-b-DCgciPF3qSInFMzaZDcr8v=w2298-h1466-no?authuser=1)

Như vậy là Nginx đã chạy thành công.
#####Bước 3: Cài đặt MySQL.

Các bạn chạy câu lệnh sau:
> sudo apt install mysql-server -y

Sau khi cài đặt xong chúng ta chạy tiện ích **mysql_secure_installation** để cấu hình bảo mật.

>sudo mysql_secure_installation

**mysql_secure_installation** sẽ giúp chúng ta cài đặt mật khẩu root MySQL, xóa người dùng ẩn danh, vô hiệu hóa Remote Mysql và xóa cơ sở dữ liệu test.

>Enter current password for root (enter for none): Nhấn Enter
Switch to unix_socket authentication [Y/n]: n
Change the root password? [Y/n]: y
New password: Mật khẩu root
Re-enter new password: Nhập lại mật khẩu root
Remove anonymous users? [Y/n]: y
Disallow root login remotely? [Y/n]: y
Remove test database and access to it? [Y/n]: y
Reload privilege tables now? [Y/n]: y

Tiếp đến các bạn truy cập vào Mysql với user root bằng lệnh:
> sudo mysql

![login-root-mysql](https://lh3.googleusercontent.com/Pts8JV3o7BSqXtIzE_6xU_-4h8B_Tndp73fLtT443Bd-fDJgu-PCNKsZOvIbOTyWisHqDPnHwYVRv66X0Y4qMICg20MfnYINdxlFgoo8lOeJ9GlUSSkg1dnc6F0zYB6Qw9FAE8ebu4BLfqO8mk6cFLlIg_I113qTZVsPkW53d91QQuXFNFSmNN--vhR1ATwCmXZwn95dyrTB7UlOOyz4GOdLx8YP7Z3PVUN4hKQTLQPGI-ZR2B-xR0rPimNtVbzM9T4T_OO3sIER5vEGED5Fpm88vK5wve7OmJJRlm8Se-UZbXPgm9BUKk0IvTJhctm5k8b8grToxs_GDtKqYUEErn0El6IockRTCqX2di2obt8cQnLmTbd_5zIPIw9UOyWx2uHSX98oIW8fNuJwKatOg4-Y1pUE-1EoUuQAwXl1zTiyzUmP3AyiFlycO6jxokXQH60BsQN1KvtILzTmWPgx0NJC4iUHE7n9Wfz2-WDeYvf11Z4i4RUsEjT8va29eMvczhcgwydDb7_N00zwlI6ZmcOSxze2A8pUqUUeyCChffoGM8OOo64ercrETy3oA5V4yDZBYzd4Gm2aBPl40As6p5_xG0HTr6H6cclzOp0wfpIipH7K7IKsjOlvhxNdvpTkNN5ehxrXO-JyBk16MemZxpL96aAHt3nS74kDolkI0cqduV3-QKjqb_hNx2h-TNKpOoJYKDpYd3Q4ye-B3uWrXKhA=w1448-h540-no?authuser=1)

Như vậy là chúng ta đã truy cập vào được MySQL.

> Từ phiên bản MySQL 5.7 trở đi, user root của MySQl có thể đăng nhập mà không cần sử dụng mật khẩu như ở trên sau khi chạy câu lệnh **mysql_secure_installation** và cấu hỉnh xong, chỉ cần chạy câu lệnh **sudo mysql** là có thể đăng nhập vào MySQL rất là tiện lợi. Nhưng khi chúng ta cần cho phép kết nối từ bên ngoài vào ví dụ như sử dụng (Navicat, phpMyAdmin v...v) truy cập sẽ phức tạp, nhất là khi cấu hình trên server và cần truy cập đến để quản lý database từ xa.

Để giải quyết vấn đề này chúng ta sẽ tạo một user mới với chức năng dùng để Remote Access đến MySQL server.

Vẫn màn hình command trong MySQL server, nếu bạn đã thoát ra thì hãy vào lại bằng `sudo mysql`.

Chạy các câu lệnh sau:

>SELECT user,authentication_string,plugin,host FROM mysql.user;

![image-show-user-mysql](https://lh3.googleusercontent.com/ttWyW1EEeEpXGJ36CFXbT2tK-NBpuOSt0D1a1jrkPQuq7H08dc9bBsUs6pcf8YWMrYfpGVw_Pwl3MJydnJl7DuVmOKfHn1Scrf5G5hr32ICN9qBaKTspYoKSKWlNlfr7RLmZH-dGgRkUUFk9BLzkO8FKwlpv_RrftNYeJuz_3ZlKJK8ArWK4JIPYuzXwHDJdoN1bt-zdluXtEmDQCRGJOcTaNWfNFSo7QTHyMMI-jLtMl7C95q0gBn_KYPsOo5lHWian9K7-84nIBOI8ln0vnYPdMN1qGyIspZ9QbW-BsC9PKbcePPWZlEq01R36y6vV3fTXUfwZGHBX3NUqy1n72DjjW9TWAv5ft5ZP8_vdW5_VsuQYjtbEOPbjmcck9F8elgTRnMdMaBs1dMQcRVWHgYYm2xosBWhDQqbhPXWEhbB2MUuTT-YCBMnbYxvVIq6xi5JL8Jl3AOyebZW3ePP_X7sAzL_Bcw2NUOYhwIqOncA-mruVUuN34-kM89_qlhmzU6wRkWBdeUpFod2aSQ89Z54ENMXwLn5TpreJKFp0PT4aXDYq4ZrcquCt4ytpxJPwdqxh-g0M5mhhPz_sWIFHDxybg4eLEV8zOvuSgL8epKIpULDoo_YzzlFkXefVfv6SOvmbjFT78fmFLfNhdAZSQ9ljOriZrnLldp4ciAZ-kGlwRmZjcFFQyBwaEIeK1fUQLga8x48PAZAMfRzz__HDyh6N=w2642-h436-no?authuser=1)

Đây là list user của mình mặc định khi cài đặt mysql sẽ có, một số bạn sẽ hơi khác chút nhưng không có vấn đề gì cả.

Câu lệnh tạo một user mới:

>CREATE USER 'user_demo1'@'%' IDENTIFIED BY 'password';

Giải thích một về kí tự **%** có ý nghĩa là chấp nhận tất các kết nội cục bộ và bên ngoài khi sử dụng user này.

Tiếp đến là cấp quyền cho người dùng có thể thao tác với tất cả các database, thêm, sửa, xóa các bảng và dữ liệu.
>GRANT ALL PRIVILEGES ON *.* TO 'user_demo1'@'%' WITH GRANT OPTION;

Chạy tiếp câu lệnh `FLUSH PRIVILEGES` để tải lại và chấp nhận các thay đổi mới.

>FLUSH PRIVILEGES;

Kiểu tra lại list user xem đã thêm mới user thành công hay chưa:

![image-them-moi-user-mysql](https://lh3.googleusercontent.com/dXc5BaSwUHtHqRNBR_Qqlo_LB8LMn7EgWYDTnb4xa5kEXHkjptT94BO6RLu2L78_NAWQirqLbRYPucg08yck_AHusWzFR63qI5cV926lu5wJcgXJgm2fPjGw7HezxlaTAiCGNLwdiR33PSUBgQKAMf1Ufp1cuCuaZX_Kq_iiN8D-LJzEDYsSzmEBCd86tITko3RmK0ogTPwu07jDTgqujCPGKiaAhViem563TdT3y3-nxURXLtXiuWhv763_LuQQIywO5qI_dbCgcKq2WPPz1x2usSTMHbgjnKep11Z7m7nVqjzRG-NzrL8FYKoFCVdxRLd2E6GUgyaqrYxehZ3IwhdzaXQyR5J82fpMClZyVJl69mlvQGrRIzDnuDLGS-InTJG2LyqAsctmXL__pH6bGLU9PK5w1DbXKDDB-9zKAqSfoWFNLzw-SdgIo12Az3_45O1Pn4lRbt0wlBoeYGeR0bYgxuYNrt5TuRlloRSpx7I_k5W7HHl5FhQCX2q_Z3FyjbrSNTim3_tUWz27d-CKsQIPAdlL-ZbeFQDvUc0NltleB1cDN3seHAUu5NuwL_gEuNxLgDucXPE3KGAQutrj36Bsb5iRsDIf6_i6e1q24PQvehZGBeAL95ck9l9B7h3GujTlBd1XLczi8-ds6w-cjMXv4287NwBD1Ns6TcYVPLZsIgP06gxCThPCADjkBWNpbEE7PiMRgsdDzBQQDCHsxKOi=w2642-h444-no?authuser=1)

Như vậy là thêm thành công, giờ bạn có thể kết nối với phpMyAdmin hoặc bằng Navicat.

#####Bước 4: Remote Access MySQL.

Nếu các bạn cài đặt cho server mysql thì sẽ cần phải kết nối từ bên ngoài vào để quản lý và thêm sửa xóa dữ liệu cho mysql. Nhưng hiện tại khi cài đặt xong chúng ta không thẻ kết nối đến được, vì mặt định mysql khi cài đặt xong trong file cấu hình `mysqld.cnf` sẽ cấu hình mysql kết nối cục bộ, các kết nối đến từ bên ngoài với `user_demo1 ` sẽ không thể kết nối đến được. Vì vậy sẽ cần phải truy cập đến file `mysqld.cnf` để chỉnh sửa cho mysql nhận kết nối từ bên ngoài.
Chạy câu lệnh sau:
> sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf

Tìm dòng `bind-address`, mặc định sẽ là `bind-addrss = 127.0.0.1` các bạn hãy đổi `127.0.0.1 = 0.0.0.0` để nhận tất cả các kết nối từ cục bộ đến bên ngoài. Nếu trong file `mysqld.conf` của bạn không có dòng `bind-address` thì hãy tự thêm vào.
 Sau đó nhấn các tổ hợp phím sau: `Ctrl + X, Y, Enter` với nano để lưu thay đổi.

 Sau đó restarr lại mysql để chấp nhận thay đổi mới.

 > sudo systemctl restart mysql


**Lưu ý:** feild host: <input> nếu là ubuntu destop sẽ điều là localhost-127.0.0.1, nếu là server sẽ điền là IP host vd: 34.344.12.33.

#####Bước 5: Cài đặt đặt PHP.

Trong bài viết này mình sẽ cài phiên bản 8.0 của PHP.

>sudo add-apt-repository ppa:ondrej/php -y

Các gói cần thiết để chạy 1 project PHP.

>sudo apt install -y php8.0 php8.0-fpm php8.0-mysql php8.0-curl php8.0-json php8.0-cgi php8.0-xsl php8.0-mbstring php8.0-opcache php8.0-gd php8.0-pgsql php8.0-intl php8.0-bcmath php8.0-soap

Sau khi cài đặt hoàn tất hãy khởi động php8.0-fpm.

>sudo systemctl start php8.0-fpm

Cho phép chạy khi cùng hệ thống.

>sudo systemctl enable php8.0-fpm

![enable-php8.0-fpm](https://lh3.googleusercontent.com/JXTc4BHlkIHybSdX23Ae-PA9sPu92R2SDBCW2JkoGVXYEPk9qwcYnD0hN1DGSZ7oifMAqTBJQhE_pN-_ymS9488u-o8j6c70ANSRIuPDXETIN_8iCEos10-xuUq5JwM09wvIIe4rSvYJGT9FW8L4veQaORiVNisjIWoIL8XJygZA70yFsyuUNmSslOy-mtgZKQVPc1A8jSX9WkQBeTIi_6FuMjdP22hfkD2t2l2ej1Ro5MoZMasVm97L4ZxP_e5F0f5uKkVxniGjT_VpGFm9Z6qOEjpX6j3eiNc2zlH4UIByeQj0rR4v75XS6L9hbzzX15ruhZqSfdwdCBv3ycNJkfBm4g5-9d6AbxSxVBWKuGvBt5P0_nv56gaR26EcXOUATPGicOKCBu0JGoKDm96MfNxEEtsfU5ZfvYPY0HOCAJDv6z8PKhlxsqOS3VDPkKz0kv4q_AInvNkYSRyGD1r8EAaaBCAPTRqL1Dv0bBxK1KvL8R8XtTWgaW6guNYJDo0rVuo4PchoclupmbqeYQf84nkNcpCmvBRWeY2TWFz4R7obNOXZE9WpE9SW6KeIK0rzCcpxqB-tSwaFz4wRf3G5546Oq48X5Tf5ZTefoVNn7GyibrbstnyhNdWK7kqIWNhBJRfJlBwsMg22fbCEMtqJYTFDVkF6ynMO3BsRnWrK9NgLFyGCrrJvAS060JqHX-mKCSm3qiiKHqZid_GgV9h0FV1q=w3214-h158-no?authuser=1)
Kiểm tra trạng thái của php-fpm có hoạt động không.

>sudo systemctl status php8.0-fpm

![statusphp8.0-fpm](https://lh3.googleusercontent.com/zAx-OPPbWVfk-89O4Z_GCsJZ2dJM0v85Y_CJFCMEpoh-LU-MtAmvYmY0_6pDcv0hX1q4-eHK07FHnQRDZIm8a2wMHFWds9MvhAF6OzVihf1RjhPzYL0al9X5GPhDomQKuD7No10klMkXsuoltRoT6fli-GQD6s7AK4vKZLRtab2P93n_AXTj4u9ClV2G978r7ofsJq5vqiiyrmbKIiHxvCEjCf4B6bL1jods-FBSFSrdePwq2Avpp0SCGUnwrVpiqP10gzkR6SS2dI9vRbCkyTXgh44RHL0igenZrIpt6MNSjl3-jtNBJeq70BZaKb0CCdI2rCdjm3U9EzYkjWnI7Ectau8QRM7huk0fbldqdP48srN-19oISQ5W8Ysy2oHLQeAa3SkHhZSW8ZeZVhPWGSx0uDPMCZw7poFprGi6zkWV2tcnkh8PAk4ftEm8SKan_lZiP_vmF0lAANankODd2_9WQhvdpHq9mNhR0fWc8USLNhzEJxx5ztAl6ulH3C1SzeSltH--RQEcem76fSW3mZHZA5nbKUOxXQSZ-jRv-xCGoEDc1FGAVcrb4KkpmnBuSqPQwLQUhqTLK9vyd4VLwjYnZW9U160vqvFTJP2I0BsDFF1hXQZdwqPE8KLTng9jO3VTsZdx0b24uDlhL2Alj23MN5eObHLuNcJljtzizmUCZ2L_7kK2HFyuF0uNw0YLZt9SMCgt4AxXQVaSYr1VB_8P=w3190-h810-no?authuser=1)

#####Bước 6: Cấu hình PHP-FPM.
Muốn Nginx có thể đọc được file php các bạn cần cấu hình cho php-fpm có thể giao tiếp được với nginx. Và php-fpm có trách nhiệm dịch các dòng code php sang html để nginx đọc và hiển thị.

Trong bài hướng dẫn này mình cấu hình PHP-FPM theo giao thức [TCP/IP socket](https://wiki.matbao.net/socket-la-gi-khai-niem-can-biet-ve-giao-thuc-tcp-ip-va-udp/)

Mở file cấu hình theo đường dẫn sau: `/etc/php/8.0/fpm/pool.d/www.conf`

> sudo nano /etc/php/8.0/fpm/pool.d/www.conf

Dưới dùng `listen = /run/php/php8.0-fpm.sock
`

Thêm dòng sau: `listen = 0.0.0.0:9000`

Tiếp theo nhấn tổ hợp phím `Ctrl + W ` và gõ `pong` các bạn hãy bỏ dấu **;** trước dòng `;ping.response = pong
` và dòng `;ping.path = /ping` sau đó lưu lại.

Khởi động lại php-fpm để cấu hình có hiệu lực.

>sudo systemctl restart php8.0-fpm

Để kiểm tra xem PHP-FPM và Nginx đã kết nối được với nhau hay chưa ta sử dụng câu lệnh sau:

> SCRIPT_NAME=/ping SCRIPT_FILENAME=/ping REQUEST_METHOD=GET cgi-fcgi -bind -connect 0.0.0.0:9000

![ping-pong](https://lh3.googleusercontent.com/kRTV0yJoOK5NQe0YvK9CzWehv0fUv8EoiE6SmoisZNhA66yusHXXRmuzyiz8_mVlJdsnhVa4_A_cuwU6tKU4zi27LbWsud7Bw-LD6Ft1AefhxnloT4bYlBCsWl7VFMlsV1QA2kGT82PcxUnA4Iw-95WMGkZtHHTrXUzAdvR3BFIBpXhqrVaWRLJv352BC8Hu_8YPudKDy-Tw5AIbm-_n637vifA_b7xG38zoF28OqG2o6WIP4E-R4kXMfj2shsmeK6gNXDPLnUuPBIoRwCSbEga6onZbwNwhnrlScCJXrjvtxoPf-STqMe1QjA1HsvaJzF5ZrP1KjVFmks2Hs3KvU6gssLwu4BslEsGONJbkDDqqVfF05Os5UfHplqlCYNqaY7OxIOCCTweyaovW4EP4ecdZDxtbXAl8knnl4h9haMkYpRZkRpl2PgM7rU-TUxRQORx8UYu-vJKqx2pQjmhBntC-eUUXX725j0IwOq5jojjVeHGiFREUjOI7i4Y3L0SgaXzVcJ9iVE6U9wm3RqIv8GeX3yJOnpa_w5VLPXG4jIU98chWvwcc2xbrkZ2T0p7erDsOzrQRpzd1OLYllEB_JXqmR0-izJtNCyZQq47hh8Krg5-xdGB3DeDyPKvJ3Mw_Kvpj0YYYc7bSKEGrAl6ty5HepRBbAeIjG7tjxHeXimv69HbzGixPKG8xKQneRJ2xdSH5-NjILAm0PYpBrZYwiFaA=w3182-h226-no?authuser=1)

Như trên hình là đã thành công.

#####Bước 6: Tạo Nginx Server Block.

Đầu tiên các bạn cần back-up 1 file cấu hình gốc của Nginx để khi cần có cái để dùng.

>sudo cp /etc/nginx/sites-available/default default.back_up

Tiếp theo xóa thư mục default:

>sudo rm /etc/nginx/sites-available/default
sudo rm /etc/nginx/sites-enabled/default

Các bạn tạo một file mới và coppy file cấu hỉnh của mình làm sẵn vào.

> sudo nano /etc/nginx/sites-available/web_example.conf

Và tại file cấu hình của mình ở link sau: [nginx.conf](https://drive.google.com/file/d/1RkrY96SgEcTYPQnf7hI9po-vvAu2AjyL/view?usp=sharing)

Dán vào như này:

![anh-dan](https://lh3.googleusercontent.com/cdoZXdVhjRMu90o0HZwjOrr5UlpOJ0v5mS_lG8ivVVBfP9NyO8TkIZcGWiEQ-ArEJ9v18G73TTbd5Gz-OwrsehpUhZ1qDi3rKckvvhKRAgR4BOKeqgmCcLWwRwyNbIl8PZaFPJK8ijo3qqzD7PA0MUmhn1UCGvlwZx-mr4oSh-0Hfi0-FMaDCsnGlBhAjY5F8m71TGNxXLOzeYjifC0jhdOZQgSfks1bkJXWhqkZMmAMCVrIq9Cw39I53yC8K6b-P7SVXrTa2I0IKVuA2t70YMJBDy8win3-FDzMt4FSVlQVYm_UR4XGoRGRR3o6dkIsLM6wxfn7vM8r00vnX7gNCzXx64KfBnal7uI8MgzQDzGxZ1UaLgL3BjWQtuthbsdBlinYb-AYu5W2po_01Uqs6DL_lHGnTmlqoHa7WybX9Lq3pHChBz9lpgq5R660nC6usVM59It-WNY1jAUX3bxBdlXn1VG1tq8cUvoungZjaKo5As12Op-ECWf25EF6U8YvKe_FLnFhWPLvjkEwoExXyqKA-Q07RML6lobuoGHw2ysBVjsxiqacFEguTunvLMshADw3AZgD11cJQSEHR9zMlNKddCB2JhdSO5IaDrLMBAwW_Q5LsyGqHpF7qpNzEpzYOZ0tM4XzCmRjNOLQV__PJ_X7FO9CByQI1d8pD5rC8uq8VNIUU6uPRL1-LvELfrc2oiBSXxSCVjEqAMgjiPUgRW9x=w690-h346-no?authuser=1)

Lưu lại vào chạy câu lệnh `sudo ln -s /etc/nginx/sites-available/web_example.conf /etc/nginx/sites-enabled/`
Câu lệnh tiếp theo:
 `sudo nginx -t` và `sudo systemctl restart nginx`

Tạo file info.php để kiểm tra xem nginx đã chạy đươc file php hay chưa.

> sudo nano /var/www/info.php

Dán phần này vào `<?php phpinfo(); ?>`
Lưu xuống.

Bây giờ trong thanh địa chỉ của trình duyệt, nhập server-ip-address/info.php, ví dụ localhost: localhost/info.php, server: 34.324.123.11/info.php

Kết quả như này là được.

![image-info.php](https://lh3.googleusercontent.com/K2BZqJsvqbqVASxgkq9cwIqSK7yQ9_IFNIfsS0bZG0HxmEOoDEVzqJ0OD40MnCqQycHgoeWaDquYxZ40kjLfa_qeKk6EvNqhmMgZ7T77uNEplxU9gEv-SHmOwnxjy_k7tSV6xX8uEo0tNJkbaSIAh6JhbAdBPtf0jfcyOLIuEJwnPCdEGBclQltjauCRfmv4jfRzXX9mCZdi33k0YViuYOVWmCNBZAdD-qMdUwSY2jJSztN9VdsgNa_6M9fe25kdNOUR3tPBPRZBzjlk-3BCrB5pG-ehw-S4IO6RIKRuTf7fHvJM_4GG7Gn_IsYc41oT3qvQs3Cp8i8zLffzLzPgb7HObq6m78ObbznyFh_7HyYqwETTkbvvZgTEftnd_1BZf9fgh8o40PzFeH6CwOrKnO0svMjBiWg3iGm5UBlpmNxAFLik5ZEFk5dgTdsBQyrpr5nlaEH_aDnV1vEX1yPmpFy6MzqUIdM8MF3jOYmdQDg8p3EiEgUCySvTkCmbYuPuoghqgbf4ZNX4GrhWO4w2q6NQrhgpR_gzKnmlltsG1fNgyfpbHy8Jp0vNCo8CqqvBoTTTCCj4VHjaRQdwxPX1mk7NSbf7sKHKW-nQIC1V0ijTx_txusG4aFjOvocUYyF4GTANeLDFL581U3N0X8usQ0vR8gHO536l607-BAeOkYtYtNZ4xmMFBVtHKIoO58Dns1N8CCtwqUmDvlPgxiixt0a-=w657-h391-no?authuser=1)

Sau khi kiểm tra xong các bạn hãy xóa đi file info.php đi nhé

Và các lỗi trong quá trình sử dụng các bạn có thể tìm xem ở log của nginx theo đường dẫn sau: `/var/log/nginx/error.log`.





















