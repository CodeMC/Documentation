# Documentation
A repository explaining how to make use of our Jenkins and Nexus instances.

Jenkins CI: [https://ci.codemc.io](https://ci.codemc.io/)<br>
Maven repository: [https://repo.codemc.io](https://repo.codemc.io/)

#### Maven setup
```xml
<repositories>
    <!-- CodeMC -->
    <repository>
        <id>codemc-repo</id>
        <url>https://repo.codemc.io/repository/maven-public/</url>
    </repository>
</repositories>
```

#### Gradle setup
```gradle
repositories {
    maven {
        name = 'codemc-repo'
        url = 'https://repo.codemc.io/repository/maven-public/'
    }
}
```

## About
Welcome to CodeMC, a public Jenkins instance and Maven repository for open source Minecraft projects.
If you want to add your build job to our instance please [contact us](#support), we'd love to support your project(s)!

## Support
If you need help or you have a question, feel free to join our Discord server! [![Discord](https://img.shields.io/discord/405915656039694336.svg?style=flat-square)](https://discord.gg/AGcFMu6)<br>

## FAQ/Wiki
To learn more about the service, you can click [here](https://github.com/CodeMC/Documentation/wiki) to read the wiki.
