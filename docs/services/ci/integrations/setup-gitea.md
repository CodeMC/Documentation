# Setup Gitea support

/// note
The following instructions also apply to [Forgejo instances](https://forgejo.org/){ target="_blank" rel="nofollow" }.
///

CodeMC supports hooking into [Gitea](https://about.gitea.com/){ target="_blank" rel="nofollow" } instances for creating new builds whenever a commit is done to your project.

## Setup automatic Builds

CodeMC allows you to create builds whenever a commit is pushed to your repository.  
The setup can be done either for an entire organization, or a specific repository. The steps are the exact same except for where you apply the changes.

1. Go to your Organization/Repository and press :octicons-tools-16: **Settings**
2. Press **Webhooks** on the left-hand side.
3. Press the **Add Webhook** button and select :simple-gitea: **Gitea**.
4. Add `https://ci.codemc.io/...` as the target URL.
5. Under **Trigger on** either leave it at `push events` or chose `Custom events...` and choose the following:
    - `Pull request`
    - `Push`
    - `Repository`
6. Press **Add Webhook** to save your new Webhook.