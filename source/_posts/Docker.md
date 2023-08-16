---
title: Docker
---
### Docker 镜像

​	镜像是Docker容器运行的前提。Docker镜像是一个特殊的文件系统，除了提供了容器运行时所需的程序、库、资源、配置等文件外，还包含了一些为运行时准备的配置参数（如匿名卷、环境变量、用户等）。镜像不会包含动态数据，在构建完成后**不会改变**。

​	镜像在设计时将其设计为分层存储架构，所以镜像只是一个虚拟概念，并非只有一个文件组成，而是由多层文件系统联合组成。

​	镜像构建时会一层一层构建，前一层是后一层的基础。每一层构建完毕就**不会发生改变**，因此，在构建镜像时，每一层尽量只包含该层需要添加的东西，额外的东西应该在该层构建结束前清理掉。举个例子：

> 假如在这一层删除前一层文件的操作，实际上不是真的删除了前一层的文件，而是仅在当前层标记为该文件已删除。在最终容器运行时，虽然不会看到这个文件，但是实际上该文件会一直跟随镜像。

### 容器

​	通过镜像运行的实例称为容器，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、暂停、删除。

​	Docker利用容器来运行应用，每个容器都是互相隔离的、保证安全的平台。

​	容器实质是进程，但和直接在宿主执行的进程不同，容器进程运行在属于自己的独立命名空间，所以容器可以有自己的root文件系统、自己的网络配置、自己的进程空间等。容器内进程运行在一个隔离的环境里，这种特性使容器封装的应用比直接在宿主运行更安全。

​	每一个容器运行时，是以镜像为基础层，在其上创建一个当前容器的存储层，我们可以称这个为容器运行时读写而准备的存储层为**容器存储层**。容器存储层的生存周期和容器一样，容器消亡时，容器存储层也随之消亡。因此，**任何保存于容器存储层的信息都会随容器删除而丢失**。

​	按照 Docker 最佳实践的要求，容器不应该向其存储层内写入任何数据，容器存储层要保持**无状态化**，所有的文件写入操作，都应该使用数据卷、或者绑定宿主目录，在这些位置的读写会跳过容器存储层，直接对宿主（或网络存储）发生读写，其性能和稳定性更高。数据卷的生存周期独立于容器，容器消亡，数据卷不会消亡。因此，使用数据卷后，容器删除或者重新运行之后，数据却不会丢失。

#### 数据卷

​	数据卷是一个可供一个或多个容器使用的特殊目录，用于持久化数据以及共享容器间的数据，它以正常的文件或目录的形式存在于宿主机上。 另外，其生命周期独立于容器的生命周期，即当你删除容器时，数据卷并不会被删除。有以下特性：		

- 数据卷可以在容器之间共享和重用
- 对数据卷的修改会立刻生效
- 对数据卷的更新不会影响镜像
- 数据卷默认会一直存在，即使容器被删除

### 仓库

Docker仓库用于镜像的集中存储、分发的地方。




