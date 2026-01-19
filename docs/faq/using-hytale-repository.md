# How to use the Hytale Repository?

CodeMC offers a Hytale Repository that allows you to download and use specific Hytale server version, without having to do things like running hytale-downloader yourself.  
To use the Repository, add the below displayed content to your `pom.xml` or `build.gradle(.kts)` file.

/// tab | :simple-apachemaven: pom.xml

//// info |
Press the :material-plus-circle: icon for extra info.
////

```xml { .annotated title="pom.xml" }
<repositories>
  <repository>
    <id>codemc-hytale-repository</id>
    <url>https://repo.codemc.io/repository/hytale/</url>
  </repository>
</repositories>

<dependencies>
  <dependency>
    <groupId>com.hypixel.hytale</groupId>
    <artifactId>Server</artifactId>
    <version>{version}</version> <!-- (1) -->
    <scope>provided</scope>
  </dependency>
</dependencies>
```

1.  Replace `{version}` with the desired Hytale server version.  
    Examples: `2026.01.17-4b0f30090`, `LATEST` if you want the latest release.
///

/// tab | :simple-gradle: build.gradle

//// info |
Press the :material-plus-circle: icon for extra info.
////

```groovy { .annotated title="build.gradle" }
repositories {
    maven{ url = "https://repo.codemc.io/repository/hytale/" }
}

dependencies {
    compileOnly("com.hypixel.hytale:Server:{version}") // (1)
}
```

1.  Replace `{version}` with the desired Hytale server version.  
    Examples: `2026.01.17-4b0f30090`, `+` if you want the latest release.
///

/// tab | :simple-kotlin: build.gradle.kts

//// info |
Press the :material-plus-circle: icon for extra info.
////

```kotlin { .annotated title="build.gradle.kts" }
repositories {
    maven("https://repo.codemc.io/repository/hytale/")
}

dependencies {
    compileOnly("com.hypixel.hytale:Server:{version}") // (1)
}
```

1.  Replace `{version}` with the desired Hytale server version.  
    Examples: `2026.01.17-4b0f30090`, `+` if you want the latest release.
///
