# Setup GitHub Integration
CodeMC supports integrating with [GitHub](https://github.com){ target="_blank" rel="nofollow" } for features such as creating new builds on commits or return a build status on Pull requests, commits, etc.  
This page tries to explain how you can enable such features.

## Setup Automatic Builds
CodeMC allows to create new builds whenever commits are done to a connected GitHub Repository.  
The setup can be done either for an entire Organization, meaning that it applies to all repositories hosted on that Organization, or for a specific repository alone. The steps are the same, except for where you access the settings:

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
The below section is not yet completed and still a work in progress!  
Any information displayed may not be up-to-date.
///

You can add a Commit Status to your repository to display wether a build was successful or not when a commit was made.  
To add a Commit status, follow these steps:

1.  Go to your Token settings found at https://github.com/settings/tokens
2.  Click **Generate new Token** :octicons-triangle-down-16: and choose either **Generate new token (classic)**
3.  Provide a descriptive name/description in **Note** to know what the token is for (i.e. `CODEMC_CI_TOKEN`).
4.  Set an Expiration (Default is 30 Days).
    
    /// note | Recommendation
    For optimal security is it recommended to **not** set the Expiration to *No expiration*, as this would be a high security risk.
    ///

5.  Check the following Scopes:
    - `repo`
    - `admin:repo_hook`
    - `admin:org_hook`
6.  Click the **Generate token** button at the bottom and copy the generated token.
7.  Go to your User/Organization on CodeMC that should use this token (`https://ci.codemc.io/job/{user|organization}`).