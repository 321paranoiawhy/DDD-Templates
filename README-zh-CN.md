# 领域驱动设计模板

特点:

- 严格遵循领域驱动设计
- 纯净, 尽可能少地引入三方插件、包、库等, 除非已是社区公认最佳实践

领域驱动设计四层:

- `Presentation Layer`
- `Application Layer`
- `Domain Layer`
- `Data Layer`

![](https://codewithandrea.com/articles/flutter-app-architecture-domain-model/images/flutter-app-architecture.webp)

## 项目整体架构

- `frontend` 包括以下前端框架
  - `Angular`
  - `Electron`
  - `Flutter`
  - `KMP`
  - `Next`
  - `Nuxt`
  - `React`
  - `React Native`
  - `UniAPP`
  - `Vue`
- `backend`
- `docs` 文档
- `cli` 脚手架, 计划使用 `` 编写
- `ide-plugins`, 用于编写 `IDE` 插件, 计划支持以下主流 `IDE`:
    - `VS Code`
    - `Jetbrains IDE`

## Core Features

- `Restful`: `GET`、`POST`、`PUT`、`DELETE`
- `Microservice` 微服务
- `Websocket`
- `gRPC`
- `SSE` server-sent events
- `Cron` 定时任务
- `Message Queue` 消息队列
- `Cache` 缓存
- `Authentication & Authorization`
- `Validation & Verfication` 入参校验
- `File Upload` 文件上传
- `Serve Static Files` 静态文件服务
- `Version Control` 版本控制
- `Documentation` 接口文档, 可使用 `Swagger`、`Apifox` 等工具
- `Tests` 接口测试: 自动化测试、压力测试 (压测)、性能测试等
- `Containerize` 容器化, 支持 `Docker` 和 `k8s` 一键启动和部署
- `Monitor` 监控, 服务监控
- `Logging` 日志, 可集成 `ELK`
- `Rate Limit` 接口限流
- `Load Balancer` 负载均衡
- `CORS` 跨域配置
- `CSRF`
- `Security`
- `Mock` 模拟数据
- `Pagination` 列表分页
- `I18n` 国际化, 通过请求头 `X-Language` 返回相应的数据、错误提示等, 也可考虑使用 `BFF`

## `ORM` or `pure SQL`

## `Layer First` or `Feature First`

`Layer First`:

```txt
‣ presentation
  ‣ feature1
  ‣ feature2
‣ application
  ‣ feature1
  ‣ feature2
‣ domain
  ‣ feature1
  ‣ feature2
‣ data
  ‣ feature1
  ‣ feature2
```

`Feature First`:

```txt
‣ features
  ‣ feature1
    ‣ presentation
    ‣ application
    ‣ domain
    ‣ data
  ‣ feature2
    ‣ presentation
    ‣ application
    ‣ domain
    ‣ data
```

## 响应体压缩

可使用以下压缩方式压缩响应体:

- `gzip`
- `br`
- `deflate`
- `zstd`

其中, `gzip` 使用最为广泛、兼容性也最好

## 统一接口响应数据格式

成功示例:

```json
{
  "code": 200,
  "message": "OK",
  "data": [],
  "timestamp": 1660926758875,
  "time": 200,
  "path": "/api/v1/login"
}
```

失败示例:

- `code` 接口内部状态码, 可根据实际业务而定, 可将 `HTTP` 请求状态码设为 `200`, 而在此处返回 `200`/`201`/`400`/`401`
- `message` 消息提示
- `data` 核心数据
- `timestamp` `13`位毫秒级时间戳
- `time` 接口耗时, 单位为 `ms`, 建议关键接口耗时压到 `200ms` 内, 复杂接口可适当予以放宽
- `path` 请求路径

获取毫秒级时间戳

`js`:

```js
// 以下三种结果一致, 均为毫秒级时间戳
const timestamp1 = new Date().getTime();
const timestamp2 = Date.now();
const timestamp3 = new Date().valueOf();
```

`dart`:

```dart
void main() {
  print(DateTime.now().millisecondsSinceEpoch);
}
```
