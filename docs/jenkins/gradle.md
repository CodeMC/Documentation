[Discord]: https://discord.gg/AGcFMu6

# Creating a Gradle Job
This page explains you step by step how to create a Build job on CodeMC for a Gradle Project.  
For how to add a Maven project, check the [Creating a Maven Job page](../maven).

## Creating the Job

!!! warning "Important"
    In order to create a job will you need to be added to the Site first, if you haven't already.  
    To get added, join the [Discord Server][Discord] and follow the instructions in the `#info` channel.

1. Go to https://ci.codemc.io/view/Author/job/:user/newJob (Replace `:user` with your user/organisation name)
2. Enter the job name in the top text box, and select `Freestyle project`. Click the `OK` button at the bottom of the page.
3. Your job is now created! You should be redirected to the configuration page.

## Configuration
Here are some recommendet configuration settings to set.

### SCM

1. In the `Source Code Management` (SCM) section, click on the `git` radio button.
2. Click on `Add repository` and paste your repository URL in the corresponding text field.
3. If you want to build only a specific branch, can you define it in the `Branch Specifier` field.

### Build Trigger (Optional)
Note that you can configure CodeMC to automatically build each time you push changes to GitHub.  
A tutorial for this can be found [here](../github-integration#automatically-build).

1. Click on `Poll SCM`
2. Put `*/5 * * * *` in the large text field, to make CodeMC check your GitHub project every 5 minutes.

### Build Environment (Optional)
It's recommended to enable `Add timestamps to the Console Output`

### Build

1. Click on `Add build step`
2. Select `Invoke Gradle script`
3. Click on the `Use Gradle Wrapper` radio button.
4. Click on `Make gradlew executable`.
5. Insert your task into the task field. This is often something like `clean build`

### Post-build Actions

1. Click on the `Add post-build action` button.
2. Select `Archive the artifacts`.
3. In `Files to archive` specify the folder, where Gradle puts the build artifacts (Usually `**/build/libs/*.jar`)

## Finishing

1. Click the `Save` button. All changes will now be saved and applied and you will be redirected to your job's page.
2. To launch your first build, click the `Build Now` button on the left side.
3. CodeMC will now queue a build job and execute it. If you want to see the console of it, click on the rotating icon next to the build number under the `Build History` section.
