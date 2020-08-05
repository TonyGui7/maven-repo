# maven-repo (Github仓库搭建配置)

## 背景

为了将个人项目应用到新的个人项目中，因此需要一个远程仓库来存储库文件，本地仓库不能满足需求是因为个人有几个不同的笔记本分散在不同地点，家和工作地。而上传至mavenCentral或jcenter个人觉得麻烦，在家经常有下不了依赖文件的情况出现，因此需要有一个个人仓库，存放个人文件，也是一个自我积累和沉淀的记录。

## 流程

- 先在github创建个人仓库，这个仓库就是后续上传文件的远程仓库，这个操作很简单，这里就不赘述，我这里创建的仓库名是''maven-repo''，如下

   ![Image text](https://github.com/TonyGui7/maven-repo/blob/master/resources/maven-repo.png)

- 在本地指定目录下创建本地仓库和上述远程仓库关联，其实就是git常用操作，我这里本地仓库的路径如下

  ```
  file:/Users/tonygui/github/maven-repository/repository/
  ```

  然后切换到该目录下执行如下常用git命令

  ```
  git init  
  git add .
  git commit -m '{你想输入的提交信息}'
  git remote add origin https://github.com/TonyGui7/maven-repo.git     //后面的git地址是上面创建的远程仓库git地址
  git push -u origin master
  ```

  至此，本地仓库和远程仓库已关联

- 将您个人的library库进行打包，并上传到本地仓库，譬如这里将如下库打包

  ![Image text](https://github.com/TonyGui7/maven-repo/blob/master/resources/packaging.png)

打包的gradle脚本如下

![Image text](https://github.com/TonyGui7/maven-repo/blob/master/resources/publish-script.jpeg)

其中repository_url就是上面创建的本地仓库路径

```
file:/Users/tonygui/github/maven-repository/repository/
```

对android studio而言，可在右侧的gradle面板中会有uopload任务，双击即可执行，如下

![Image text](https://github.com/TonyGui7/maven-repo/blob/master/resources/publish-operation.jpeg)

之后在本地仓库中就出现打包的文件，然后按照平常git提交代码一样，将文件推送至远程仓库。



至此，文件已经上传仓库了，其它项目可以直接依赖。



## 仓库的依赖

这里已android studiuo为例，要在项目依赖该仓库，只用在你自己的项目的主工程目录下的build.gradle文件的repositories添加如下依赖

```
maven {
  url "https://raw.githubusercontent.com/TonyGui7/maven-repo/master"
}
```

然后在对应module依赖对应的文件，具体的依赖方式看对应项目说明



 **附：**上面是url是raw.githubusercontent.com，一定不要写成github.com，前一个是用来存储用户上传的素材文件的，后一个才是仓库项目文件