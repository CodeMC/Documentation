# Documentation
A repository explaining how to make use of our Jenkins and Nexus instances.

Jenkins CI: [https://ci.codemc.org](https://ci.codemc.org/)<br>
Maven repository: [https://repo.codemc.org](https://repo.codemc.org/)

Maven
```xml
    <repositories>
        <!-- CodeMc -->
        <repository>
            <id>codemc-repo</id>
            <url>https://repo.codemc.org/repository/maven-public/</url>
        </repository>
    </repositories>
```

Gradle
```gradle
    repositories {
        maven {
            name = 'codemc-repo'
            url = 'https://repo.codemc.org/repository/maven-public/'
        }
    }
```

## About
Welcome to CodeMC, a public Jenkins/Maven repository for open source Minecraft projects.
If you want to add your build job to our instance please contact us, we'd love to support your project(s)!

## Support
If you need help or you have a question, please join our Discord server: ![Discord](https://img.shields.io/discord/405915656039694336.svg?style=flat-square)<br>
If you don't have Discord you can contact us via [email](mailto:codemc.org@gmail.com).

## FAQ and Wiki
To get more information about the service, you can click [here](https://github.com/CodeMC/Documentation/wiki)
