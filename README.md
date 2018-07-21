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