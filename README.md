# filebrowser One-Click Installation Script

filebrowser is an open-source file management system that provides a simple and intuitive web interface for managing files. It allows users to access, upload, download, and edit files through a web browser, and also supports file sharing and permission management.

---

## Installation

- The **first parameter (`port`)** sets the service port. Make sure the same port is configured in NGINX.
- The **second parameter (`username`)** sets the username you want to register.  
  It must contain **only English letters** or **letters + numbers**.

```bash
bash <(curl -Ls https://raw.githubusercontent.com/Meokj/filebrowser/main/bash/install_filebrowser.sh) 8088 username
```

## Uninstallation

```bash
bash <(curl -Ls https://raw.githubusercontent.com/Meokj/filebrowser/main/bash/uninstall_filebrowser.sh)
```

## NGINX Configuration

```nginx
location ^~ / {
    proxy_pass http://127.0.0.1:8088/;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

    client_max_body_size 2G;      # Maximum size of a single uploaded file
    proxy_buffers 4 8k;           # 4 buffers of 8KB
    proxy_busy_buffers_size 8k;   # Allow up to 8KB memory usage

    sendfile on;                  # Improve file transfer performance
    tcp_nopush on;                # Optimize large file transfers
}
```

## Service Management Commands

| Action            | Command                                    |
|------------------|---------------------------------------------|
| Start service    | `sudo systemctl start filebrowser`          |
| Stop service     | `sudo systemctl stop filebrowser`           |
| Restart service  | `sudo systemctl restart filebrowser`        |
| Check status     | `sudo systemctl status filebrowser`         |
| View logs        | `sudo journalctl -u filebrowser -f`         |
| Enable on boot   | `sudo systemctl enable filebrowser`         |
| Disable on boot  | `sudo systemctl disable filebrowser`        |
