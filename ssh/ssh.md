# ssh

---

## ssh 免密登录

---

生成密钥：

```sh
ssh-keygen -t rsa -C email@example.com
```

拷贝公钥到服务器：

```sh
ssh-copy-id -i ~/.ssh/id_rsa.pub user@host
```

如何没有 `ssh-copy-id` 命令，可以执行以下操作：

在客户机上把公钥拷贝到服务机。

```sh
scp ~/.ssh/id_rsa.pub user@host:~/.ssh
```

在服务机上把公钥追加到 authorized_keys 中，如果没有 authorized_keys 文件需要自己创建。

```sh
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```

禁用密码登录：

在 `/etc/ssh/ssh_config` 文件中添加以下配置：

```sh
PasswordAuthentication no
UsePAM no
ChallengeResponseAuthentication no
```
