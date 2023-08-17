## **kubecm 的一些实践**

## **问题背景**

在维护和管理多个k8s集群时，每个集群都有自己对应的config文件，那么带来的问题就是在 ~/.kube 目录下就会有一大堆各种环境的 yaml，对于管理来说不是特别的友好。
更有可能在不同的集群切来切去，造成运维事故。因此这里介绍一种管理 kubeconfig 的一种方式.(这个主要以 mac 来作为演示).
<div className="video-container">
  <iframe src="//player.bilibili.com/player.html?aid=531017349&bvid=BV1nu411L7nh&cid=1198974833&page=1" width="100%" height="360" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
</div>


## **解决痛点**
  - 统一管理多个k8s集群
  - 来回切换指定namespace繁琐
  - 很多时候不知道自己在哪个集群下

## **如何安装**

Mac安装地址：[只需要使用 brew 直接安装kubecm即可](https://formulae.brew.sh/formula/kubecm)




## **kubecm 案例:**

参数说明：

  - 我最常用的就是添加，删除，切换集群

```shell
                                                 
        Manage your kubeconfig more easily.        
                                                   

██   ██ ██    ██ ██████  ███████  ██████ ███    ███ 
██  ██  ██    ██ ██   ██ ██      ██      ████  ████ 
█████   ██    ██ ██████  █████   ██      ██ ████ ██ 
██  ██  ██    ██ ██   ██ ██      ██      ██  ██  ██ 
██   ██  ██████  ██████  ███████  ██████ ██      ██

 Tips  Find more information at: https://kubecm.cloud

Usage:
  kubecm [command]

Available Commands:
  add         Add KubeConfig to $HOME/.kube/config   # 添加
  alias       Generate alias for all contexts
  clear       Clear lapsed context, cluster and user
  cloud       manage kubeconfig from cloud
  completion  Generate completion script
  create      Create new KubeConfig(experiment)
  delete      Delete the specified context from the kubeconfig  # 删除
  help        Help about any command
  list        List KubeConfig
  merge       Merge multiple kubeconfig files into one
  namespace   Switch or change namespace interactively
  rename      Rename the contexts of kubeconfig
  switch      Switch Kube Context interactively  # 切换
  version     Print version info

Flags:
      --config string   path of kubeconfig (default "$HOME/.kube/config")
  -h, --help            help for kubecm
      --ui-size int     number of list items to show in menu at once (default 4)

Use "kubecm [command] --help" for more information about a command.
```


首先我们先回到：家目录下的`.kube`目录

```shell
$ pwd
/Users/beiyiwangdejiyi/.kube
```
#### **添加一个集群**

```shell
kubecm add -f enflame.yaml
```

#### **删除一个集群**

```shell
$ kubecm delete   # 选择删除的集群，选择True
Use the arrow keys to navigate: ↓ ↑ → ←  and / toggles search
Select The Delete Kube Context
  😼 ucloud-k3s(*)
    enflame
    produce
↓   pve
```
#### **切换一个集群**
```shell
$ kubecm switch   # 可以上下切换，选择集群环境
Use the arrow keys to navigate: ↓ ↑ → ←  and / toggles search
Select Kube Context
    ucloud-k3s(*)
    bj
  😼 dev
↓   produce
```

以上就是kubecm 的一些安装和使用方法，其他的如果感兴趣可以自己试一试。



!!! info "kubens kubectx"
文章地址：[kubenc](https://github.com/ahmetb/kubectx)


## **kubectx安装**
如果你使用Homebrew，你可以像这样安装：
```shell
brew install kubectx
```
安装完成之后，来这样使用kubens就可以很方便的切换namespace。


## **fzf安装**

!!! info "fzf 安装"
    - [fzf官网](https://github.com/junegunn/fzf#fuzzy-completion-for-bash-and-zsh)
这里面比较好玩的还有一个带有模糊搜索的交互式菜单，安装完成之后再使用kubens就香的很啊

```shell
brew install fzf
$(brew --prefix)/opt/fzf/install
```
!!! warning "温馨提示"
    - 如果不能使用，需要关闭终端，重新打开

fzf除了这些，还有很多的骚操作，shell命令补全，另外fzf 重写了 ctrl+r 搜索历史命令



### ** 文章参考:**

- https://formulae.brew.sh/formula/kubecm
- https://github.com/sunny0826/kubecm