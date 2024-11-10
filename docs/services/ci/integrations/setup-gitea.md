# Setup Gitea/Forgejo support

/// note
The following instructions also apply to [Forgejo instances](https://forgejo.org/){ target="_blank" rel="nofollow" }.
///

CodeMC supports hooking into [Gitea](https://about.gitea.com/){ target="_blank" rel="nofollow" } instances for creating new builds whenever a commit is done to your project.

## Setup automatic Builds

CodeMC allows you to create builds whenever a commit is pushed to your repository.  
Unlike other Sites is the setup for Gitea/Forgejo a little more complicated and requires some steps on the CI first.

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