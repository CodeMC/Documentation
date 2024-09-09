# How do I build a Maven Project with JDK 8?

Jenkins dropped official support for JDK 8 Maven builds. To still build projects using this Java version can you either use our custom Maven plugin to select a JDK Toolchain based on your `maven-compiler-plugin` settings or cross-compile with a newer JDK Version.

## Toolchain Plugin

Our custom Maven Plugin can select a toolchain (e.g. JDK 8) during the build process. For this the following workaround is required:

1. Set the JDK version to JDK 11.
2. Add the following maven goal to the command line:  
    `io.codemc.maven.plugins.toolchain:codemc-toolchain-selector:0.0.2-SNAPSHOT:select`

## Cross-Compiling

Cross-compiling is the process of targeting a different platform than the compiler itself.  
In this case, it allows to use any JDK beyond Java 8 to generate a build that is still compatible with the older version.

You can achieve this by using `source` and `target` in the `maven-compiler-plugin` configuration. However, the usage of `release` is recommended in order to verify that you don't use any Java API methods introduced in later Java versions:  

```xml
<plugins>
  <plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.10.1</version> <!-- Make sure to update when necessary -->
    <configuration>
      <release>8</release>
    </configuration>
  </plugin>
</plugins>
```
