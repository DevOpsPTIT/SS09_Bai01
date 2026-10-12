# BÁO CÁO BÀI 1: Kiểm tra cài đặt Docker Engine và chạy Container Hello-World

**Họ và tên:** [Điền tên]  
**Ngày thực hiện:** 2026-10-12

---

## Mục tiêu

Thực hành chạy các lệnh kiểm tra phiên bản Docker CLI và khởi chạy container đầu tiên trên máy cá nhân.

---

## 1. Lệnh `docker version`

```bash
$ docker version
```

**Kết quả:**

```
Client:
 Version:           27.5.1
 API version:       1.47
 Go version:        go1.22.11
 Git commit:        9f9e405
 Built:             Wed Jan 22 13:37:36 2025
 OS/Arch:           linux/amd64
 Context:           default

Server: Docker Engine - Community
 Engine:
  Version:          27.5.1
  API version:      1.47 (minimum version 1.24)
  Go version:       go1.22.11
  Git commit:       4c9b3b0
  Built:            Wed Jan 22 13:37:36 2025
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.7.25
  GitCommit:        bcc810d6b9066471b0b6fa75f557a15a1cbf31bb
 runc:
  Version:          1.2.4
  GitCommit:        v1.2.4-0-g6c52b3f
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
```

**Giải thích:**
- Lệnh `docker version` hiển thị thông tin phiên bản của Docker Client và Docker Server (Engine).
- Kết quả cho thấy cả Client và Server đều đang chạy phiên bản 27.5.1, xác nhận Docker Engine đã được cài đặt thành công.

---

## 2. Lệnh `docker info`

```bash
$ docker info
```

**Kết quả:**

```
Client:
 Version:    27.5.1
 Context:    default
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.20.0
  compose: Docker Compose (Docker Inc.)
    Version:  v2.32.4

Server:
 Containers: 1
  Running: 0
  Paused: 0
  Stopped: 1
 Images: 1
 Server Version: 27.5.1
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Using metacopy: false
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: systemd
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: bcc810d6b9066471b0b6fa75f557a15a1cbf31bb
 runc version: v1.2.4-0-g6c52b3f
 init version: de40ad0
 Kernel Version: 5.15.167.4-microsoft-standard-WSL2
 Operating System: Ubuntu 24.04.1 LTS
 OSType: linux
 Architecture: x86_64
 CPUs: 12
 Total Memory: 7.592GiB
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false
```

**Giải thích:**
- Lệnh `docker info` hiển thị thông tin chi tiết về hệ thống Docker bao gồm: số container, số image, storage driver, logging driver, kernel version, OS,...
- Kết quả xác nhận Docker Daemon đang hoạt động và kết nối thành công không cần `sudo`.

---

## 3. Lệnh `docker run hello-world`

```bash
$ docker run hello-world
```

**Kết quả:**

```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
e6590344b1a5: Pull complete
Digest: sha256:d715f14f9eca81473d9112df50457893aa7a0a5e23d9dbf9b3c3ce3b44a3b4b2
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

**Giải thích:**
- Docker Client gửi yêu cầu tới Docker Daemon.
- Docker Daemon kiểm tra image `hello-world` trên máy local, không tìm thấy nên tự động pull từ Docker Hub.
- Docker Daemon tạo container mới từ image đó và chạy chương trình bên trong.
- Kết quả xuất hiện dòng **"Hello from Docker! This message shows that your installation appears to be working correctly."** → Xác nhận Docker hoạt động chính xác.

---

## Kết luận

- ✅ Docker Engine đã được cài đặt thành công.
- ✅ Docker CLI hoạt động bình thường, kết nối được tới Docker Daemon mà không cần `sudo`.
- ✅ Container `hello-world` chạy thành công, xác nhận toàn bộ pipeline Docker (Client → Daemon → Hub → Container) hoạt động đúng.

---

## Ghi chú

- Nếu gặp lỗi phân quyền khi chạy lệnh Docker, có thể thêm user vào group `docker`:
  ```bash
  sudo usermod -aG docker $USER && newgrp docker
  ```
- Sau khi thêm, cần logout và login lại hoặc chạy `newgrp docker` để áp dụng thay đổi.
