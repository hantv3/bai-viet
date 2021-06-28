<h2>Hướng dẫn cài đặt LEMP Stack trên Ubuntu 20</h2>

> LEMP là viết tắt của Linux, Nginx (Engine x), MySQL và PHP, và đây là một trong những biến thể của web server.

> Lưu ý: Bài viết chỉ giúp mọi người cài đặt và chạy được với PHP, sẽ không giải thích sâu vào từng thành phần của LEMP. Nếu các bạn muốn mình viết sâu hơn về phần này thì hãy comment để cho mình biết và thực hiện sớm nhất.

> Trước khi làm các bạn có thể đọc trước về các sử dụng command phổ biến cho linux hoặc ubuntu, các sử dụng nano editor hoặc vim.

<h5>Bước 1: Cập nhật và nâng cấp các gói có sẵn và đã cũ trong hệ thống bằng câu lệnh sau:</h5>
> sudo apt-get update && sudo apt-get upgrade -y

Câu lệnh trên giúp chúng ta cập nhật các gói(package) có sãn trong hệ thống nằm trong file có đường dẫn: `/etc/scources.list`, `-y` ở cuối câu dùng chấp nhận các package cần thiết khi update và nâng cấp được đề xuất.
**Lưu ý**: Phải chạy câu lệnh update trước câu lệnh nâng cấp upgrade vì update được sử dụng để đồng bộ hoá lại các index file từ các nguồn từ `/etc/scources.list`.
<h5>Bước 2: Cài đặt Nginx.</5>
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

![status nginx](https://lh3.googleusercontent.com/hJ1Or7gcxni4K6qy2qhhK333R2bW1Cu_ZE--ldG0_XwmJe_zbTMV4Kzr0X-3cduBCO_LW04yRkYeK9LG0Yx8fMw14ZBBbwzIFym0eUmWiSFupek5SHcfl-Z-x_q3zJ5IOXc1YrHZg4q0a08J3dpGttqXemL09iVCrG2vwGJs2scUlZMpJpzTqocnMT43usDWfQlsYr_GD2kQ3UTnQcgWiUpB2zOesoRZFV0rW5MWqd_T3RzDWOwMK_o6UYxnD0_UdpLWV2GyQKcrmiqmEzxQcbIWzYv9QWQCazvaBJ4dFOaMQGbd1y2BYeMxWghWXFIjBAgGCOI9mSVA_vcPaWHTgtmW5Fx228kyNJuQrfqDsfcGgvKJcaA6UTfnEg6l5ZZb7-7oZiBP7RMHQ4VVIKWePx3a0pzoLlvc_dQEeCj26XTQylJEA-6xPjx6a80kMXVIqzrY6CrgfuvCF5oxR9sy4-p8V7Wj7FamrKOMoJv5xDZ_RAtsQynwulCl5DcI_0_K0acnfzj-VwfSKNy0IdIkvE-JhZQbZP4l-MYql6iRg_ohUqpivVbsv2bkSEut3-1hxtkUd_cfH10GgLk5Iif8RHa6OGk6S-WRJZGv5MjzyXmeElTA3yiWs4-yo9zUiqupCUEUuSWcJ9KWe9wnftCAqN-Q4XibuLAUi8vYYi4ACAAaz0-30HUEP77NGBHzYn-m9_hsy8Ek3HHY4VzIdDF9pIGW=w3198-h166-no?authuser=1)

Giờ bạn mở trình duyệt lên và gõ [http://locahost](http://locahost)


![image-localhost](https://lh3.googleusercontent.com/AxMuINBLsVhtiI6w27GjaQxusaBi8mb7bxvakSMyhfnsihLD3Uc7TDWCCAj1jvNYjWEK6vVXwD2op3e5p0xhStVAB60ODYSLbO80_zs5gspS-ZlyiTSNpfqDmKABHtM8BhJB2vnN-4LXQOm63kJo9qle0zicYxXNraI0N2tMnzpkhsT0ozwslzO89k6kIQNWk33Ze8G9_DN1SBLKDVN8h_DYt05qNG8M-hfTBnORSMpTJwAdgn_SlVeEgVXYwEynhP2tUgBLBoj6RpJlCRab92gU1-_2_RZNDNCmEm4_OrfolnWP6mj5p8VH7L0RbImhwQboZTpmAEofaxy-V0ev_7CBfYYc7uzYB0BKHlzUDoBQLvJ6VZb9oQGVaiofJoD_geOtoCvXkrdEzt_oicptbSyPtgLScOzeKpxo4_02Fgx5HqnhkdV6iiiW4T7Suax2OOOIfBuPnluynckxh6GJUfchmvd9by_o8DGCq0MiFX7J-GcXNfd4RK4njxZNiZQhRouir1nAa7Up2wmQvCXFWfLicwXhR_VKaBGn95EwyEWOZul8SO0cIM-EwlT1MHoq13RRj7BobqTpsSd96pRw-aWawKHXxR6zTtxDVE5gWHcYH8F-fQH3PHSWLesnxEdNCZX3szTCZ090VwH8efzDYoqPU9t5xK89jfCONRYTocF8tndJk-_lR4fRy8k9EeIR8WVmmJb5-QRIh292JUfVXjmC=w2298-h1466-no?authuser=1)

Như vậy là Nginx đã chạy thành công.
<h5>Bước 3: Cài đặt MySQL.</h5>

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

![login-root-mysql](https://lh3.googleusercontent.com/FqEgobkDnwzdOh8gmC02kMOu2c_zgrCNKi5F5xP3yfN5vmYu-ge_oxxHLu34ekWlI_EZ5SGiNjiFEcyp-DWj-jMEsHIXGaBtOwN59g3xZXZzuX1Plj1LKfiFV3_2NeZAunIYpJDJjabX6ZHGPUaQ_PjSPu2-FRWNE9UTV_rJIXX0H6RhtqtBG_KUtWvtLi2OGhxjn0HlLeQZwzXAw53mXM4TnANhly_seuNqP3y74NKWUSU_gHeRX179ucgh8usoONCinZHUMjW1n52DYY9mrmqt0_ffH5nyFQ1XEHwQyKmXBfU25PUd64kgNJj9ZN1rhSensdRJkv8-AZyJBpMT-25x_aDVgcSmOWS513TiBKH5yOPssVFDQofdjdd12hXohR5Fd4ri4_bN_r5l1eYJ4J5AfTGxLry0MOdOzHtvt01XvjeuaEnJTjvBcABjCvlNEJjbTz9JlKXXiXIqIKv8GnDPebIX0R9QFVmiJ1JZ1qle6gazE_4MrK8PF4cLQ1mANFL3qqs0U6-pZsOjSu31RocQdEH9HwGpWoXOY6bWWYve-F-IbWz1Bg6E1eV4YdLXDmd_9VxUpQP3o8ZIj4AQrzRSegSGsniRpP2rprqcYfU0Qfze8MgqqIX6l4n9XuwO0zbdJwm2UY4fmegjQVA5xS8Gle7aReieH6AegOtqotsC60ouSh9tD3T2a-qQrMgKqVB32OVdc4tQCMaDDbod5IRW=w1448-h540-no?authuser=1)

Như vậy là chúng ta đã truy cập vào được MySQL.

> Từ phiên bản MySQL 5.7 trở đi, user root của MySQl có thể đăng nhập mà không cần sử dụng mật khẩu như ở trên sau khi chạy câu lệnh **mysql_secure_installation** và cấu hỉnh xong, chỉ cần chạy câu lệnh **sudo mysql** là có thể đăng nhập vào MySQL rất là tiện lợi. Nhưng khi chúng ta cần cho phép kết nối từ bên ngoài vào ví dụ như sử dụng (Navicat, phpMyAdmin v...v) truy cập sẽ phức tạp, nhất là khi cấu hình trên server và cần truy cập đến để quản lý database từ xa.

Để giải quyết vấn đề này chúng ta sẽ tạo một user mới với chức năng dùng để Remote Access đến MySQL server.

Vẫn màn hình command trong MySQL server, nếu bạn đã thoát ra thì hãy vào lại bằng `sudo mysql`.

Chạy các câu lệnh sau:

>SELECT user,authentication_string,plugin,host FROM mysql.user;

![image-show-user-mysql](https://lh3.googleusercontent.com/eMJODPzEZebFpPeoNKkHhqTqC0ZFBsjShnGfNhuu0xD9NjaFVER-_bTe-Vz2x9KkLtxjFdaNFVxUlZyGtqjlPAUGtR7oScJZ4cBWFXdzYtPfeHvCLeP63qksw5hkK1bSPY0TaSw789fKQnOYOBpxz3qpoJUNg-YqUtQtgs_euW6QumN41AShSzD4BUJavMw991gfgO83bk_CLzArtx4m_PjF6ycaUnpaawWDK9DX94NIkg7G8TVtq8Tti2EWn8Zrz1adwtTkuhYlW1jaPeBG6jprvptwOkckeEVwhJYu1zzwv0erLgy0KqOsollXTqTNMuQGxYLS3kl6X0gnhygURKf9EBrTWyCRqAFptXZ54_df595_8m6JDALNUo4afyJDKqYlTuxr4vKgt5V3AAm6oGYDUEQlg2ljcQjOx3XrXFUlykzhFC44qYeFagicEglgdhQfyGV05CxN45mbirT8w_3m8rWCEWNt87AGKSuUQY4XwPqOp4I8Yh4ysg0l_DwghEm551IO6CngiWPo7bx9d9Rtlv3msx-7y5QSipIbZSbgkhK5XBUkGr__8yjxI7tbFONcL7wCY5xygyGA407_zmcAKpjw3XKvSwMpVuqov7R-BRvvsw0yiLfDs-OM-huLZCDPzpC8yEPCzAeRxnlw76l1ntwR3cHdU851QUF3S8LNvKkmScZu9g5VXLol_ksXH9m5x3YM7L3a7uTAXhI5qhhN=w3180-h524-no?authuser=1)

Đây là list user của mình mặc định khi cài đặt mysql sẽ có, một số bạn sẽ hơi khác chút nhưng không có vấn đề gì cả.

Câu lệnh tạo một user mới:

>CREATE USER 'user_demo1'@'%' IDENTIFIED BY 'password';

Giải thích một về kí tự **%** có ý nghĩa là chấp nhận tất các kết nội cục bộ và bên ngoài khi sử dụng user này.

Tiếp đến là cấp quyền cho người dùng có thể thao tác với tất cả các database, thêm, sửa, xóa các bảng và dữ liệu.
>GRANT ALL PRIVILEGES ON *.* TO 'user_demo1'@'%' WITH GRANT OPTION;

Chạy tiếp câu lệnh `FLUSH PRIVILEGES` để tải lại và chấp nhận các thay đổi mới.

>FLUSH PRIVILEGES;

Kiểu tra lại list user xem đã thêm mới user thành công hay chưa:

![image-them-moi-user-mysql](https://lh3.googleusercontent.com/4EDF2FwETLYxEZybSO9lzyG65Lu1mTpa_NsMXHT_0L21u3AZY8m-CvKgxgXGUIxS5YSDlUIAkfoJPLxK0iI8UwyljyPyWuMuSN0zzTxPI_BH8NKVACpvwYrLnsIrwM-LeuuRJQ7ksc9erehyKWX6y2gxTO1v0qelcMK-SBcS1IqtxFOmflIQyErrbrEVtk5FYQB0dbNBt3SqCNriohX2E_XEQ7MUjJclcUmLMqI3-BDw4-9qXhdsSkYHUBukymbJ_CJWIwFpmnWiNbxZmlFwviHhl0eqOD1QWLf-8AXGUyih71tKOVeXzjeavTUpnlVPcRwS2mqmpQPwYt1II08iySvFzHlgyMFYgQnJ4uDXpTm9m0dIngINYiseC29loCt8Et21_w4YQvnHQbrLFmIBcPzDSVSqg4ORemQDajOWc_NKSpWegra-TGKpaOPRb5Wsl_PWZBUeiMCttYfzBJriILolIIvoVqnIs9OZT3bb44lliRw99WfQzsvjTwC6Y5NC6qBT9yK252L7MgJ4wjL0uHRq4Q8pQQ76_2Fn3y6AO0SDF4AQob88h2nBJGBg5Eupp8fM_7OtytywVfE-1uXzh4KidFDzUVCIAYuVhVkGTxjydOBUZi91A1_TLTwUBsdJU7AoPb80x8HGOzSA60HbEsjrrytTsVYsm60hoZOX0MHa0q3RebQrhfgWoWAWIDiuIVpO0vmUaLIeeqoD6ErgggOk=w3198-h536-no?authuser=1)

Như vậy là thêm thành công, giờ bạn có thể kết nối với phpMyAdmin hoặc bằng Navicat.

<h5>Bước 4: Remote Access MySQL.</h5>

Nếu các bạn cài đặt cho server mysql thì sẽ cần phải kết nối từ bên ngoài vào để quản lý và thêm sửa xóa dữ liệu cho mysql. Nhưng hiện tại khi cài đặt xong chúng ta không thẻ kết nối đến được, vì mặt định mysql khi cài đặt xong trong file cấu hình `mysqld.cnf` sẽ cấu hình mysql kết nối cục bộ, các kết nối đến từ bên ngoài với `user_demo1 ` sẽ không thể kết nối đến được. Vì vậy sẽ cần phải truy cập đến file `mysqld.cnf` để chỉnh sửa cho mysql nhận kết nối từ bên ngoài.
Chạy câu lệnh sau:
> sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf

Tìm dòng `bind-address`, mặc định sẽ là `bind-addrss = 127.0.0.1` các bạn hãy đổi `127.0.0.1 = 0.0.0.0` để nhận tất cả các kết nối từ cục bộ đến bên ngoài. Nếu trong file `mysqld.conf` của bạn không có dòng `bind-address` thì hãy tự thêm vào.
 Sau đó nhấn các tổ hợp phím sau: `Ctrl + X, Y, Enter` với nano để lưu thay đổi.

 Sau đó restarr lại mysql để chấp nhận thay đổi mới.

 > sudo systemctl restart mysql


**Lưu ý:** feild host: <input> nếu là ubuntu destop sẽ điều là localhost-127.0.0.1, nếu là server sẽ điền là IP host vd: 34.344.12.33.

<h5>Bước 5: Cài đặt đặt PHP.</h5>

Trong bài viết này mình sẽ cài phiên bản 8.0 của PHP.

>sudo add-apt-repository ppa:ondrej/php -y

Các gói cần thiết để chạy 1 project PHP.

>sudo apt install -y php8.0 php8.0-fpm php8.0-mysql php8.0-curl php8.0-json php8.0-cgi php8.0-xsl php8.0-mbstring php8.0-opcache php8.0-gd php8.0-pgsql php8.0-intl php8.0-bcmath php8.0-soap

Sau khi cài đặt hoàn tất hãy khởi động php8.0-fpm.

>sudo systemctl start php8.0-fpm

Cho phép chạy khi cùng hệ thống.

>sudo systemctl enable php8.0-fpm

![enable-php8.0-fpm](https://lh3.googleusercontent.com/pkIxFS0yE9dvsejWDsNe0UKg6msy6Dg7pNukLd4Q2sC7mq4x2g0jdhSGwo3FawNRp1SC-0380XUhQs1TR3WyQXi63PASMa7OT3W9jHQoafyinmCLh1WuJbUCujSnAkh7QSCGq6i-oC-a8FdnbEIT6SecTPOqQAGdfJDwvhZhcZyNXgoOaaOQs8t75s_HdWHdyYmNH7Wmqe7KpAv4w49RYytFnXRNUT1mxVpWUeY0SytM5c1FEB006-fXyRWO7rI1lCu-5JCvQrhqY9zrf73UBT6ncT6lXiMGxx6FjsPXJ_uk96hBxgNytDBkNrBAtdPo6BIrMNM-8-w1H19zYtPZXzQRswOLeF_1v3TO87rdm7twIPNakW2mROZSpk5nVtLqDCGU2fRKwXOnvCFTLJ0QMFRAnNJW34MnTXm-wuC_tiO0lcApJ4e87WmOMzM3x0e7bmGnqObyZdkz7p3qk-iE4J0PUH4EyNoCDo4EhHlSdVa5_dZEHcB6ulQVMhZa_PSk2vIWcGQ_SKp5k3RfA_bEgubvstZUtcWCLL8QMGfcuyLDSoTy8cXsxKcXooxne_Fbg0SY-7QIzmjtL-SVkEX0n_CK_AfXTeRulJNRze4QbAHGWUVA4_d9XGR9xZukViFK00M0I5aJ3BQ94gtSPdyWacYBAEAYCHB0ajbyZcFIzh4X0XMxnEuCnEkH1MpayXXaMyls-8qrU3gaulVyEsxHlXmN=w3214-h158-no?authuser=1)
Kiểm tra trạng thái của php-fpm có hoạt động không.

>sudo systemctl status php8.0-fpm

![statusphp8.0-fpm](https://lh3.googleusercontent.com/zdk1Hp9mdyhzRyjyFyD8B4IAv_jD97kJ_9VkqBPrM_xSxGnc9Fx9TpvL27xTdLa_6ASg5XNTy9VJ4cKQZZ6zwfuHyqi2yZtVY9EzAVHydRUyl2rXbp_EeT_4QPCwazDTPHX7ftUbPZqFxx4iRyghQQw0IxNAPezlES9I6TcDLRY5oggw5EIYHpV2K7cApR9MnBuE41yx28LsdVCYNmMj72pQmoOhaS9dbN_H179KPudddM7_hvqNgVS_BQcmv2mMilxgMOMIrb_BrrAlcwoIVz6G1MyQN_TGlVcLxEG82kMmLkxEd-opcpSXnND1LSCY8lxrknO3zZR8CmywOc9d1YyA8w1H8hizVhVZtPxeQPwpvhL_1n8YmOqJ73W9Bk5loXErJDtV5LPN8UNW2qNlgCJ4b4ksvdIK69pDOXU5xvFtiYmjRel9I6kdHjEVDMrphLGtSNAEDukAl0ytvo5tFytUJe-d_fbsJ_jHbe8chmxZ6EKjgJbOkKOD-gh6-gZ9ymgyAdMr8CjO8q0DgcVQkhHeiQGkB6PYn042DwZIyCnA9IRdm7fneoMemGDJ_PGusID1i829NX4LPWVTZ07wn6qIpwBukIDGt6jDmAolokXI4v95Jo5jjGSkRQ2vHweKuCrGgMWgRdnINHFNlg3yayVU18wHUhGvkHZeXp1HiPS9-yBpnq0ps7V2XFZ_wZ1_Yo7n_4GOlSqRxVf5hdJuCy9H=w3190-h810-no?authuser=1)

<h5>Bước 6: Cấu hình PHP-FPM.</h5>
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

![ping-pong](https://lh3.googleusercontent.com/ftqi-CdEc7em0btOVRL7V_vO2dGkyOrSs-dSDPbNgz0zu_-B1u480-tRcjZJgSpqfTqT2NQ85xj4YqIWZrS_61Xc5wMOIswQToeNeynmDFuS0xGlAmEW0CHO3HBQU5YqBctsuh-LmpE94ExMXhhw6zXPJ5jA_XbKBpETNwC0KcgJZcZaSXfeximjXs9Ws4mlPOw6PDHOPEAut7qRT2TCbO24oCOv61RA3yKVhkyS52XTqjtVhfm0Yh-BvZAsdvb-aGj0sOj7rvgNNQKDnBSzzs9zTO0Q-2Hh56HH5Qaa0uaZP-GT0_A64-t_fK6aC31NkkIZS-MKWJNYhEcEojIo2ItipP_f2bnHCxtB_ffY6m1fym-koKIJno6vpn9K4sMJHz75glKEs4sZbnq1oEBhGSbFIdB-oZKirI9r91ZVCPghnIVzkD6gpz00RfqWMVg8AmBFK2BJq1H3CPIhgqabIsFYN9MVMm8u3xxLUkR92hPWCC7I3pWKe3g3LM-XceVCgZ5FOxSn6SVtQXqKNUYIBQh_vd74VrNkMUhGIfZvb7rXI8UM4cZFO-mwOirugseQRueioOHrmX5QwsW71C_-eg-nGuBFn-qb2nw0bpZoFcaJAeMWG-PfrwmgDQWxX2vojBIEbTMvEl343B3xiRsq9J-mO4ZxwSvaffE-mG8FKuAr6KocB59JchE284T8gmgI-7djycgkjGmc0O4IkcSvPALH=w3182-h226-no?authuser=1)

Như trên hình là đã thành công.

<h5>Bước 6: Tạo Nginx Server Block.</h5>

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





















