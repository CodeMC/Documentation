# Setup GitHub Integration

CodeMC supports integrating with [GitHub](https://github.com){ target="_blank" rel="nofollow" } for features such as creating new builds on commits or return a build status on Pull requests, commits, etc.  
This page tries to explain how you can enable such features.

## Setup Automatic Builds

CodeMC allows to create new builds whenever commits are done to a connected GitHub Repository.  
The setup can be done either for an entire Organization, meaning that it applies to all repositories hosted on that Organization, or for a specific repository alone. The steps are the same, except for where you access the settings:

/// note
Organizations require to have the [CodeMC Application](https://github.com/settings/connections/applications/2debe3b061b244423bf5){ target="_blank" rel="nofollow" } approved to properly access the Organization on the CI.
///

1. Go to your Organization/Repository and press the :octicons-gear-16: **Settings** Tab.
2. Click :octicons-webhook-16: **Webhooks** on the left sidebar.
3. Click the **Add Webhook** Button on the top-right of the page.
4. Add `https://ci.codemc.io/github-webhook/` as the value of **Payload URL**.
5. For **Which events would you like to trigger this webhook?** either leave it at *"Just the `push` event."* or select *"Let me select individual events."* and select the following options:
    - `Pull requests`
    - `Pushes`
    - `Repositories`
6. Save your Webhook by clicking the **Add webhook** button at the bottom.

## Setup a Commit Status

/// danger | Work in Progress
This section is currently being reworked and not available right now.
///