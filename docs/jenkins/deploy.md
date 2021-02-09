# Deploying to the CodeMC Nexus
CodeMC offers you a way to upload your API or project to a nexus, so that other developers can integrate it into their own projects to use.  
This page here will explain how you can achieve this.

!!! info "Important"
    You can only deploy your project to the nexus from within your Jenkins Project.  
    If you try to deploy from outside of it will you receive an "Unauthorized" exception.

## Prerequisites
Before you can publish your project to the nexus will you need to make a few first steps to have everything setup and running.

### Login
To get started, first go to your project's Jenkins Page on CodeMC (https://ci.codemc.io/job/:user/job/:project) and login to your account if you didn't already.

### Configure Project
On the project's page, click *:fontawesome-solid-cog: Configure* to go to the project settings.  
From there, scroll down to the *Build Enviroment* section and click on *Use secret text(s) or file(s)*.

A new section called *Bindings* should now open. Click the *Add* button and select *Username and password (separated)*.  
You should now see two text fields called *Username Variable* and *Password Variable* respectively. Enter the names for the User and Password Variable that you want to use.  
Common examples to use are `ORG_GRADLE_PROJECT_mavenUsername` and `ORG_GRADLE_PROJECT_mavenPassword`

!!! warning "Note"
    Do NOT enter your actual username and password in those fields. They are only used to define the Enviroment Variables used on Jenkins.

Under *Credentials* leave *Specific credentials* selected and use *jenkins-deploy/\*\*\*\*\*\* (jenkins-deploy)* from the dropdown menu.

Continue to the *Build* section.

!!! info "No Build step set?"
    If you don't have a Build set create one as follows:
    
    **Maven**:
    
    1. Leave *Maven Version* to that of your maven used and set *Root POM* to the path to your pom.xml file (Usually just `pom.xml`).
    2. In the *Goals and options* field, put `clean install deploy`
    
    **Gradle**
    1. Click *Add build step* and select *Invoke Gradle script*.
    2. Click *Use Gradle Wrapper* and make sure that *Make gradlew executable* is checked.
    3. In the *Tasks* field put `clean publish`

----
## Maven
After you've setup your Jenkins Project properly can you now continue to configure your Maven project.

In your Project's `pom.xml` can you add the following info:

!!! info ":brands-maven: pom.xml"
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

After that can you just publish it to your GitHub and trigger a build on CodeMC.

----
## Gradle
After you've setup your Jenkins Project properly can you now continue to configure your Gradle project.

How you configure your project depends on whether you use the Groovy or the Kotlin distribution of Gradle.

!!! info "Gradle"
    === ":brands-gradle: build.gradle"
        [:fontawesome-solid-file-code: Source](https://docs.gradle.org/current/userguide/publishing_maven.html#publishing_maven:complete_example)  
        ```groovy
        plugins {
            id 'maven-publish'
        }
        
        group = "your.project.group"
        version = "1.0.0"
        
        publishing {
            publications {
                mavenJava(MavenPublication) {
                    groupId = group
                    artifactId = "YourArtifactName"
                    version = project.version
                    
                    from components.java
                }
            }
            
            repositories {
                maven {
                    def snapshotUrl = "https://repo.codemc.io/repository/maven-snapshots/"
                    def releaseUrl = "https://repo.codemc.io/repository/maven-releases/"
                    
                    url = project.version.endsWith("SNAPSHOT") ? snapshotUrl : releaseUrl
                    
                    def mavenUsername = System.getenv("ORG_GRADLE_PROJECT_mavenUsername") ? System.getenv("ORG_GRADLE_PROJECT_mavenUsername") : null
                    def mavenPassword = System.getenv("ORG_GRADLE_PROJECT_mavenPassword") ? System.getenv("ORG_GRADLE_PROJECT_mavenPassword") : null
                    
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
    
    === ":brands-kotlin: build.gradle.kts"
        [:fontawesome-solid-file-code: Source](https://github.com/Minecrell/ServerListPlus/blob/master/build.gradle.kts#L146-L178)  
        ```kotlin
        plugins {
            'maven-publish'
        }
        
        group = "your.project.group"
        version = "1.0.0"
        
        publishing {
            publications {
                create<MavenPublication>("mavenJava") {
                    groupId = group
                    artifactId = "YourArtifactName"
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
