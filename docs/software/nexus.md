# Nexus安装

## docker环境

1. 拉取镜像

   ```shell
   docker pull sonatype/nexus3
   ```

2. 创建数据文件挂在目录

   ```shell
   mkdir -vp /opt/nexus/datas
   ```

3. 运行docker

   ```shell
   docker run -d --name nexus3 -p 18081:8081 -v /opt/nexus/datas:/var/nexus-data sonatype/nexus3
   ```

4. 查看admin密码

   - 进入交互模式

   ```shell
   docker exec -it [container_id] /bin/bash
   ```

   - 查看密码

   ```shell
   vi /nexus-data/admin.password
   ```

   

   

