Reference 
- https://viblo.asia/p/docker-chua-biet-gi-den-biet-dung-phan-1-ByEZkWrEZQ0

- https://viblo.asia/p/docker-chua-biet-gi-den-biet-dung-phan-2-RQqKLzeOl7z

- https://kipalog.com/posts/Toi-da-dung-Docker-nhu-the-nao
 
# StudyDocker
- `docker pull {image_name}`: Pull một image từ Docker Hub

- `docker run --name {container_name} -p {host_port}:{container_port} -v {/host_path}:{/container_path} -it {image_name} /bin/bash`:
Tạo mới một container, đồng thời khởi động với tùy chọn cổng và volume

For Example:
`sudo docker pull ubuntu:16.04`
`sudo docker run -it ubuntu:16.04 /bin/bash`

# Some basic operations
- `docker images`: Liệt kê các images hiện có

- `docker rmi {image_id/name}`: Xóa một image

- `docker ps`: Liệt kê các container đang chạy

- `docker ps -a`: Liệt kê các container đã tắt

- `docker rm -f {container_id/name}`: Xóa một container

- `docker start {new_container_name}`: Khởi động một container

- `docker exec -it {new_container_name} /bin/bash`: Truy cập vào container đang chạy

# Dockerfile
Dạng text, không có đuôi, giúp thiết lập `cấu trúc` cho `docker image` nhờ chứa một tập hợp các câu lệnh.
Từ những câu lệnh đó, Docker có thể thực hiện `đóng gói` một docker images theo yêu cầu tùy biến của riêng bạn.
```
[Dockerfile] -----build---->[Docker image]----run---->[Docker container]
```

## Thiết lập image gốc
- FROM
E.g `FROM ubuntu:16.04`
Khi Docker đọc tới câu lệnh này, nó sẽ tự động tìm xem image ubuntu:16.04 này đã tồn tại trong máy chưa, 
nếu chưa thì Docker sẽ tự động pull image này về.

- MAINTAINER: 
Một optional dùng để đặt tên cho tác giả của Dockerfile mà bạn đang viết.
E.g `MAINTAINER seulement<nthien86@gmail.com>`

## Cài đặt ứng dụng
- RUN
Để thực thi một câu lệnh nào đó trong `quá trình build images`.

- CMD
Để thực thi một câu lệnh trong quá trình `bật container`

Mỗi Dockerfile `chỉ có` một câu lệnh CMD, nếu như có `nhiều hơn` một câu lệnh CMD thì chỉ có câu lệnh CMD `cuối cùng` được sử dụng.
Một câu hỏi đặt ra là nếu tôi muốn `khởi động nhiều ứng` dụng khi start container thì sao, lúc đó hay nghĩ tới ENTRYPOINT

- ENTRYPOINT
Để thực thi `một số câu lệnh` trong quá trình `start container`, những câu lệnh này sẽ được viết trong `file .sh`.


## Cấu hình
- EXPOSE
Container sẽ lắng nghe trên các cổng mạng được chỉ định khi chạy

- ADD
Copy file, thư mục, remote file thêm chúng vào filesystem của image.

- COPY
Copy file, thư mục từ host machine vào image. Có thể sử dụng url cho tập tin cần copy.

- WORKDIR
Định nghĩa directory cho `CMD`

- VOLUME
Mount thư mục từ máy host vào container.

# Cách sử dụng Dockerfile
## Build docker image từ Dockerfile
`sudo docker build -t <image_name> .`
E.g `sudo docker build -t ubuntu_nginx .`  ----> `docker images` to see the results

## Tạo container từ image.
`sudo docker run -v <forder_in_computer>:<forder_in_container> -p <port_in_computer>:<port_in_container> -it <image_name> /bin/bash`

- `-v`
Thể hiện việc mount volume, dữ liệu từ thư mục từ máy thật có thể được truy cập từ thư mục của máy ảo.

- `-p`
Cổng mạng từ máy thật để dẫn tới cổng mạng của máy ảo đang chạy.

- `-t`
Chạy container và mở terminal bằng /bin/bash

E.g `sudo docker run -p 9000:80 -it nginx /bin/bash`
`sudo docker run -v ~/Docker/webroot:/var/www/html -p 9000:80 -it nginx /bin/bash`