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


## 编辑workflow。 定义 workflow 也就是配置 在什么event下。执行这个docker 容器
- 文件定义在 `.github/workflows/main.yml`
- yml 文件内 string 不需要 “”
- workflows 下面定义的都是 action执行的步骤和配置
- 允许定义多个文件。以此来区分不同环境的action  [Can I have multiple actions in the workflows](https://stackoverflow.com/questions/57115520/can-i-have-multiple-github-actions-workflow-files)
- 文件内容 ： name: 这个action 执行的 name
- on： 在什么事件下触发 可以指定分支+ 事件类型
- jobs: 执行的任务 
    - 需要有一个单独的 name (unique)
    - runs-on  使用什么执行
    - steps 这一个 job 执行的任务
    - 第一个的 user : actions/checkout@v1 是使用一个公共的 actions 使用了这个，  Github Action 才能访问仓库 代码
    - 在github action 能访问仓库代码后。 通过 -uses  提供一个 仓库内的文件路径 让action访问。
    - 这样 github hosting 就知道通过 /action-b 下面的action.yml 来执行单一 action
    - with 代表的是最外层注入的环境变量


## 整体总结
  - DockerFile 定义一个image  用来执行希望执行的任务。 这里执行的是 entrypoint.sh。 而且这个 DockerFile 是对仓库有完整访问权限的。
    - 运行的主体就是这个 DockerFile 所创建出来的 image
  - action.yml 这个定义了一个 步骤的具体执行方法。 里面 有name/desc/author/ 输入变量 / 以及怎么跑起来 runs ： docker DockerFile 以及该步的颜色。 可以看成一个单一的步骤
- workflows/action.b.yml 这个是 定义了 最上层的 GitHub Action 一系列步骤的集合体。。 意思是 在一个 ubuntu 环境下监听 特定的 on 事件触发不同的执行步骤
  - 可以有多个jobs, 每个job 又执行不同的步骤。 
  - steps 里面定义的就是步骤
  - uses actions/checkout@v1 代表的意思是。让这个集合体/让当前这个Action 可以访问到仓库代码
  - uses ./actions-b 提供出一个步骤的路径。 通过这个路径找到 action.yml 然后进行子步骤的执行 里面的参数可以传递到docker中`




  ## 错误
    - `Dockerfile` 必须 `D`大写 `f` 小写。 这会导致，镜像名称大写。无法构建
    - `chmod +x /entrypoint.sh` 是给予权限