# GitHub Integrations
Below can you find some tutorial to integrate the CI server of CodeMC into GitHub (or vice-versa).

## Add CommitStatus
To add a CommitStatus of CodeMC to GitHub, follow these basic steps:

1. Go to https://github.com/settings/tokens
2. Click `Generate new token`
3. Give the token a descriptive name (i.e. `CodeMC-CommitStatus`) and grant it the following Scopes:
    - `repo`
    - `admin:repo_hook`
    - `admin:org_hook`
4. Click on `Generate token` and copy the generated code.
5. Head over to https://ci.codemc.io/job/:organisation (replace `:organisation` with your user/organisation name)
6. Click on `Configure` and under Projects, click the `Add` button right next to the `Credentials` field.
7. A drop-down menu should now open. Click your user/organisation name.
8. Eneter your username and use the copied token as password. Then Click `Add`.
9. Select the credentials in the drop-down menu and click `Save`.
10. You're done!

----
## Automatically build
When you want CodeMC to automatically build artefacts once you push commits to your repository, can you follow these steps:

### Organisations

!!! info "Important"
    These webhooks will work for events fired on repositories of the entire Organisations.  
    If you only want webhooks to be triggered for specific repositories, setup one for a [specific repository](#repositories)

1. Go to https://github.com/organizations/:organisation/settings/hooks (Replace `:organisation` with the name of your organisation).
2. Click `Add webhook`
3. Put https://ci.codemc.io/github-webhook/ as the Payload URL.
4. Under `Which events would you like to trigger this webhook?` select `Let me select individual events` and enable the below options:
    - `Pull requests`
    - `Pushes`
    - `Repositories`
    
    !!! info "Note"
        You can also leave the setting on "Just the `push` event" if you only want pushes to trigger it
5. Click `Add Webhook`
6. You're done!

### Repositories

1. Go to https://github.com/:user/:repo/settings/hooks (Replace `:user` with your user/organisation name and `:repo` with the repository name).
2. Click `Add webhook`
3. Put https://ci.codemc.io/github-webhook/ as the Payload URL.
4. Under `Which events would you like to trigger this webhook?` select `Let me select individual events` and enable the below options:
    - `Pull requests`
    - `Pushes`
    - `Repositories`
    
    !!! info "Note"
        You can also leave the setting on "Just the `push` event" if you only want pushes to trigger it
5. Click `Add Webhook`
6. You're done!
