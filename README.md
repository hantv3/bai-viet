Hướng dẫn cài đặt LEMP Stack trên Ubuntu 20
LEMP là viết tắt của Linux, Nginx (Engine x), MySQL và PHP, và đây là một trong những biến thể của web server.

Lưu ý: Bài viết chỉ giúp mọi người cài đặt và chạy được với PHP, sẽ không giải thích sâu vào từng thành phần của LEMP. Nếu các bạn muốn mình viết sâu hơn về phần này thì hãy comment để cho mình biết và thực hiện sớm nhất.

Trước khi làm các bạn có thể đọc trước về các sử dụng command phổ biến cho linux hoặc ubuntu, các sử dụng nano editor hoặc vim.

Bước 1: Cập nhật và nâng cấp các gói có sẵn và đã cũ trong hệ thống bằng câu lệnh sau:
> sudo apt-get update && sudo apt-get upgrade -y
Câu lệnh trên giúp chúng ta cập nhật các gói(package) có sãn trong hệ thống nằm trong file có đường dẫn: /etc/scources.list, -y ở cuối câu dùng chấp nhận các package cần thiết khi update và nâng cấp được đề xuất. Lưu ý: Phải chạy câu lệnh update trước câu lệnh nâng cấp upgrade vì update được sử dụng để đồng bộ hoá lại các index file từ các nguồn từ /etc/scources.list.

Bước 2: Cài đặt Nginx. - Nginx hiện tại là một máy chủ được sử dùng từ web nhỏ cho tới web siêu lớn vì hiệu năng mà nó mang lại.
Sau cập nhật và năng cấp các gói trong hệ thống ta bắt đầu chạy câu lệnh cài đặt Nginx:

sudo apt-get install nginx -y

Lưu ý: Nếu hệ thống yêu cầu nhập mật khẩu thì bạn hãy nhập mật khâu, và mật khẩu khi nhập ở màn hình command sẽ không hiện ****** chỉ cẩn nhập xong là nhất Enter. Sau khi cài đặt xong chạy tiếp câu lệnh:

sudo nginx -v nginx version: nginx/1.18.0 (Ubuntu)

Nếu hiện dòng nginx version: nginx/1.18.0 (Ubuntu) thì bạn đã cài đặt thành công với 1.18.0 là phiên bản bạn đang sử dụng.

Tiếp theo sẽ là cấu hình tường lửa:

Cài đặt tường lửa để đảm bảo tính bảo mật và cho phép lưu lượng truy cập qua các cổng mặc định, thông thường các web sẽ sử dụng 2 giao thức HTTP & HTTPS tương đương với cổng 80 & 443.

Chạy 2 câu lệnh sau:

sudo ufw allow http sudo ufw allow https

image-ufw

Chạy câu lệnh:

sudo systemctl status nginx.service

status nginx done

Dòng Active: active (running) là đã chạy.

Nếu bạn chạy câu lệnh trên màn hình command hiện như sau: status-nginx-fail Dòng Active: active (dead) là chưa chạy. Như vậy là Nginx chưa được chạy. Bạn hãy chạy câu lệnh:

sudo systemctl star nginx.service

Sau đó chạy tiếp câu lệnh:

sudo systemctl enable nginx.service

Cho phép Nginx khởi động cùng hệ thống.

status nginx

Giờ bạn mở trình duyệt lên và gõ http://locahost

image-localhost

Như vậy là Nginx đã chạy thành công.

Bước 3: Cài đặt MySQL.
Các bạn chạy câu lệnh sau:

sudo apt install mysql-server -y

Sau khi cài đặt xong chúng ta chạy tiện ích mysql_secure_installation để cấu hình bảo mật.

sudo mysql_secure_installation

mysql_secure_installation sẽ giúp chúng ta cài đặt mật khẩu root MySQL, xóa người dùng ẩn danh, vô hiệu hóa Remote Mysql và xóa cơ sở dữ liệu test.

Enter current password for root (enter for none): Nhấn Enter Switch to unix_socket authentication [Y/n]: n Change the root password? [Y/n]: y New password: Mật khẩu root Re-enter new password: Nhập lại mật khẩu root Remove anonymous users? [Y/n]: y Disallow root login remotely? [Y/n]: y Remove test database and access to it? [Y/n]: y Reload privilege tables now? [Y/n]: y

Tiếp đến các bạn truy cập vào Mysql với user root bằng lệnh:

sudo mysql

login-root-mysql

Như vậy là chúng ta đã truy cập vào được MySQL.

Từ phiên bản MySQL 5.7 trở đi, user root của MySQl có thể đăng nhập mà không cần sử dụng mật khẩu như ở trên sau khi chạy câu lệnh mysql_secure_installation và cấu hỉnh xong, chỉ cần chạy câu lệnh sudo mysql là có thể đăng nhập vào MySQL rất là tiện lợi. Nhưng khi chúng ta cần cho phép kết nối từ bên ngoài vào ví dụ như sử dụng (Navicat, phpMyAdmin v...v) truy cập sẽ phức tạp, nhất là khi cấu hình trên server và cần truy cập đến để quản lý database từ xa.

Để giải quyết vấn đề này chúng ta sẽ tạo một user mới với chức năng dùng để Remote Access đến MySQL server.

Vẫn màn hình command trong MySQL server, nếu bạn đã thoát ra thì hãy vào lại bằng sudo mysql.

Chạy các câu lệnh sau:

SELECT user,authentication_string,plugin,host FROM mysql.user;

image-show-user-mysql

Đây là list user của mình mặc định khi cài đặt mysql sẽ có, một số bạn sẽ hơi khác chút nhưng không có vấn đề gì cả.

Câu lệnh tạo một user mới:

CREATE USER 'user_demo1'@'%' IDENTIFIED BY 'password';

Giải thích một về kí tự % có ý nghĩa là chấp nhận tất các kết nội cục bộ và bên ngoài khi sử dụng user này.

Tiếp đến là cấp quyền cho người dùng có thể thao tác với tất cả các database, thêm, sửa, xóa các bảng và dữ liệu.

GRANT ALL PRIVILEGES ON . TO 'user_demo1'@'%' WITH GRANT OPTION;

Chạy tiếp câu lệnh FLUSH PRIVILEGES để tải lại và chấp nhận các thay đổi mới.

FLUSH PRIVILEGES;

Kiểu tra lại list user xem đã thêm mới user thành công hay chưa:

image-them-moi-user-mysql

Như vậy là thêm thành công, giờ bạn có thể kết nối với phpMyAdmin hoặc bằng Navicat.

Bước 4: Remote Access MySQL.
Nếu các bạn cài đặt cho server mysql thì sẽ cần phải kết nối từ bên ngoài vào để quản lý và thêm sửa xóa dữ liệu cho mysql. Nhưng hiện tại khi cài đặt xong chúng ta không thẻ kết nối đến được, vì mặt định mysql khi cài đặt xong trong file cấu hình mysqld.cnf sẽ cấu hình mysql kết nối cục bộ, các kết nối đến từ bên ngoài với user_demo1 sẽ không thể kết nối đến được. Vì vậy sẽ cần phải truy cập đến file mysqld.cnf để chỉnh sửa cho mysql nhận kết nối từ bên ngoài. Chạy câu lệnh sau:

sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf

Tìm dòng bind-address, mặc định sẽ là bind-addrss = 127.0.0.1 các bạn hãy đổi 127.0.0.1 = 0.0.0.0 để nhận tất cả các kết nối từ cục bộ đến bên ngoài. Nếu trong file mysqld.conf của bạn không có dòng bind-address thì hãy tự thêm vào. Sau đó nhấn các tổ hợp phím sau: Ctrl + X, Y, Enter với nano để lưu thay đổi.

Sau đó restarr lại mysql để chấp nhận thay đổi mới.

sudo systemctl restart mysql

Lưu ý: feild host: nếu là ubuntu destop sẽ điều là localhost-127.0.0.1, nếu là server sẽ điền là IP host vd: 34.344.12.33.

Bước 5: Cài đặt đặt PHP.
Trong bài viết này mình sẽ cài phiên bản 8.0 của PHP.

sudo add-apt-repository ppa:ondrej/php -y

Các gói cần thiết để chạy 1 project PHP.

sudo apt install -y php8.0 php8.0-fpm php8.0-mysql php8.0-curl php8.0-json php8.0-cgi php8.0-xsl php8.0-mbstring php8.0-opcache php8.0-gd php8.0-pgsql php8.0-intl php8.0-bcmath php8.0-soap

Sau khi cài đặt hoàn tất hãy khởi động php8.0-fpm.

sudo systemctl start php8.0-fpm

Cho phép chạy khi cùng hệ thống.

sudo systemctl enable php8.0-fpm

enable-php8.0-fpm Kiểm tra trạng thái của php-fpm có hoạt động không.

sudo systemctl status php8.0-fpm

statusphp8.0-fpm

Bước 6: Cấu hình PHP-FPM.
Muốn Nginx có thể đọc được file php các bạn cần cấu hình cho php-fpm có thể giao tiếp được với nginx. Và php-fpm có trách nhiệm dịch các dòng code php sang html để nginx đọc và hiển thị.
Trong bài hướng dẫn này mình cấu hình PHP-FPM theo giao thức TCP/IP socket

Mở file cấu hình theo đường dẫn sau: /etc/php/8.0/fpm/pool.d/www.conf

sudo nano /etc/php/8.0/fpm/pool.d/www.conf

Dưới dùng listen = /run/php/php8.0-fpm.sock

Thêm dòng sau: listen = 0.0.0.0:9000

Tiếp theo nhấn tổ hợp phím Ctrl + W và gõ pong các bạn hãy bỏ dấu ; trước dòng ;ping.response = pong và dòng ;ping.path = /ping sau đó lưu lại.

Khởi động lại php-fpm để cấu hình có hiệu lực.

sudo systemctl restart php8.0-fpm

Để kiểm tra xem PHP-FPM và Nginx đã kết nối được với nhau hay chưa ta sử dụng câu lệnh sau:

SCRIPT_NAME=/ping SCRIPT_FILENAME=/ping REQUEST_METHOD=GET cgi-fcgi -bind -connect 0.0.0.0:9000

ping-pong

Như trên hình là đã thành công.

Bước 6: Tạo Nginx Server Block.
Đầu tiên các bạn cần back-up 1 file cấu hình gốc của Nginx để khi cần có cái để dùng.

sudo cp /etc/nginx/sites-available/default default.back_up

Tiếp theo xóa thư mục default:

sudo rm /etc/nginx/sites-available/default sudo rm /etc/nginx/sites-enabled/default

Các bạn tạo một file mới và coppy file cấu hỉnh của mình làm sẵn vào.

sudo nano /etc/nginx/sites-available/web_example.conf

Và tại file cấu hình của mình ở link sau: nginx.conf

Dán vào như này:

anh-dan

Lưu lại vào chạy câu lệnh sudo ln -s /etc/nginx/sites-available/web_example.conf /etc/nginx/sites-enabled/ Câu lệnh tiếp theo: sudo nginx -t và sudo systemctl restart nginx

Tạo file info.php để kiểm tra xem nginx đã chạy đươc file php hay chưa.

sudo nano /var/www/info.php

Dán phần này vào <?php phpinfo(); ?> Lưu xuống.

Bây giờ trong thanh địa chỉ của trình duyệt, nhập server-ip-address/info.php, ví dụ localhost: localhost/info.php, server: 34.324.123.11/info.php

Kết quả như này là được.

image-info.php

Sau khi kiểm tra xong các bạn hãy xóa đi file info.php đi nhé

Và các lỗi trong quá trình sử dụng các bạn có thể tìm xem ở log của nginx theo đường dẫn sau: /var/log/nginx/error.log.
