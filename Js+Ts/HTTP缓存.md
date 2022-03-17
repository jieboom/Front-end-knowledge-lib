#####缓存控制
缓存控制
1. 依据新鲜度, cache-control:max-age  modified   是否强制缓存

缓存验证
2. 缓存不新鲜则在使用etag if none match  / last-modified   校验文件是否新鲜

#### 常见状态码 
成功 200 success  204  no-content  206 partial content 返回部分内容 可用于断点续传 
重定向相关 301 moved permanently 304 not modified
客户端问题 400 bad request 401 unauthorized(认证信息丢失) 403 forbidden(没有权限) 404 not found
服务器问题  500 服务器报错不知道哪里出问题  502 网关错误 503 服务器不能处理请求,宕机或者维护中