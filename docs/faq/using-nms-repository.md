# How to use the NMS Repository?

CodeMC offers a NMS Repository that allows you to download and use specific NMS content from a particular version, without having to do things like running BuildTools yourself.  
To use the Repository, add the below displayed content to your `pom.xml` or `build.gradle(.kts)` file.

/// info
Replace `{version}` with a matching version.  
CodeMC follows the same version naming as Spigot and Paper do, so if you use `1.21-R0.1-SNAPSHOT` for Spigot can you use the same version for the NMS repository.
///

/// tab | :simple-apachemaven: pom.xml
```xml
<repositories>
  <repository>
    <id>codemc-nms-repository</id>
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
///

/// tab | :simple-gradle: build.gradle
```groovy
repositories {
    maven{ url = "https://repo.codemc.io/repository/nms/" }
}

dependencies {
    compileOnly("org.spigotmc:spigot:{version}")
}
```
///

/// tab | :simple-gradle-kotlin: build.gradle.kts
```kotlin
repositories {
    maven("https://repo.codemc.io/repository/nms/")
}

dependencies {
    compileOnly("org.spigotmc:spigot:{version}")
}
```
///
