
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

## 注意事项

- 确保将URL中的用户名和仓库名替换为您实际使用的GitHub仓库信息
- 如果使用的是SNAPSHOT版本，请确保snapshots配置已正确启用
- 建议在开发环境中设置`updatePolicy`为`always`以确保及时获取最新版本
