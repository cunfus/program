# rsync

本地的资料常常需要同步到开发服务器。rsync 支持增量备份，这一点对开发者很友善。

```shell
$ rsync -av src remote:/folder/

# -a             递归同步文件元信息
# -v             传输日志显示到终端
# -n             模拟执行
# --delete       同步时，远程将删除本地中没有的文件
# --link-desk    指定基准目录，然后增量备份
# --exclude=path 同步时排除 path 文件夹
# ...
```

