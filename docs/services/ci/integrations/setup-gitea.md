# Setup Gitea/Forgejo support

/// note
The following instructions also apply to [Forgejo instances](https://forgejo.org/){ target="_blank" rel="nofollow" }.
///

CodeMC supports hooking into [Gitea](https://about.gitea.com/){ target="_blank" rel="nofollow" } instances for creating new builds whenever a commit is done to your project.

## Setup automatic Builds

CodeMC allows you to create builds whenever a commit is pushed to your repository.  
Unlike other Sites is the setup for Gitea/Forgejo a little more complicated and requires some steps on the CI first.

/// warning | Important
Using this setup will trigger a build no matter the changes or targeted files.  
It will ignore any exclusion/inclusion settings of the Polling options.

Use the [Periodic Builds](#setup-periodic-builds) setup to avoid this.
///

1. Login to your account on `https://ci.codemc.io` if you haven't already.
2. Click your username on the top-right.
3. Click **Security** on the left-hand side.
4. Under **API Token** press **Add new Token**, give the token a proper name and press **Generate**.
5. Copy the token.
6. Encode the token alongside your Username in the format `{username}:{token}` using a Base64 encoder (i.e. [base64encode.org](https://base64encode.org){ target="_blank" rel="nofollow" }).
7. Copy the generated Base64 code for later.

After completing the above steps, head over to your Gitea/Forgejo repository and follow these steps.

1. Press :octicons-tools-16: **Settings**
2. Press **Webhooks** on the left-hand side.
3. Press the **Add Webhook** button and select :simple-gitea: **Gitea** (:simple-forgejo: **Forgejo** may also work).
4. Add `https://ci.codemc.io/job/{username}/job/{project}/build` as the target URL.
5. Under **Trigger on** either leave it at `push events` or chose `Custom events...` and choose the following:
    - `Pull request`
    - `Push`
6. Under **Authorization-Header** put `Basic {code}` where `{code}` is the Base64-encoded text you've created previously.
7. Press **Add Webhook** to save your new Webhook.

## Setup periodic Builds

If you don't need to have builds made when a commit is pushed can periodic builds be used instead to regularely check your repository for changes and build those.

1.  Login to your account on `https://ci.codemc.io` if you haven't already.
2.  Head over to your project on CodeMC and open the settings by clicking :octicons-gear-24: **Configure**.
3.  Under :octicons-git-branch-24: **Source Code Management** make sure that **Git** is selected and that the URL to your repository is configured under **Repository URL**
    - Make sure that **Branch Specifier (blank for 'any')** is set to the default branch of your repository (Usually `*/master` or `*/main`).
    - *Optional:* Under **Additional Behaviours** press the **Add** button and add **Polling ignores commits in certain paths** to add settings to define paths that should be included or excluded during a poll.
4.  Scroll down to the **Build Triggers** section and make sure to check **Poll SCM**
5.  In the **Schedule** field, add a cron-job-compatible pattern. [crontab.guru]{ target="_blank" rel="nofollow" } can be used to create one.  
    Please keep the frequency of polls to a reasonable number such as every 15 minutes (`H/15 * * * *`)
    
    /// tip
    `H` should be used instead of `*` when defining a interval for the polling.
    
    Using `H` tells the CI to delay the poll should too many other polls already be run at the same time, reducing load on the CI in general.  
    Note that `H` is not a supported cron-job pattern and specific to the CI. Sites such as [crontab.guru]{ target="_blank" rel="nofollow" } will not support it.
    ///

6.  Press **Save** to save and apply your changes.

[crontab.guru]: https://crontab.guru/