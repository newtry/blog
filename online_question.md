## 异常
Failed to save registry store file, cause: Can not l       ock the registry cache file /root/.dubbo/dubbo-registry-zk.infra.middleware.xueleyun.com.cache, ignore and retry later, maybe multi java process use the file, please config:        dubbo.registry.file=xxx.properties, dubbo version: service, current host: 192.168.8.50

Dubbo在保存服务列表时失败，拿不到文件锁，无法保存服务列表。
Dubbo通过注册中心发现服务，发现的服务Dubbo同时也会保存到本地缓存一份，缓存的好处有很多，比如不需要每次使用的时候都通过注册中心获取，注册中心不可用了，不影响消费端的调用，因为本地缓存了一份服务提供者列表。

导致：dubbo每次去注册中心去取服务列表。
解决方案：在启动脚本里面添加配置（指定缓存的保存文件）： -Ddubbo.registry.file=/home/newad/.dubbo/dubbo-registry-Order-0.cache

