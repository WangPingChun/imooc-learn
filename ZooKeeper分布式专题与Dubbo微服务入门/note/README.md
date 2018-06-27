# ZooKeeper分布式专题与Dubbo微服务入门

### ZooKeeper Watch:
#### 一.事件类型
##### 父节点：
- `NodeCreated`
- `NodeDataChanged`
- `NodeDeleted`
##### 子节点
- `NodeChildrenChanged`
  > 子节点的新增和删除都触发NodeChildrenChanged事件<br>
  > 子节点的修改不触发任何事件<br>
  > 针对子节点去修改，要把子节点当做父节点才能绑定事件
  

#### 二.watch使用场景

- 统一资源配置
![统一资源配置](images\watch-统一资源配置.png)

  
  