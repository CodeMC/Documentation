# Setup GitLab Integration
CodeMC supports integrating with [GitLab](https://gitlab.com){ target="_blank" rel="nofollow" } for features such as creating new builds on commits or return a build status on Pull requests, commits, etc.  
This page tries to explain how you can enable such features.

## Setup Automatic Builds
CodeMC allows to create new builds whenever commits are done to a connected GitLab Repository. The full steps are available in the [GitLab Documentation](https://docs.gitlab.com/ee/integration/jenkins.html#configure-the-jenkins-project).

1. First, go to your Jenkins Job, and click on the :octicons-gear-16: **Settings** tab.
2. Select *Build when a change is pushed to GitLab* checkbox, then scroll down to the *Advanced Tab*.
3. Once you click on the Advanced Tab, Navigate to the *Secret Token* Text Box.
4. Click on `Generate`, copy the text inside the text bar, and save your Jenkins Configuration.
5. In your GitLab Project, create a webhook with the trigger url as `https://ci.codemc.io/project/{USERNAME}/{JOB_NAME}`.
6. Paste the copied token in the *Secret Token* text bar.
7. Test the webhook by pressing the *Test* Button.

## Setup a Commit Status
You can add a Commit Status to your repository to display wether a build was successful or not when a commit was made. Full instructions are available on [GitLab](https://docs.gitlab.com/ee/integration/jenkins.html#configure-the-jenkins-project).
To add a Commit status, follow these steps:

1. In your Jenkins project, click on the :octicons-gear-16: **Settings** tab.
2. Navigate to the *Post-build Actions* section.
3. Upon clicking on *Add post-build Action*, click on the one titled *Publish build status to GitLab*.

If you are using a freestyle or Maven project, your process is done. However, if you are using a Pipeline project, continue with the steps below.

1.  Moving back to your project, create or locate the `Jenkinsfile` inside the root directory.
2.  Inside of the `Jenkinsfile`, create a stage that sets the build status for your project:
    ```groovy
    pipeline {
        agent any
        
        stages {
            stage('gitlab') {
                steps {
                    echo 'Notify GitLab'
                    updateGitlabCommitStatus name: 'build', state: 'pending'
                    updateGitlabCommitStatus name: 'build', state: 'success'
                }
            }
        }
    }
    ```
