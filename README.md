# Linux高级编程

## 一、Github

### 1.1	查询

- 关键字查询

  - `awesome`，在此标签类别中查询项目。
  - `python tutorial`，查询资料、书籍等。
  - `socket sample`，查询对应技术的代码样本。

  

### 1.2	Github三要素

1. **仓库（repository）:**仓库是github项目管理存储基本单位，一个仓库中存储一个项目，一个用户可以拥有多个仓库，仓库分为public仓库和private仓库。
2. **提交（commit）:**程序员在整个开发周期，对代码的所有修改都可以通过commit的方式进行记录，便于程序员回溯代码。
3. **分支（branch）:**在仓库中可以包含多个分支，分支才是代码文件的第一存储单位，默认的仓库主分支为master/main。

<img src="C:\Users\gengh\Desktop\科林\笔记\Linux笔记图片\image-20240607102406883.png" alt="image-20240607102406883" style="zoom: 50%;" />

### 1.3	仓库内容

1. **code:**进行资源存储，包括代码资源、二进制文件、项目管理脚本、许可证的等。
2. **issues:**使用时遇到的bug等反馈信息。
3. **README:**使用markdown编写，内容主要是工程自述，开发进度，版本更新，使用介绍等。

**LICENSE许可证：**

​		GPL2.0，GPL3.0，Apahce2.0，Mit，这些许可证给使用者最大使用权限和最少的限制。

### 1.4	Git提交项目

- 设备认证

​		让网站账户与设备绑定，后续完成对代码的管理。

```shell
git init //创建本地仓库
git config --list //查看git的配置文件
git config --global user.email "邮箱"
git config --global user.name "用户名"
ssh-keygen -t rsa -C "注册邮箱" //创建本地密文

/*
* 去对应目录查找密文文件；
* 打开rsa.pub文件，复制密文，粘贴至github(setting->SSH key and GPG->new ssh key->粘贴)；
*/
ssh -T git@github.com //测试关联是否成功
```

********

- 为目标仓库起别名，定位目标仓库，用于后续上传。

```shell
git remote add orgin "ssh地址" //为ssh仓库地址创建别名为origin
git remote remove orgin //删除origin别名
```

***************

- 文件上传

```shell
git add code.c
git commit -m "提交说明"
git push orgin master
```

************

- 本地设备与云端仓库的交互逻辑

<img src="C:\Users\gengh\Desktop\科林\笔记\Linux笔记图片\image-20240607104940059.png" alt="image-20240607104940059" style="zoom:50%;" />

```shell
git add 文件 //添加内容
git rm 文件 //删除本地文件并删除仓库
git restore //恢复被删除（仓库存在）
```

***********

- 依赖关系被破坏

​		通常本地内容要比云端内容新，本地内容提交后实现本地与云端同步。但是如果直接在云端修改内容，就会导致本地内容无法再次提交。

​		解决方法：

​		先拉取云端内容，与本地内容合并或进行其他操作，之后再次提交。

```shell
git pull --rebase orgin master
git rebase --skip //忽略本地内容，保留云端内容
git rebase --abort //撤销rebase
git rebase --continue
```

### 1.5	下载开源代码

```shell
git clone "https仓库地址" //下载开源项目的code资源
```

