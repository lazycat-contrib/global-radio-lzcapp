# Global Radio for LazyCat

将 [GlobalRadio](https://github.com/moli-xia/global-radio)（全球电台）打包为 LazyCat LPK v2。

一个基于 Vue 3 + Vite 的在线电台应用：电台搜索（支持中文）、播放控制、收藏与播放历史、睡眠定时器、亮暗主题与多语言界面，并支持作为 PWA 安装。

## 镜像来源

上游在 Docker Hub 发布镜像，本应用直接使用，不需要重新构建：

- 上游镜像：`superneed/global-radio:latest`
- 运行镜像：`docker.1ms.run/superneed/global-radio:latest`（Docker Hub 默认加速）
- 镜像为 nginx 托管的纯静态站点，监听容器内 `80`，单架构 `linux/amd64`

上游只发布 `latest` 可变 tag，没有版本 tag，因此本仓库跟踪该 tag 的 digest：digest 不变则跳过，digest 变化时递增 patch 版本并重新发布。

## 数据

纯静态应用，没有后端与数据库。收藏、播放历史与主题偏好保存在浏览器本地，更换浏览器或清理数据会丢失。

## 本地构建

```bash
lzc-cli project build -o dist/application.lpk
lzc-cli lpk info dist/application.lpk
```

## 自动发布

`.github/workflows/lazycat.yml` 使用 `ca-x/lazycat-github-action` 跟踪镜像 digest，创建版本化 GitHub Release Asset 并只发布到喵喵私有商店。需要为仓库配置 `APPSTORE_URL`、`APPSTORE_TOKEN`，以及可选的 `APP_ID`、`PRIVATE_STORE_GROUP_CODES`。

## 许可

MIT（上游）