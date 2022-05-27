## Welcome to "Hello World" with GitHub Actions

This course will walk you through writing your first action and using it with a workflow file. 

**Ready to get started? Navigate to the first issue.**

# action 分为  container action  和JavaScript Actions。
- 一般都是使用 container action。  所以需要 了解dockerfile. docker 将会在GitHub host 的 Linux 环境里面创建
- JavaScript action 能够更快的执行，但是需要自己管理代码。


## 开始创建一个action 创建 分支 和文件
- branch - action-b
- DockerFile

## 创建dockerfile， 里面的内容是，继debian 镜像 然后将 action-b 里面的entrypoint.sh 添加到镜像内，然后修改执行权限。
- [ENTRYPOINT 的讲解](https://yeasy.gitbook.io/docker_practice/image/dockerfile/entrypoint) 是一个入口执行命令。可以接受运行镜像时候的CMD 参数
- 这样 整个镜像其实就是一个有entrypoint.sh的容器。
- 容器build run 时执行 entrypoint.sh
- 这里的意思就是在运行镜像的时候执行 sh entrypoint.sh
- entrypoint 的内容 ， sh -c 代表， 使用 shell 执行 cmd

## 当运行这个Docker 的时候， 需要一些环境变量。以及定义 一个Action的所需的metadata（元数据）。 所有的这些都会被放到 action.yml 文件里面
- 创建action.yml。 
- inputs 里面放的是 注入到 容器内的变量
- runs 是代表这个action 执行的类型
- branding 是一个action 执行的颜色配置
- name/ description / author 代表 action的基本数据