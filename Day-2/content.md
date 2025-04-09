# 🌐 NGINX Web Server - Deep Dive (8 April 2025)

## 🕸️ History

- **NGINX** was developed by *Igor Sysoev* to solve the C10k problem.
- It’s capable of handling **hundreds of thousands of concurrent connections**.
- Powers over **50% of the busiest websites** in the world.
- It’s an open-source solution for:
  - Web serving
  - Reverse proxying
  - Caching
  - Load balancing
  - Media streaming
  - Email proxying (IMAP, POP3, SMTP)

> **NGINX is lightweight and high-performance.**

---

## 🚨 Why NGINX?

- Created to be the **fastest web server** with efficient handling of large concurrent requests.
- Frequently used as a **reverse proxy** and **load balancer**.
- **Software-based** — more flexible and cost-effective than hardware balancers.
- Supports **microservices**, **HTTP/2**, **Docker**, and many **third-party libraries**.
- Example:  
  ```bash
  docker run nginx:1.27.0
  ```

---

## 📈 NGINX vs Apache

| Feature               | Apache                          | NGINX                             |
|-----------------------|----------------------------------|-----------------------------------|
| Architecture          | Process/thread-based             | Event-driven, async (non-blocking)|
| Module Integration    | Easy insertion via .htaccess     | Must be efficient, no blocking    |
| Performance           | Great for low-traffic sites       | Great for high-traffic sites      |
| Dynamic Content       | Native support                   | Uses external like PHP-FPM        |
| Static Content Speed  | Slower (2.5x less than NGINX)    | Extremely fast                    |
| Directory Overrides   | Supports .htaccess               | No per-directory override         |

---

## 💻 Installing NGINX (APT)

```bash
sudo apt update
sudo apt install -y nginx
ps aux | grep nginx
sudo systemctl status nginx
ls -l /etc/nginx
cat /etc/nginx/nginx.conf
```

---

## 🧑‍💻 Installing NGINX from Source

1. Launch an EC2 instance (Ubuntu)
2. Download source:
   ```bash
   wget http://nginx.org/download/nginx-<version>.tar.gz
   ```
3. Install dependencies:
   ```bash
   apt-get install build-essential libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev make
   ```
4. Compile and install:
   ```bash
   ./configure --sbin-path=/usr/bin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-pcre --pid-path=/var/run/nginx.pid --with-http_ssl_module
   make
   make install
   nginx -v
   nginx
   ```

---

## ➕ Add NGINX to Systemd

- Create a systemd unit file `/lib/systemd/system/nginx.service`
- Enable with:
  ```bash
  sudo systemctl enable nginx
  sudo systemctl status nginx
  ```

---

## 🚀 HTTP Status Codes Cheat Sheet

### ✅ 2xx – Success
- `200 OK`: Everything's working.
- `201 Created`: Resource created.
- `204 No Content`: No response body.

### 🔁 3xx – Redirection
- `301 Moved Permanently`
- `302 Found`
- `304 Not Modified`

### ❌ 4xx – Client Errors
- `400 Bad Request`
- `401 Unauthorized`
- `403 Forbidden`
- `404 Not Found`
- `405 Method Not Allowed`
- `429 Too Many Requests`

### 💥 5xx – Server Errors
- `500 Internal Server Error`
- `502 Bad Gateway`
- `503 Service Unavailable`
- `504 Gateway Timeout`

---

## ✊ Configuration Structure

### Contexts & Directives

- **Main Context**
  - Global: `user`, `worker_processes`, `pid`, etc.
- **Events Context**
  - `worker_connections`, connection handling.
- **HTTP Context**
  - Web handling: gzip, access log, SSL, etc.
- **Server Context**
  - Virtual hosts, listen, server_name, root.
- **Location Context**
  - URI pattern matching, request control.
- **Upstream Context**
  - Load balancing backends.
- **Mail Context**
  - Email proxying.

```nginx
http {
  server {
    listen 80;
    server_name example.com;
    location / {
      root /var/www/html;
    }
  }
}
```

---

## 🧪 Lab – Serve Static Files with MIME Types

Fix missing `.css` or `.js` rendering:

```nginx
http {
  include mime.types;
  server {
    listen 80;
    root /bloggingtemplate/;
  }
}
```

Check and reload:
```bash
nginx -t
nginx -s reload
```

---

## 🧪 Lab – Location Context

```nginx
server {
  listen 80;
  root /bloggingtemplate/;

  location /contactus {
    return 200 "Hello, this is the Custom Page";
  }
}
```

**Matching Types:**
- `=` Exact match
- `~` Case-sensitive regex
- `~*` Case-insensitive regex
- `^~` Preferential match

**Priority:**
1. Exact match
2. Prefix match
3. Regex match

---

## 🧮 NGINX Variables

Use `set` to define and access variables:

```nginx
set $a "hello world";
location /find {
  return 200 "$hostname 
 $args 
 $nginx_version";
}
```

---

## 🔁 Rewrite and Redirect

```nginx
location /welcome {
  return 301 /assets/images/about/welcome-banner.jpg;
}

rewrite ^/guest/(\w+) /welcome/$1;
```

---

## 📂 try_files Directive

Check for multiple paths:

```nginx
location /testobject {
  try_files $uri /assets/images/about/profile_image.jpg /video;
}
```

---

## 📝 Logging

Default logs:
- `/var/log/nginx/error.log`
- `/var/log/nginx/access.log`

View live:
```bash
cd /var/log/nginx
tail -f *
```

Empty logs:
```bash
> access.log
> error.log
```

---

## 🧠 Final Thoughts

This is a comprehensive NGINX journey — from installation to advanced configuration. Whether you're debugging 403s, configuring MIME types, or rewriting routes, NGINX offers robust, scalable performance.

> Stay curious. Keep experimenting. NGINX is just the beginning.
