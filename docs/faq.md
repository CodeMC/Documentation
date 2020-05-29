[Discord]: 
[Connection Settings]: https://github.com/settings/applications
[CodeMC application]: https://github.com/settings/connections/applications/2debe3b061b244423bf5


# FAQ
Commonly asked questions about CodeMC and related projects.

## How can my projec(s) be added to CodeMC?
To get your project(s) added, join the [CodeMC Discord][Discord] and contact an Administrator.  
When doing so, make sure to follow those basic guides:

- Provide your GitHub username. GitHub is the main system to login on the site.
- You need to have at least one open source project (Private repositories don't count).

Please stay patient when requesting to be added as we might have other things to do.

----
## My project isn't about Minecraft. Can I still be added?
Yes, you can.  
CodeMC accept nearly every open source project, as long as it is Java-based (And follows the points in the above FAQ entry).

----
## I can't access any job configuration or folders in my Organisation. What is happening?
You need to make sure to have granted access to your organisation when you logged in the first time.  
To check this, head over to your [Connection Settings] on GitHub and make sure to have granted the [CodeMC application] access to your account and organisations.

----
## How can I deploy my maven artefacts to the CodeMC repository?
When you use Maven can you add the following settings to your `pom.xml`  
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

Alternatively can you also execute an upload to the repository through the command line.  
Just execute the following maven command for that:
```
clean install org.apache.maven.plugins:maven-deploy-plugin:2.8.2:deploy -DaltSnapshotDeploymentRepository=codemc-snapshots::default::https://repo.codemc.io/repository/maven-snapshots/ -DaltReleaseDeploymentRepository=codemc-releases::default::https://repo.codemc.io/repository/maven-releases/
```

!!! warning "Important"
    Make sure to have the right cridentials for the deploy to be successful!  
    Ask a staff member on the [Discord] for support, when you're lost.