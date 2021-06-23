###Lệnh sudo apt-get update và upgrade có chức năng gì trên Ubuntu.

- Ubuntu là một hệ điều hành mã nguồn mở và miễn phí. Và nó sử dụng nhân Linux và các lệnh GNU. Người dùng sẽ sử dụng apt hoặc lệnh apt-get để quản lý các hoạt động phần mềm như cài đặt, cập nhật, xoá v...v.
#####Lệnh sudo apt-get update làm gì?
>sudo apt-get update

1. Lệnh `sudo apt-get update` được sử dụng để cập nhật tất cả các package đã cài từ internet hay còn gọi là từ các trang cung cấp package.
2. Các nguồn thường được xác định trong tệp `/etc/apt/sources.list` và các tệp khác nằm trong thư mục `/etc/apt/sources.list.d/`.
#####Các xem tệp /etc/apt/sources.list.
Gõ lệnh cat:
> sudo cat /ect/apt/sources.list

#####Lệnh apt-get upgrade
Như ở trên các bạn đã biết lệnh `sudo apt-get update` dùng để cập nhật các gói đã cài từ internet.
Nhưng nếu các package cài đặt đã bị lỗi thời? Làm cách nào chúng ta có thể cập nhật các bản nâng cấp tăng tính bảo mật cho hệ thống.
Bạn hãy chạy câu lệnh `sudo apt-get upgrade` để cài đặt các bản nâng cấp cho các gói hiện tại được cài đặt trên hệ thống từ các nguồn mà bạn đã cấu hình qua tệp sourcé.list.

#####Sự khác biệt giữ cập nhật và lệnh nâng cấp.
*sudo apt-get update*
> update được sử dụng để đồng bộ hoá lại các index file từ các nguồn của chúng. Index của các gói có sẵn được tìm thấy từ vị trí được chỉ định trong `/etc/apt/sources.list`. Và cập nhật luôn phải thực hiện trước khi nâng cấp hoặc nâng cấp bản phân phối.
> Lưu ý: Thanh kích thước đo tiếp độ và kích thước được hiển trên màn hình command không chính xác vì không thể biết kích thước các tệp gói.

*sudo apt-get upgrade*
> Upgrade được sử dụng để cài đặt phiên bản mới nhất trên hệ thống từ các mã nguồn được nạp vào trong /etc/sources.list. Các gói hiện tại sẽ được nâng cấp lên phiên bản mới, trong trường hợp các gói đã bị xoá và chưa cài đặt sẽ không được nâng cấp. Các gói đã là phiên bản mới nhất sẽ không thể nâng cấp và sẽ không thay đổi trạng thái đặt và sẽ được dữ nguyên.

Chạy hai lệnh trong một dòng:
`sudo apt-get update && sudo apt-get upgrade`
