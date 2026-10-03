
# Maven GitHub 仓库配置指南

本文档介绍如何在您的Maven项目中配置和使用GitHub仓库中的依赖。

## 配置步骤

### 1. 添加仓库配置

在项目的`pom.xml`文件中添加以下仓库配置：

```xml
<repositories>
    <repository>
        <id>mvn-repo</id>
        <url>https://raw.github.com/super-npc/mvn-repo/master</url>
        <snapshots>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
        </snapshots>
    </repository>
</repositories>
```
```shell
# 本地打包后没有生成sha1导致校验失败
mvn install:install-file \
  -Dfile=binlog4j-core-1.9.1.jar \
  -DgroupId=cc.bronya \
  -DartifactId=binlog4j-core \
  -Dversion=1.9.1 \
  -Dpackaging=jar \
  -DlocalRepositoryPath=/home/chenwenxi/npc/git/mvn-repo
```

```shell

mvn deploy:deploy-file -DgroupId=cc.bronya -DartifactId=binlog4j-core -Dversion=1.9.1 -Dpackaging=jar -Dfile=binlog4j-core-1.9.1.jar -Durl=https://raw.github.com/super-npc/mvn-repo/master

mvn deploy:deploy-file -Dfile=binlog4j-core-1.9.1.jar \
                       -DgroupId=cc.bronya \
                       -DartifactId=binlog4j-core \
                       -Dversion=1.9.2 \
                       -Dpackaging=jar \
                       -DrepositoryId=github \
                       -Durl=https://maven.pkg.github.com/super-npc/mvn-repo \
                       -s /home/chenwenxi/npc/git/bronya/settings.xml
# 从项目打包后再上传可以解决签名问题
mvn -f pom.xml install -pl binlog4j-core -am org.apache.maven.plugins:maven-deploy-plugin:2.8:deploy -DskipTests -DaltDeploymentRepository=internal.repo::default::file:/home/chenwenxi/npc/git/mvn-repo -s /home/chenwenxi/npc/git/bronya/settings-github.xml
```

```
https://raw.githubusercontent.com/super-npc/mvn-repo/refs/heads/main/hosts/company
```

## 注意事项

- 确保将URL中的用户名和仓库名替换为您实际使用的GitHub仓库信息
- 如果使用的是SNAPSHOT版本，请确保snapshots配置已正确启用
- 建议在开发环境中设置`updatePolicy`为`always`以确保及时获取最新版本

使用github一个项目作为maven私有仓库
将一个jar包使用命令的方式推送到这个github私有仓库,并从另外一个项目可以进行依赖
