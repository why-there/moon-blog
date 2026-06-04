# 月亮加盐

个人博客，使用 [Hugo](https://gohugo.io/) 和 [Hextra](https://github.com/imfing/hextra) 主题构建。

访问地址：https://why-there.github.io/moon-blog/

## 本地开发

需要安装：[Hugo](https://gohugo.io/getting-started/installing/)（extended 0.156.0+）、[Go](https://golang.org/doc/install)、[Git](https://git-scm.com)

```shell
# 解析模块依赖
hugo mod tidy

# 启动本地服务器（端口 1313）
hugo server --logLevel debug --disableFastRender -p 1313
```
