# Documentation
A repository explaining how to make use of our Jenkins and Nexus instances.

Jenkins CI: [https://ci.codemc.org](https://ci.codemc.org/)<br>
Maven repository: [https://repo.codemc.org](https://repo.codemc.org/)

#### Maven setup
```xml
<repositories>
    <!-- CodeMC -->
    <repository>
        <id>codemc-repo</id>
        <url>https://repo.codemc.org/repository/maven-public/</url>
    </repository>
</repositories>
```

#### Gradle setup
```gradle
repositories {
    maven {
        name = 'codemc-repo'
        url = 'https://repo.codemc.org/repository/maven-public/'
    }
}
```

## About
Welcome to CodeMC, a public Jenkins instance and Maven repository for open source Minecraft projects.
If you want to add your build job to our instance please [contact us](#support), we'd love to support your project(s)!

## Support
If you need help or you have a question, feel free to join our Discord server! [![Discord](https://img.shields.io/discord/405915656039694336.svg?style=flat-square)](https://discord.gg/AGcFMu6)<br>
If you don't have Discord, you can also contact us via [email](mailto:codemc.org@gmail.com).

## FAQ/Wiki
To learn more about the service, you can click [here](https://github.com/CodeMC/Documentation/wiki) to read the wiki.

## Sponsor
Our infrastructure is sponsored by [FastVM](http://www.fastvm.io). Do you need a cheap yet powerful VPS? Then check them out!
