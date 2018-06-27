# ZooKeeper分布式专题与Dubbo微服务入门

### 1 ZooKeeper Watch:
#### 1-1 事件类型
##### 父节点：
- `NodeCreated`
- `NodeDataChanged`
- `NodeDeleted`
##### 子节点
- `NodeChildrenChanged`
  > 子节点的新增和删除都触发NodeChildrenChanged事件<br>
  > 子节点的修改不触发任何事件<br>
  > 针对子节点去修改，要把子节点当做父节点才能绑定事件
#### 1-2 watch使用场景

- 统一资源配置
![统一资源配置](https://github.com/WangPingChun/imooc-learn/blob/master/zookeeper/note/images/watch-统一资源配置.png?raw=true)

### 2 ZooKeeper ACL:
#### 2-1 命令行
- `getAcl`:获取某个节点的acl权限信息
- `setAcl`:设置某个节点的acl权限信息
- `addauth`:输入认证授权信息，注册时输入明文密码（登录）但在zk的系统里，密码 是以加密的形式存在的
#### 2-2 ACL的构成
##### zk的acl通过「scheme:id:permissions」来构成权限列表
- `scheme`:代表采用的某种权限机制
- `id`:代表允许访问的用户
- `permissions`:权限组合字符串

##### scheme和id
1. `world`: world下只有一个id，即只有一个用户，也就是anyone，那么组合的写法就是`world:anyone:[permissions]`
2. `auth`:代表认证登录，需要注册用户有权限就可以,形式为`auth:user:password:[permissions]`
3. `digest`:需要对密码加密才能访问，组合形式为`digest:username:BASE64(SHA1(password)):[permissions]`
> auth与digest的区别就是，前者明文，后者密文<br>
> `setAcl /path auth:lee:lee:cdrwa`
> `setAcl /path digest:les:BASE64(SHA1(lee)):cdrwa`</br>
> 上面两个操作是等价的，在通过`addauth digest lee:lee`后都能操作指定节点的权限
4. `ip`:当设置为ip指定的ip地址，此时限制ip进行访问，比如`ip:192.168.1.1:[permissions]`
5. `super`:代表超级管理员，拥有所有权限
##### permissions
1. `CREATE`:创建子节点
2. `READ`:获取节点/子节点
3. `DELETE`:删除子节点
4. `WRITE`:设置节点数据
5. `ADMIN`:设置权限

#### 2-3 ACL的常用使用场景
- 开发/测试环境分离，开发者无权操作测试库的节点，只能看
- 生产环境上控制指定ip的服务可以访问相关节点，防止混乱

### 3 ZooKeeper Four Letter Words:
#### 3.1 简介
- zk可以通过它自身提供的简写命令来和服务器进行交互
- 需要使用到nc命令，需要安装:yum install nc
- echo [command] | nc [ip] [port]

#### 3.2 Four Letter Words
1. `stat`:查看zk的状态信息，以及mode
    > `echo stat | nc localhost 2181`
    > ![](https://github.com/WangPingChun/imooc-learn/blob/master/zookeeper/note/images/flw-stat.png?raw=true)