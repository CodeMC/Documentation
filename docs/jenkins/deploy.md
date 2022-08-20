[source_gradle]: https://docs.gradle.org/current/userguide/publishing_maven.html#publishing_maven:complete_example
[source_gradle_kts]: https://github.com/Minecrell/ServerListPlus/blob/ef8cda91cc73a4599c359640c4e97dde9b699649/build.gradle.kts#L146-L178

# Deploying to the CodeMC Nexus
CodeMC offers you a way to upload your API or project to a Nexus Repository, so that other developers can integrate it into their own projects to use.  
This page here will explain how you can achieve this.

!!! info "Important"
    You can only deploy your project to the Nexus from within your Jenkins Project.  
    If you try to deploy from outside of it will you receive an "Unauthorized" exception.

## Prerequisites
Before you can publish your project to the nexus will you need to make a few first steps to have everything setup and running.

### Login
To get started, first go to your project's Jenkins Page on CodeMC (https://ci.codemc.io/job/:user/job/:project) and login to your account if you didn't already.

### Configure Project

#### :brands-gradle: Gradle

1. Click on *:fontawesome-solid-gear: Configure* on your Project's page to open the project settings.
2. Scroll down to the section *Build Enviroment* and click *Use secret text(s) or file(s)*.
3. A new section called *Bindings* appears. Click the *Add* button and select *Username and password (separated)*.
4. In the two appearing text fields, add a name for *Username Variable* and *Password Variable*  
    
    !!! warning "Important"
        Do NOT enter your actual username and password into those fields. They are used to define the Enviroment variables to use in your Gradle project for the username and password respectively.

5. Under *Credentials* leave *Specific credentials* selected and select *jenkins-deploy* from the dropdown menus.
6. Move to the *Build* section.
7. If you don't have a build setup yet, create one as follows:
    1. Click on *Add build step* and select *Invoke Gradle script*.
    2. Click on *Use Gradle Wrapper* and check that *Make gradlew executable* is active.
    3. Add `clean publish` into the *Tasks* field. You may add additional actions to this if you need them.
8. Save your project's changes.

#### :brands-maven: Maven

Maven doesn't require any specific preparations as the Jenkins will inject the required username and password from its global Maven configuation to use.  
If you don't have a Build setup in the *Build* section yet, do the following:

1. Change *Maven Version* to that of your project's and set *Root POM* to the path to your main `pom.xml` (Usually just `pom.xml`).
2. In the *Goals and options* field, put `clean install deploy`. You may add additional goals to this line if they are needed.
3. Save your project's changes.

----
## Configure your build files
After you've setup your Jenkins Project properly can you now continue to add the right information into your `pom.xml`, `build.gradle` or `build.gradle.kts` file.

### :brands-maven: Maven (`pom.xml`)

Add the following content to your `pom.xml` file:

```xml
<distributionManagement>
    <repository>
        <id>codemc-releases</id>
        <url>https://repo.codemc.io/repository/maven-releases/</url>
    </repository>
    <!-- Only needed when publishing snapshots -->
    <snapshotRepository>
        <id>codemc-snapshots</id>
        <url>https://repo.codemc.io/repository/maven-snapshots/</url>
    </snapshotRepository>
</distributionManagement>
```

### :brands-gradle: Gradle (`build.gradle`)

> [:fontawesome-solid-file-code: Source][source_gradle]  

In your `build.gradle` file, add the following:

```groovy
plugins {
    id 'maven-publish'
}

// Your other stuff like group, version, repositories, etc.

publishing {
    publications {
        mavenJava(MavenPublication) {
            groupId = project.group // Group instance of your project
            artifactId = "YourProjectName"
            version = project.version // Version instance of your project
            
            from components.java
        }
    }
    
    repositories {
        maven {
            def snapshotUrl = "https://repo.codemc.io/repository/maven-snapshots/"
            def releaseUrl = "https://repo.codemc.io/repository/maven-releases/"
            
            // You can also directly set the URL if you don't want to publish snapshots.
            url = project.version.endsWith("SNAPSHOT") ? snapshotUrl : releaseUrl
            
            // GRADLE_PROJECT_MAVEN_USERNAME and GRADLE_PROJECT_MAVEN_PASSWORD are the variables you defined in the previous section.
            def mavenUsername = System.getenv("GRADLE_PROJECT_MAVEN_USERNAME") ? System.getenv("GRADLE_PROJECT_MAVEN_USERNAME") : null
            def mavenPassword = System.getenv("GRADLE_PROJECT_MAVEN_PASSWORD") ? System.getenv("GRADLE_PROJECT_MAVEN_PASSWORD") : null
            
            if(mavenUsername != null && mavenPassword != null) {
                credentials {
                    username = mavenUsername
                    password = mavenPassword
                }
            }
        }
    }
}
```

### :brands-kotlin: Gradle Kotlin-DSL (`build.gradle.kts`)

> [:fontawesome-solid-file-code: Source][source_gradle_kts]  

In your `build.gradle.kts` file, add the following:

```kotlin
plugins {
    'maven-publish'
}

publishing {
    publications {
        create<MavenPublication>("mavenJava") {
            groupId = project.group // Group instance of your project
            artifactId = "YourProjectName"
            version = project.version // Version instance of your project
            
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

----
## Final steps

Once finished can you now push the changes to your repository and trigger a build on CodeMC to get your project published to the repository.  
See the [GitHub Integration](../github-integration) page on how to do this automatically.
