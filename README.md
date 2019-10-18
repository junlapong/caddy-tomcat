# Caddy Server with Tomcat

## Objective

- เพื่อวางสถาปัตยกรรมของระบบ ให้เป็นแบบ Web App สำหรับ Java Web Application
- สามารถใช้งานได้ทั้ง platform ที่เป็น Windows และ Unix
- รองรับการทำ run system service - see [caddy-service](https://github.com/hacdias/caddy-service)
- รองรับการทำ [logging](https://caddyserver.com/v1/docs/log) โดยให้ Web Server ทำหน้าที่นี้ ไม่ต้องแก้ไข Application Server
- รองรับการ cache static contents
- รองรับการใช้ https
- กำหนด config เกี่ยวกับ Web Security โดยกระทบกับการแก้ไข Java App น้อยที่สุด

## Structure

caddy server
tomcat หรือ spring boot application

## Caddy Server

### Download

- https://caddyserver.com/v1/download
- [Windows 64-bit](https://caddyserver.com/download/windows/amd64?plugins=hook.service,http.cache,http.cors,http.minify,http.ratelimit,http.realip&license=personal&telemetry=off)
- [macOS](https://caddyserver.com/download/darwin/amd64?plugins=hook.service,http.cache,http.cors,http.minify,http.ratelimit,http.realip&license=personal&telemetry=off)

```
curl https://getcaddy.com | bash -s personal hook.service,http.cache,http.cors,http.minify,http.ratelimit,http.realip
```

### Configuration

Caddyfile

```
localhost 127.0.0.1   # Your site's address

ext .html   # Clean URLs
errors error.log {       # Error log
    404 html/error-404.html   # Custom error page
    503 html/error-50x.html
}

# API load balancer
proxy /app localhost:8080 localhost:8081
```

### Run

```
$ cd caddy
$ ./caddy
Activating privacy features... done.

Serving HTTP on port 80 
http://localhost
```

## Tomcat

