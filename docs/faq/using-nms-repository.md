# How to use the NMS Repository?

CodeMC offers a NMS Repository that allows you to download and use specific NMS content from a particular version, without having to do things like running BuildTools yourself.  
To use the Repository, add the below displayed content to your `pom.xml` or `build.gradle(.kts)` file.

/// tab | :simple-apachemaven: pom.xml

//// info |
Press the :material-plus-circle: icon for extra info.
////

```xml { .annotated title="pom.xml" }
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
    <version>{version}</version> <!-- (1) -->
    <scope>provided</scope>
  </dependency>
</dependencies>
```

1.  Replace `{version}` with the same version you would use for the Spigot API.  
    As an example, if you use `1.21-R0.1-SNAPSHOT` for the Spigot API would you also need to use it for the NMS repository.
///

/// tab | :simple-gradle: build.gradle

//// info |
Press the :material-plus-circle: icon for extra info.
////

```groovy { .annotated title="build.gradle" }
repositories {
    maven{ url = "https://repo.codemc.io/repository/nms/" }
}

dependencies {
    compileOnly("org.spigotmc:spigot:{version}") // (1)
}
```

1.  Replace `{version}` with the same version you would use for the Spigot API.  
    As an example, if you use `1.21-R0.1-SNAPSHOT` for the Spigot API would you also need to use it for the NMS repository.
///

/// tab | :simple-gradle: build.gradle.kts

//// info |
Press the :material-plus-circle: icon for extra info.
////

```kotlin { .annotated title="build.gradle.kts" }
repositories {
    maven("https://repo.codemc.io/repository/nms/")
}

dependencies {
    compileOnly("org.spigotmc:spigot:{version}") // (1)
}
```

1.  Replace `{version}` with the same version you would use for the Spigot API.  
    As an example, if you use `1.21-R0.1-SNAPSHOT` for the Spigot API would you also need to use it for the NMS repository.
///
