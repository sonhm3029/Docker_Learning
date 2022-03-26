# Docker note


# Table of contents

- [Docker note](#docker-note)
  - [1. Xem các image hiện có:](#1-xem-các-image-hiện-có)
  - [2. Tải image từ trên Docker Hub về](#2-tải-image-từ-trên-docker-hub-về)
  - [3. Xóa image hiện có trên máy](#3-xóa-image-hiện-có-trên-máy)
  - [4. Chạy container với image hiện có trên máy](#4-chạy-container-với-image-hiện-có-trên-máy)
  - [5. Thoát khỏi container khi đang chạy](#5-thoát-khỏi-container-khi-đang-chạy)
  - [6. Xem danh sách container đang chạy](#6-xem-danh-sách-container-đang-chạy)
  - [7. Vào lại container đang chạy](#7-vào-lại-container-đang-chạy)
  - [8. Xóa container](#8-xóa-container)
  - [9. Chạy lại một container đã dừng/ dừng một container đang chạy](#9-chạy-lại-một-container-đã-dừng-dừng-một-container-đang-chạy)
  - [10. Chạy lệnh của container khi đang không trong container đang chạy:](#10-chạy-lệnh-của-container-khi-đang-không-trong-container-đang-chạy)
  - [11. Lưu container thành image với commit](#11-lu-container-thnh-image-vi-commit)
  - [12. Lưu image ra file với docker save](#12-lưu-image-ra-file-vơi-docker-save)
  - [13. Nạp image vào docker từ 1 file](#13-nạp-image-vào-docker-từ-1-file)
  - [14. Ánh xạ thư mục máy host vào container](#14-ánh-xạ-thư-mục-máy-host-vào-container)


Các lệnh:

## 1. Xem các image hiện có:

```cmd
docker images
```

## 2. Tải image từ trên Docker Hub về

```cmd
docker pull image:tag
```

Với `image` là tên image public trên docker hub, `tag` là tên version xem trên docker hub. Nếu không có `:tag` thì mặc định sẽ pull về bản mới nhất ( tương đương vs `:latest`)

Có thể tìm các image hiện có trên Docker Hub bằng cách lên web xem hoặc gõ lệnh

```cmd
docker search image_name
```

Tìm kiếm image có tên `image_name`.

## 3. Xóa image hiện có trên máy

```cmd
docker image rm imagename
```

`imagename` là tên của image, nếu có nhiều verion (nhiều tag thì thêm `imagename:tag`). Có thể thay `imagename` bằng `imageID` ( Xem trên cmd bằng lệnh `docker images`).

**Chú ý :** Nếu không xóa được image bằng id thì dùng `ten:tag` có thể hoạt động được.s

## 4. Chạy container với image hiện có trên máy

```cmd
docker run -it --name NAME -h HOST image
```

Với `-it` là kết hợp của `-i` (tương tác với image) `-t` (terminal của image). `NAME` là define tên của container, `HOST` là define tên của host và `image` là tên image dùng.

Chú ý có thể thay tên image bằng id của nó (id chỉ cần chỉ ra một bộ phận, không cần phải tất cả id). 

**Có thể dùng lệnh :**

```cmd
docker run -it --name NAME --rm -h HOST image
```

Tham số `rm` được thêm vào sẽ xóa container  ngay sau khi ta thoát, không dùng container nữa.

## 5. Thoát khỏi container khi đang chạy

tổ hợp phím `Ctrl P Q`

## 6. Xem danh sách container đang chạy

```cmd
docker ps
```

Xem tất cả các container, cả đang chạy lẫn đã dừng

```cmd
docker ps -a
```

## 7. Vào lại container đang chạy

```cmd
docker attach container
```

`container` là tên container (do mình đặt hoặc mặc định được tự đặt, xem bằng lệnh `docker ps` hoặc `docker ps -a`). Có thể thay tên bằng id của container.

## 8. Xóa container

```cmd
docker rm container
```

`container` là tên hoặc id của container cần xóa.

`container` là tên container hoặc id

Có thể xóa nhiều container cùng 1 lúc bằng cách sau

```cmd
docker rm container1 container2...
```

Với `container1`, `container2` là chỉ định của từng container, mỗi chỉ định cách nhau một dấu cách.

**Nếu như container muốn xóa đạng chạy thì dùng lệnh**

```cmd
docker rm container -f
```

Với `-f` có nghĩa là force (buộc dừng)

## 9. Chạy lại một container đã dừng/ dừng một container đang chạy

Đầu tiên nên `docker ps -a` để xem tất cả container.

`docker start container_id` để chạy container có id là `container_id`.

- Để dừng một container đang chạy:

```cmd
docker stop container_id
```

Với `container_id` là id của container đang chạy cần dừng.

## 10. Chạy lệnh của container khi đang không trong container đang chạy:

```cmd
docker exec container_name/container_id lenh
```

Hoặc 

```cmd
docker exec -it container_name/container_id lenh
```

Lệnh trên tương đương với `attach` container và chạy lệnh trong container.

## 11. Lưu container thành image với commit

```cmd
docker commit ten/id_container ten_image:tag
```

Lưu container với `ten` hoặc `id` thành image có tên `ten_image` với tag là `tag`.

## 12. Lưu image ra file với docker save

```cmd
docker save --ouput tenfile.tar id/ten_image
```

`tenfile.tar` là tệp `.tar` tên là `tenfile` hoặc có thể để `.zip`

`id/ten_image` là id hoặc tên của image cần lưu

## 13. Nạp image vào docker từ 1 file

```cmd
docker load -i tenfile
```

Có thể khi load vào, gõ `docker images` không ra image mới được nạp vào (do không chỉ ra tên và tag của image)

Ta có thể thêm tên vào tag lúc nạp vào xong như sau:

```cmd
docker tag image_id ten:tag
```

Trong đó `image_id` là id của image vừa nạp vào. `ten:tag` là tên và tag ta set cho image.

## 14. Ánh xạ thư mục máy host vào container

```cmd
docker run -it -v pathHost:pathContainer imageid
```

Trong đó `pathHost` là đường dẫn đến thư mục của máy chính đang chạy. `pathContainer` là đường dẫn đến thư mục muốn ánh xạ thư mục từ máy chính vào của container.

**Chú ý đường dẫn trên window:**

**Ví dụ:**

```cmd
docker run -it -v C:/User/pC/OneDrive/Desktop/test:/home/test
```

Ở đây `C:/User/pC/OneDrive/Desktop/test` là đường dẫn trên máy chính ( chú ý để `/` thay vì `\`). `/home` là đường dẫn trên container.

Một khi đã kết nối thì việc thay đổi trong thưc mục ở cả hai phía là như nhau. (cả 2 đều cùng thay đổi).

## 15. Chia sẻ dữ liệu ánh xạ từ máy chính vào container này đến container khác

```cmd
docker run -it --volumes-from tenContainer imageID
```

Câu lệnh trên tạo ra một container mới đc phép lấy dữ liệu từ container có tên `tenContainer`, ta có thể dùng `id` của container cũng đc. Container được tạo ra bởi image có `imageID`...

## 16. Xem, tạo các ổ đĩa để cho vào container, làm việc.

### Xem docker đang có ổ đĩa nào:

```cmd
docker volume ls
```

### Tạo ổ đĩa

```cmd
docker volume create tenODia
```

Tạo ra ổ đĩa với tên `tenODia` trong docker.

### Kiểm tra thông tin ổ đĩa

```cmd
docker volume inspect tenODia
```

### Xóa ổ đĩa

```cmd
docker volume rm tenODia
```

### Gán ổ đĩa vào container

```cmd
docker run -it --name tenContainer --mount source=tenODia,target=pathContainer imageID
```

Câu lệnh trện sẽ tạo ra một container có tên là `tenContainer`, trong container đã được mount vào ổ đĩa tên là `tenODia` với đường dẫn đến ổ đĩa trong container là `pathContainer`. Container được tạo ra từ image có id là `imageID`.

Chú ý khi làm việc với ổ đĩa trong container, khi xóa container, dữ liệu trong ổ đĩa và ổ đĩa vẫn tồn tại. Giống như việc sử dụng ánh xạ dữ liệu từ máy chính vào container.

**Chú ý**: Việc gán ổ đĩa vào container chỉ có thể được thực hiện khi bắt đầu khởi tạo container. Nếu muốn gán ổ đĩa vào một container đã được tạo từ trước thì cần `commit` container đó lại thành một image, Rồi khởi tạo một container mới từ ổ đĩa cần gán và image là container cũ đã được `commit`.

Để gán vào nhiều ổ đĩa:

```cmd
docker run -it --name tenContainer --mount source=tenODia1,target=pathContainer1 --mount source=tenODia2,target=pathContainer2 imageID
```

### Tạo ổ đĩa ánh xạ vào thư mục trên máy chính

```cmd
docker create --opt device=pathHOST --opt type=none --opt o=bind DISKNAME
```

Đối với loại ổ đĩa này thì không thể gán cho container bằng tham số `--mount` mà dùng như sau:

```cmd
docker run -it -v DISKNAME:pathContainer imageId
```

## 17. Docker Network

### Xem docker đang có các mạng nào

```cmd
docker network ls
```

Mặc định thì các container trong docker sẽ được kết nối tới mạng `bridge`

![img](./img/network_1.png)


### Xem mạng có những container nào đang kết nối đến.

```cmd
docker network inspect tenMang
```

Kết quả trả về ví dụ:

![network_2](./img/network_2.png)

### Xem container kêt nối đến mạng nào

```cmd
docker inspect tenContainer
```

![network_3](./img/network_3.png)

![network_4](./img/network_4.png)

Xem [Ví dụ](./example/network_busybox) nhỏ về kết nối các container trong cùng mạng với busybox


### Ánh xạ cổng port từ mạng này sang mạng trong docker.

Ví dụ ánh xạ port 80 sang port 8888 của localhost

![busy_7](./img/bust_7.png)
![busy_8](./img/busy_8.png)
![busy_9](./img/busy_9.png)