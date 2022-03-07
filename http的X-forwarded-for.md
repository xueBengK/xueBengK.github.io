# http的X-forwarded-for字段

### 一、字段作用

用来在多层代理的情况下追踪客户端源IP

### 二、 原理解析

当nginx在配置文件中配置了

```nginx
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
```

ingress-nginx配置了

```nginx
use-forwarded-headers: "true"
```

此时，该字段会记录每一次代理转发时候的TCP会话的发起方的IP，不断追加到字段末尾，以逗号分隔

X-forwarded-for: 客户端IP，代理服务器Aip，代理服务器Bip

后端程序就可以据此取到客户端IP进行一些校验判定

[1]: https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#use-forwarded-headers



