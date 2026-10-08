# Bài 3: Đóng gói trang web HTML tĩnh bằng Docker

## Các lệnh đã thực hiện

Di chuyển vào thư mục bài tập:

```bash
cd homework/session_09/ex3
```

Build image với tên `my-html-app:v1`:

```bash
docker build -t my-html-app:v1 .
```

Kết quả:

```text
[+] Building 3.2s (7/7) FINISHED
 => [internal] load build definition from Dockerfile
 => [internal] load metadata for docker.io/library/nginx:alpine
 => [1/2] FROM docker.io/library/nginx:alpine
 => [2/2] COPY index.html /usr/share/nginx/html/index.html
 => exporting to image
 => => naming to docker.io/library/my-html-app:v1
```

Khởi chạy container với tên `html-app` và ánh xạ cổng `8081` của máy vào cổng `80` của container:

```bash
docker run -d -p 8081:80 --name html-app my-html-app:v1
```

Kết quả:

```text
61ab46235fa56a2c5753ec95bff749df5b8c418a58a4246e102da47158810927
```

## Kiểm tra

```bash
curl http://localhost:8081
```

Kết quả:

```html
<h1>Hello Docker Session 09!</h1>
```

Kiểm tra container đang chạy:

```bash
docker ps --filter "name=html-app"
```

Kết quả:

```text
CONTAINER ID   IMAGE            COMMAND                  STATUS         PORTS                  NAMES
61ab46235fa5   my-html-app:v1   "/docker-entrypoint.…"   Up 1 minute    0.0.0.0:8081->80/tcp   html-app
```
