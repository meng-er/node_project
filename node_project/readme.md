
# 编写数据库初始化脚本（sql/init.sql）
要求可以直接从命令行运行，实现在数据库初始化的功能，主要包括
- 设计用户数据表，计划需要的字段，选择合适的类型
- 创建数据表结构，如果数据存在就删除原有数据，并新建
- 插入必要的初始数据，例如管理员账户等
执行脚本并检查数据库初始化是否成功

# 实现用户服务功能
同时实现用户服务api（api/user.js，8080端口）和测试脚本（test/user.js），用户服务实现全部的用户管理功能，测试脚本测试全部的功能
- 用户的注册、登录、退出、密码重置、用户信息修改等
# 实现app服务
app服务包含各种服务类型，这个demo服务都放在app目录中，每个服务可以单独启动，并且都必须指定启动的端口号。
- 图片大小转换（无状态服务），对上传的图片文件，转换为指定的尺寸（app/imgResize.js)
- 实现用户的todo List功能，实现todo List的增、删、修和列表功能(app/todoList.js），todoList的内容放在数据库中，数据库初始化脚本中增加todoList的初始化内容，并重新初始化数据库
- 实现和前面相同的todoList功能（app/todoList-local.js），但是todoList的内容放在todoList.js的工作目录中的data目录中，且每个用户的内容放在独立的文本文件中，文本文件的存放格式自己定义，并形成文档
# 实现app的测试脚本
对每个app,开发测试脚本，检测服务是否正常，测试脚本同样可以指定端口号，测试脚本在test/app目录中，文件名与app服务的文件名相同
# 实现app服务的发布功能
- 定义app服务的发布文件规范（deploy.readme.md），通过发布文件定义每个app的实例的服务端口，1个app可以启动多个实例
- 编制发布文件（deploy.json），对已经开发的3种app各配置2个实例
- 编制发布程序，读取发布文件的内容，并按照配置启动服务，输出每个服务实例的启动信息的日志文件（deploy.log）
- 编制服务状态检测程序，按照发布文件，调用测试脚本检查服务实例的状态及性能（测试耗时）
# 实现服务映射关系的管理api
- 定义每个转发服务需要的属性，例如：url、状态（有/无）、模式（转发/分配url）、映射后的url（一对多）及状态（例如已服务数)
- 定义服务转发的配置文件规范（api/map.readme.md），通过map.json的配置文件，将每个类型的服务映射到不同的path上
- 通过配置文件定义服务转发的属性，同类服务用相同的url,可以实际对应多个服务实例
- 开发服务映射程序（api/map.js，端口可以指定），启动后可以用不同map启动的url的不同path调用不同的类型的服务，并要求对todoList-local的服务请求，同个用户（相同用户的定义可以是相同用户名、相同ip等），每次都映射到固定的服务实例上（如果需要数据库，请重构数据库初始化脚本）
- 在服务映射程序上开发服务列表功能，可以返回所有的服务类型和访问路径

# 通过vue开发web和app