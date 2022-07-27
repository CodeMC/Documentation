[Discord]: https://discord.gg/AGcFMu6
[Connection Settings]: https://github.com/settings/applications
[CodeMC application]: https://github.com/settings/connections/applications/2debe3b061b244423bf5


# FAQ

Commonly asked questions about CodeMC and related projects.

## What is the NMS Maven Repository?

!!! note
    Below, replace `{version}` with the version number you wish to use.  
    The version syntax is similar to the Spigot API (e.g. `1.15.2-R0.1-SNAPSHOT`)

Add the following parts to your `pom.xml` when using Maven:  
```xml
<repositories>
    <repository>
        <id>nms-repo</id>
        <url>https://repo.codemc.io/repository/nms/</url>
    </repository>
</repositories>

<dependencies>
    <dependency>
        <groupId>org.spigotmc</groupId>
        <artifactId>spigot</artifactId>
        <version>{version}</version>
        <scope>provided</scope>
    </dependency>
</dependencies>
```

Add this to your `build.gradle` file when using Gradle:
```groovy
repositories{
    maven{ url = "https://repo.codemc.io/repository/nms/" }
}

dependencies{
    compileOnly(group: 'org.spigotmc', name: 'spigot', version: '{version}')
}
```

----
## How can my project(s) be added to CodeMC?

To get your project(s) added, join the [CodeMC Discord][Discord] and read the pinned message in the `#request-access` channel.  
Please stay patient when requesting to be added as we might have other things to do.

----
## My project isn't about Minecraft. Can I still be added?

Yes, you can.

CodeMC accepts nearly every open-source project, as long as it is Java-based (and follows the points in the above FAQ entry).

----
## I can't access any job configuration or folders in my Organisation. What is happening?
You need to make sure to have granted access to your organisation when you logged in the first time.  
To check this, head over to your [Connection Settings] on GitHub and make sure to have granted the [CodeMC application] access to your account and organisations.

----
## How can I deploy my maven artifacts to the CodeMC repository?

You can read about the requirements and general process in the [Deploy to the CodeMC Nexus](../jenkins/deploy/) page.

----
## How to build a JDK 8 Maven project?

Jenkins dropped the official support for JDK 8 Maven builds, the following workaround is required:
- Set the JDK version to JDK 11
- Add the following maven goal to the commandline:
`io.codemc.maven.plugins.toolchain:codemc-toolchain-selector:0.0.2-SNAPSHOT:select`
