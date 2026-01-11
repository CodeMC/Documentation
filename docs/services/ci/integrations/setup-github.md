# Setup GitHub Integration

CodeMC supports integrating with [GitHub](https://github.com){ target="_blank" rel="nofollow" } for features such as creating new builds on commits or return a build status on Pull requests, commits, etc.  
This page tries to explain how you can enable such features.

## Setup Automatic Builds

CodeMC allows to create new builds whenever commits are done to a connected GitHub Repository.  
The setup can be done either for an entire Organization, meaning that it applies to all repositories hosted on that Organization, or for a specific repository alone.

1. Go to https://github.com/apps/codemc-ci and install the **CodeMC CI** app to your repositories/organizations.
2. Go to your Jenkins build job settings, enable the **GitHub hook trigger for GITScm polling** option.

## Setup a Commit Status

1. Go to https://github.com/apps/codemc-ci and install the **CodeMC CI** app to your repositories/organizations.
2. Go to your Jenkins build job settings.
3. Add the **CodeMC Set GitHub Commit Status to PENDING** pre-build step, leave the default credentials.
4. Add the **CodeMC GitHub Commit Status** post-build actions, leave the default credentials.
