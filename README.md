# hello-world
learn how to use github
this is the new branch's change

## Git 与 SVN

svn存储的是diff，git存储的事每个snapshot
Git是分布式的，无网络可以工作，但是svn是集中式的，必须联网

## Git Flow

![image-20220512201912046](http://xingyajie.oss-cn-hangzhou.aliyuncs.com/uPic/image-20220512201912046.png)

## Git名词

**HEAD** 指当前分支的最后一次提交对象

**mode**在Git里，几个常 用的mode值包括:

- 100644 - 普通文件;
- 100755 - 可执行文件;
- 120000 - 符号链接(symbolic link); 040000 - 目录;

**Git index**  文件就是暂存区
Git在.git 文件夹下面存放了index文件，该文件表示Git stage的内容。该文件是二进制文件，保存了被stage的文件的所有信息，想innode信息，hash信息等等

**git add** 实际上做的事
把文件内容计算出hash值作为key，把文件内容压缩后作为value，存放到objects目录里面，然后把对应文件信息放到index文件中

## Git常用操作

**git reset**

用于回退版本，可以指定退回某一次提交的版本。

–-soft:回退到暂存区。

-–hard:回退到工作目录。 

```
git reset HEAD .
```

**git commit**

```
git commit -m ‘更新内容’
```

**git checkout** 
切换分支
重新存储工作区文件

```
git checkout master
```

# Git 使用

cd /Users/xyj/Desktop/dnf
git init
git config user.email
git config user.name 
git config user.name xyj
git add . //点指的是当前目录
git commit -m 'add 前三行'
git log --oneline --decorate --graph --stat  // 查看提交信息
//修改文件 
git add . //点指的是当前目录
git commit -m 'add 第四行'
git log --oneline --decorate --graph --stat
git reset --hard HEAD~1  // 回退到工作目录，修改的代码会丢失
git log --oneline --decorate --graph --stat
//再次修改文件
git add . 
git commit -m '第五行'
git log --oneline --decorate --graph --stat
git reset --soft HEAD~1 //回退到暂存区，修改的内容还在本地
git status //查看状态
git reset HEAD .  // 从暂存区移出，git add的逆向操作
git checkout -- . // 重新存储工作区文件，此时恢复到第一次提交的文件状态

git cat-file -p 0e3760631ad12cf235be3f2a13fbd98cae3c1fab 根据key找对应文件

git ls-files -s //查看暂存区具体信息

git hash-object -w test.text
    git hash-object 计算一个文件的git对象ID，即SHA1的哈希值
    将制定对象写入数据库

git update-index --add --cacheinfo 100644 582f5e8a8956d7bf05eebf0370211c4814d6f6da test.text
    git update-index 讲工作目录的文件加入索引/暂存区域
    --add 添加指定文件
    --cacheinfo 按照格式将指定的信息

git write-tree 生成当前的树

git read-tree --prefix=dnf/ 4e9ccdacc6720dd0851c93f0c52a4f8ff2170775
手动生成一个树dnf/，并将之前生成的树放在dnf里面

git write-tree 4d4fcd1cac25427d51a54ac6d730bcd3d9dac41a

git checkout -- dnf/ 将生成的树从暂存区恢复到文件内

## git key-value文件系统
根据修改的文件进行hash，将hash值作为key，将文件作为value，存放到.git

Git将存储对象的40位HASH分为两部分
    1、前两位作为文件夹
    2、后面38位作为对象文件名，路径文 .git/objects/hash[:2]/hash[2:40]

为什么这么设计
    1、部分文件系统对目录下的文件数量有限制，
    2、部分文件系统查找文件属于线性查找，目录下文件越多，访问速度越慢
