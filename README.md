# 基于3台MySQL的gilab集群

## 用法

1. 准备docker环境

1台

2. 启动

`docker-compose up -d`

等待启动完成

3. 登录集群中一台机器

`docker-compose exec mysql1 /bin/bash`

4. 更改root密码

随机密码在log中，搜`password`

`ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass';`

5. 检查集群运行状态

`ndb_mgm`

会看到

```
bash-4.2# ndb_mgm
-- NDB Cluster -- Management Client --
ndb_mgm>
```

输入`show`

会看到

```
bash-4.2# ndb_mgm
-- NDB Cluster -- Management Client --
ndb_mgm> show
Connected to Management Server at: 192.168.0.2:1186
Cluster Configuration
---------------------
[ndbd(NDB)]     2 node(s)
id=2    @192.168.0.3  (mysql-5.7.24 ndb-7.6.8, Nodegroup: 0, *)
id=3    @192.168.0.4  (mysql-5.7.24 ndb-7.6.8, Nodegroup: 0)

[ndb_mgmd(MGM)] 1 node(s)
id=1    @192.168.0.2  (mysql-5.7.24 ndb-7.6.8)

[mysqld(API)]   1 node(s)
id=4    @192.168.0.10  (mysql-5.7.24 ndb-7.6.8)

ndb_mgm>
```

启动完毕