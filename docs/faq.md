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
To get your project(s) added, join the [CodeMC Discord][Discord] and contact an Administrator.  
When doing so, make sure to follow those basic guides:

- Provide your GitHub username. GitHub is the main system to login on the site.
- You need to have at least one open-source project (private repositories don't count).

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
When using Maven, you can add the following settings to your `pom.xml`  
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

Alternatively, can you also execute an upload to the repository through the command line.  
Just execute the following maven command for that:
```
clean install org.apache.maven.plugins:maven-deploy-plugin:2.8.2:deploy -DaltSnapshotDeploymentRepository=codemc-snapshots::default::https://repo.codemc.io/repository/maven-snapshots/ -DaltReleaseDeploymentRepository=codemc-releases::default::https://repo.codemc.io/repository/maven-releases/
```

!!! warning "Important"
    Make sure to have the right credentials for the deploy to be successful!  
    If you're lost, ask a staff member on the [Discord] for support.
