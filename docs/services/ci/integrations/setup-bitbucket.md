# Setup BitBucket Integration
CodeMC supports integrating with [BitBucket](https://bitbucket.org){ target="_blank" rel="nofollow" } for creating new builds on commits, pull requests, or other events.

## Setup Automatic Builds
CodeMC allows to create new builds whenever commits are done to a connected BitBucket Repository.

1. Go to your repository and press the :octicons-gear-16: **Settings** Tab.
2. Click :octicons-webhook-16: **Webhooks** inside the column.
3. Click the **Add Webhook** Button on the top-right of the page.
4. Add `https://ci.codemc.io/bitbucket-webhook/` as the value of the **URL**.
5. For **Title**, set it to something recognizable (e.g. `CodeMC`).
6. For **Which events would you like to trigger this webhook?** either leave it at *"Repository push"* or select *"Choose from a full list of triggers"* and select the following options:
    - `Pull requests`
    - `Pushes`
    - `Repositories`
7. Save your Webhook by clicking the **Add webhook** button at the bottom.