### Ingress Controller 的三种选择
- Nginx
- Traefik
- Envoy

---
- 创建密钥对象
```
kbc create secret tls tomcat-ingress-tomcat --cert=tls.crt --key=tls.key
```
