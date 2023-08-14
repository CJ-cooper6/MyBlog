# Hero 常用命令

- `hexo generate`：在`public`目录中生成静态网页文件
- `hexo clean`：清空缓存和`public`目录，遇到一些问题时可以尝试运行此命令
- `hexo server`：启动预览服务器（实时更新，刷新网页即可）
- `hexo deploy`：从`_config.yml`中读取设置部署至远程站点，详情等到下一篇讲
- `hexo new "My New Post"`：在`./source/_posts`中创建新文章，引号内写标题，也可以选择不使用此命令自己手动新建文件



发布三连：

```go
hexo clean
hexo generate
hexo deploy
```





#### Butterfly 主题页面

标题 分类 标签  图库

https://butterfly.js.org/posts/dc584b87/