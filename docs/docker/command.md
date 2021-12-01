# 常用命令

- 查看版本号

  ```shell
  docker version
  ```

- 查看docker系统层面信息

  ```shell
  docker info 
  ```

- 从容器导出

  ```shell
  docker export -o [目标文件] [容器名称]
  ```

- 从容器导入

  ```shell
  docker import [目标文件] [容器名称]
  ```

- 从镜像导出

  ```shell
  docker save -o [目标文件] [镜像名称]
  ```

- 从镜像导入

  ```shell
  docker load -i [目标文件]
  ```

- 删除镜像

  ```shell
  docker rmi [镜像id]     //其中doss-api为关键字
  ```

- 批量删除镜像

  ```shell
  docker rmi --force `docker images | grep wms | awk '{print $3}'`   //其中wms关键字 print $3就是列出第三列 即镜像id
  ```

  
