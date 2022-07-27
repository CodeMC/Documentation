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

Jenkins dropped the official support for JDK 8 Maven builds. You can either use our Maven plugin to select a JDK toolchain based on your `maven-compiler-plugin` settings or cross-compile with newer JDK version.

### Toolchain plugin

Our custom Maven plugin can select a toolchain (e.g. JDK 8) during the build process. For this the following workaround is needed:

1. Set the JDK version to JDK 11
2. Add the following maven goal to the commandline:
`io.codemc.maven.plugins.toolchain:codemc-toolchain-selector:0.0.2-SNAPSHOT:select`

### Cross-compiling

Cross-compiling is the process of targeting a different platform than the compiler itself. In this case, it allows to use any JDK beyond Java 8 to generate a build that is still compatible with the older version.

You can achieve this by using `source` and `target` in the `maven-compiler-plugin`. However, the usage of `release` is recommended in order to verify that you don't use any Java API methods introduced in later Java versions.
```xml
  <plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.10.1</version>
    <configuration>
      <release>8</release>
    </configuration>
  </plugin>
```
For more details visit: https://maven.apache.org/plugins/maven-compiler-plugin/examples/set-compiler-release.html

Please note that in comparison to the `toolchain-selector`, this approach will run code during the build process using the selected JDK version. This means that unit and integration tests will run using the newer JDK version instead of Java 8. 
