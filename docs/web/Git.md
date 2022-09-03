# Git基本操作

1.git创建本地仓库的两步（先添加（临时存储），后提交（本地历史仓库））

![image-20220304145948372](H:%5CF%5Csecond-period%5Cdocs%5Cweb%5Cimg%5Cimage-20220304145948372.png)

2.git命令

![image-20220304150336066](H:%5CF%5Csecond-period%5Cdocs%5Cweb%5Cimg%5Cimage-20220304150336066.png)

3.![image-20220304150431930](H:%5CF%5Csecond-period%5Cdocs%5Cweb%5Cimg%5Cimage-20220304150431930.png)

先创建



# Git与Idea

### 一、idea集成git

1.新建项目，在file选项下找到setting设置，再找到Version Control下的Git配置其软件路径进行测试，成功后代表git就已经集成成功。

![image-20220304142208217](H:%5CF%5Csecond-period%5Cdocs%5Cweb%5Cimg%5Cimage-20220304142208217.png)

2.找到VCS，import into Version Control——>create Git Repository,创建本地仓库（项目目录）

![image-20220304142303710](H:%5CF%5Csecond-period%5Cdocs%5Cweb%5Cimg%5Cimage-20220304142303710.png)

3.提交项目√，Commit Message填写该版本代码信息。

![image-20220304142637269](H:%5CF%5Csecond-period%5Cdocs%5Cweb%5Cimg%5Cimage-20220304142637269.png)

注：Version Control下的log可以查看提交状态记录，√左边的表示pull操作

![image-20220304142850846](H:%5CF%5Csecond-period%5Cdocs%5Cweb%5Cimg%5Cimage-20220304142850846.png)

### 二、idea中的git版本切换

在log下右击想要切换的版本，点击reset两次（最后一次会丢失）

revert——>merge冲突管理点掉两个叉

### 三、分支管理

1.VCS——>Git——>Branches,然后新建之后选择一个分支进行编程，分支下的check out

![image-20220304144534185](H:%5CF%5Csecond-period%5Cdocs%5Cweb%5Cimg%5Cimage-20220304144534185.png)

2.VCS——>Git——>Merge，进行合并分支

### 四、推送管理和克隆代码到本地

1.推送代码到远程仓库：VCS——>Git——>push,其中URL在gittee远程仓库里面

2.克隆代码到本地：在创建项目选项页选择最下面的check out from Version Control

![image-20220304145506861](H:%5CF%5Csecond-period%5Cdocs%5Cweb%5Cimg%5Cimage-20220304145506861.png)

