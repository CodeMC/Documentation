# Deploy to the Nexus
When joining the CodeMC Project, you will be given a login for our Nexus service. The Nexus Service from CodeMC allows you to distribute your project for others to integrate into their own projects as a library, using their build management tools.

We will explain how you can setup automatic deployments to the Nexus within this page.

/// warning | Important!
Remember to follow our [Usage Guidelines](../../usage-guidelines.md) on how to use our services to not be punished.
///

## Prerequisites
Before you can deploy your project to the Nexus, you will first need to do some preparations to ensure that everything will work as expected.

### Login
You first need to login to your CodeMC Account and head towards the project you own that should have automatic deployments setup.

### Configure Project
How you configure your project is slightly different depending on the build manager you use.

/// tab | :simple-gradle: Gradle (Freestyle Project)
1.  Press the :octicons-gear-16: **Configure** button on the left-hand side.
2.  Scroll to the **Build Environment** Section and press **Use secret text(s) or file(s).
3.  In the appearing sub-menu, press **Add** and select **Username and password (separated)**
4.  For the **Username Variable** and **Password Variable** text boxes, set a fitting name to use.
    
    //// warning | Important
    These text boxes are NOT for your actual username and password. They are used to set the Environment Variable names that jenkins should use to get the respective values.
    ////
    
5.  Set **Credentials** to **nexus-repository** if it isn't selected already.
6.  Move to the **Build** Section.
    - Should you not have any Build settings yet, follow these steps:
        - Press **Add build step** and select **Invoke Gradle script**.
        - Press **Use Gradle Wrapper** and make sure that **Make gradlew executable** is checked.
        - Set `clean publish` as the value for the **Tasks** field. You may add additional tasks if needed.
    - Should you already have Build settings, update them to execute the `publish` task.
7. Save your changes.
///

/// tab | :simple-apachemaven: Maven
Unlike Gradle does Maven not require any particular preparations, as the Jenkins service will automatically inject the required username and password from its global configuration to use.

Should you not have a Build task yet in your **Build** section, follow these steps:

1. Change **Maven Version** to that of your project's and set **Root POM** to the path to your main `pom.xml` file (Usually just `pom.xml`).
2. In the **Goals and options** field, put `clean install deploy`. You may add additional tasks if needed.
3. Save your project.

In case you already have a Build task, make sure that **Goals and options** includes `deploy`.
///

## Configure your Build files
Once your Jenkins Project is ready can you update your `pom.xml`, `build.gradle` or `build.gradle.kts`, depending on the tool used.

/// tab | :simple-apachemaven: pom.xml
Add or update the following section to your `pom.xml` file:
```xml { .annotated title="pom.xml" }
<distributionManagement>
    <repository>
        <id>codemc</id>
        <url>https://repo.codemc.io/repository/{username}/</url> <!-- (1) -->
    </repository>
</distributionManagement>
```

1. Replace `{username}` with your **lowercased** GitHub Username used to login to CodeMC.
///

/// tab | :simple-gradle: build.gradle
[:octicons-file-code-16: Source](https://docs.gradle.org/current/userguide/publishing_maven.html#publishing_maven:complete_example){ target="_blank" rel="nofollow" }

//// info |
Press the :material-plus-circle: icon for extra info.
////

Add or update the following parts:
```groovy { .annotate title="build.gradle" }
plugins {
    // Other plugins
    id 'maven-publish'
}

// Other content (Group, version, ...)

publishing {
    publication {
        mavenJava(MavenPublication) {
            groupId = project.group
            artifactId = "projectname"
            version = project.version
            
            from components.java
        }
    }
    
    repositories {
        maven {
            url = "https://repo.codemc.io/repository/{username}/" // (1)
            
            // (2)
            def mavenUsername = System.getenv("GRADLE_PROJECT_MAVEN_USERNAME")
            def mavenPassword = System.getenv("GRADLE_PROJECT_MAVEN_PASSWORD")
            
            if (mavenUsername != null && mavenPassword != null) {
                credentials {
                    username = mavenUsername
                    password = mavenPassword
                }
            }
        }
    }
}
```

1. Replace `{username}` with your **lowercased** GitHub Username used to login to CodeMC.
2.  You need to replace `GRADLE_PROJECT_MAVEN_USERNAME` and `GRADLE_PROJECT_MAVEN_PASSWORD` with the values you have defined in the [Prerquisites](#prerequisites) section of this page.  
    Do **NOT** directly set the username and password here, as it would allow anyone to take and use it!
///

/// tab | :simple-kotlin: build.gradle.kts
[:octicons-file-code-16: Source](https://github.com/Minecrell/ServerListPlus/blob/ef8cda91cc73a4599c359640c4e97dde9b699649/build.gradle.kts#L146-L178){ target="_blank" rel="nofollow" }

Add or update the following parts:
```kotlin { title="build.gradle.kts" }
plugins {
    // Other plugins
    `maven-publish`
}

publishing {
    publications {
        create<MavenPublication>("mavenJava") {
            groupId = project.group
            artifactId = "projectname"
            version = project.version
            
            from(components["java"])
        }
    }
    
    repositories {
        val mavenUrl: String? by project
        val mavenSnapshotUrl: String? by project
        
        (if(version.toString().endsWith("SNAPSHOT")) mavenSnapshotUrl else mavenUrl)?.let { url ->
            maven(url) {
                val mavenUsername: String? by project
                val mavenPassword: String? by project
                if(mavenUsername != null && mavenPassword != null) {
                    credentials {
                        username = mavenUsername
                        password = mavenPassword
                    }
                }
            }
        }
    }
}
```
///