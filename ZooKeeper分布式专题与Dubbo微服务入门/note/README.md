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
![统一资源配置](https://raw.githubusercontent.com/WangPingChun/imooc-learn/master/ZooKeeper%E5%88%86%E5%B8%83%E5%BC%8F%E4%B8%93%E9%A2%98%E4%B8%8EDubbo%E5%BE%AE%E6%9C%8D%E5%8A%A1%E5%85%A5%E9%97%A8/note/images/watch-%E7%BB%9F%E4%B8%80%E8%B5%84%E6%BA%90%E9%85%8D%E7%BD%AE.png)

  
  