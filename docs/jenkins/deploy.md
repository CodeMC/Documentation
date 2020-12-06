# Deploying to the CodeMC Nexus
CodeMC offers you a way to upload your API or project to a nexus, so that other developers can integrate it into their own projects to use.  
This page here will explain how you can achieve this.

!!! info "Important"
    You can only deploy your project to the nexus from within your Jenkins Project.  
    If you try to deploy from outside of it will you receive an "Unauthorized" exception.

## Maven
To get started, make sure to have the following information added to your `pom.xml` file:  
```xml
<distributionManagement>
  <repository>
    <id>codemc-releases</id>
    <url>https://repo.codemc.io/repository/maven-releases/</url>
  </repository>
  <snapshotRepository>
    <id>codemc-snapshots</id>
    <url>https://repo.codemc.io/repository/maven-snapshots/</url>
  </snapshotRepository>
</distributionManagement>
```
