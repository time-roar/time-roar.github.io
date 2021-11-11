

# SSH生成与多账号切换

## SSH生成

1. 对本地的git 设置Github用户

```shell
git config --global user.name "timeroar" 
git config --global user.email  "xxxxxx@qq.com"
```

2. 切换到user用户名下的.ssh路径

```shell
cd ～/.ssh
```

2. 生成 Rsa key

``` shell
ssh-keygen -t rsa -C "519451569@qq.com"
```

出现下文则表示输入你的ssh_key文件的名称

```shell
Enter file in which to save the key (/c/Users/51945/.ssh/id_rsa): 
```

下面则表示输入ssh key密码

```shell
Enter passphrase (empty for no passphrase):
```

3. 将生成public key放入gitHub

   - 访问github

   ```html
   https://github.com/
   ```

   - 进入setting
   - 左边列表选择SSH and GPGkeys
   - 点击New SSH key
   - 起个名字,复制你的key信息(右键生成的xx.pub,用记事本打开),注意不要复制错对应仓库的

   

5. 查验是否配置成功

```shell
ssh git@github.com
```

##	多账户切换

1. 执行ssh key生成命令,有几个账号生成几次 ,配置参考[SSH生成](#SSH生成)

   ```shell
   ssh-keygen -t rsa -C "你的邮箱"
   ```

2. 执行ssh添加,多个重复执行

   ```shell
   ssh-add 生成第二步的命名
   ```

   如果出现错误,例如:

   ```shell
   Could not open a connection to your authentication agent.
   ```

   请执行以下命令即可解决

   ```shell
   ssh-agent bash
   ```

   执行成功则会提示让你输入密码

   ```shell
   Enter passphrase for blog:
   ```

   密码验证成功后会提示田间成功并返回邮箱

   ```shell
   Identity added: blog (519451569@qq.com)
   ```

3. 查看是否添加成功

   ```shell
   ssh-add -l
   ```

   如果删除可执行

   ```shell
   ssh-add -D
   ```

4. 创建config

   ```shell
   touch config
   ```

5. 在config中添加如下信息

   ```shell
   Host timeroar.github.com
        HostName github.com
        PreferredAuthentications publickey
        User 66666655@qq.com
        IdentityFile ~/.ssh/blog
   Host time-roar.github.com
        HostName github.com
        PreferredAuthentications publickey
        User 66666666@qq.com
        IdentityFile ~/.ssh/doc
   ```

   - Host的第一排 则为你的host别名,用于第9步的修改替换
   - 第四排则为你用户邮箱路径
   - 第五排则为你ssh的路径

6. 取消全局global-config

   ```shell
   git config --global --unset user.name
   git config --global --unset user.email
   ```

7. 每个项目需要单独设置用户名邮箱

   ```shell
   git config  user.email "519451569@qq.com"
   git config  user.name "timeroar"
   ```

8. 查看是否成功,跟上面的有区别

   ```shell
   ssh -T git@timeroar.github.com
   ```

9. 本地使用时注意修改ssh路径为别名路径如:

   ```shell
   git@github.com:timeroar/timeroar.github.io.git
   ```

   变更为

   ```shell
   git@timeroar.github.com:timeroar/timeroar.github.io.git
   ```

