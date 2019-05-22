### 1、什么是git

git 分布式版本管理系统，
集中式： svn，cvs

### 2、为什么使用git

### 3、git基本操作

* git init 初始化，创建工作空间
* git add 添加到暂存区
* git commit -m '****' 添加到本地仓库
* git push origin master 提交到远程代码仓库

### 4、git可视化提交工具，sourcetree

* 安装2.*版本sourcetree
* 安装完成进入 %LocalAppData%\Atlassian\SourceTree\ 目录
* 创建accounts.json,插入内容
``` 
[
  {
    "$id": "1",
    "$type": "SourceTree.Api.Host.Identity.Model.IdentityAccount, SourceTree.Api.Host.Identity",
    "Authenticate": true,
    "HostInstance": {
      "$id": "2",
      "$type": "SourceTree.Host.Atlassianaccount.AtlassianAccountInstance, SourceTree.Host.AtlassianAccount",
      "Host": {
        "$id": "3",
        "$type": "SourceTree.Host.Atlassianaccount.AtlassianAccountHost, SourceTree.Host.AtlassianAccount",
        "Id": "atlassian account"
      },
      "BaseUrl": "https://id.atlassian.com/"
    },
    "Credentials": {
      "$id": "4",
      "$type": "SourceTree.Model.BasicAuthCredentials, SourceTree.Api.Account",
      "Username": "",
      "Email": null
    },
    "IsDefault": false
  }
]
```



### 公司一般使用gitlab做git代码管理仓库