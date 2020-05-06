# dailyfresh
B2B by Django3.0.5

黑马程序员Django练习项目重构到到新版本Django3.0.5
## 用户
- ### 用户注册
    - 注册用户后发送激活邮件, 点击激活邮件里面对应的网页链接可激活账户
    - 激活链接的身份标识用itsdangerous的TimedJSONWebSignatureSerializer加密
    - celery任务队列来发送激活邮件(我的是在window使用，有报错但能正常运行), redis作为中间人
- ### 用户登录
    - 使用自带的user认证系统
    - redis作为session缓存
    - 在需要判断登录的视图用Mixin方法,以此检测是否登录
- ### 用户中心
    - redis作为储存历史游览记录   
    - 可以上传多个地址 设置默认地址待补充
- ### 搜索
    - 采用haystack框架 jieba分词
    - 为了兼容新版本Django模块 安装six模块 复制到了django.utils里面
- ### 购物车
    - 后台通过ajax添加购物车
    - 存在redis中
    - 订单并发问题用悲观锁解决和mysql事务解决
    - 支付宝沙盒账号测试
### 简单启动项目 
- 下载压缩包 解压缩 pycharm打开
- 执行迁移生成mysql表 打开redis服务器端 fdfs_trackerd和fdfs_storaged启动 nginx启动
- 支付宝获取公钥私钥放在order文件夹下的 alipy_public_key_pem和app_private_key.pem
- 到Scripts文件夹下执行 python ../manage.py runserver