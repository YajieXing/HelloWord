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
