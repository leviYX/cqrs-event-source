# 1、简介
使用pg作为write_source,使用es作为read_source，通过kafka作为事件驱动来实现cqrs+event_source的内容。


# 2、组件启动
## 2.1、启动kafka集群
~~~markdown
# 1、项目的docker-compose目录下有一个[docker-compose.yml](docker-compose/docker-compose.yml)文件
可以用来启动kafka集群。docker-compose -f docker-compose.yml  up -d
~~~