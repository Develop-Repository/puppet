# A Puppet Control Repository

- [A Puppet Control Repository](#a-puppet-control-repository)
  - [What You Get From This control-repo](#what-you-get-from-this-control-repo)
  - [Copy This Repo Into Your Own Git Server](#copy-this-repo-into-your-own-git-server)
    - [GitHub](#github)
    - [GitHub Enterprise](#github-enterprise)
  - [Code Manager Setup](#code-manager-setup)


## What You Get From This control-repo

This is a template [control repository](https://puppet.com/docs/pe/latest/code_management/control_repo.html) that has the minimum amount of scaffolding to make it easy to get started with [r10k](https://puppet.com/docs/pe/latest/code_management/r10k.html) or Puppet Enterprise's [Code Manager](https://puppet.com/docs/pe/latest/code_management/code_mgr.html).

The important files and items in this template are as follows:

* Basic example of roles and profiles.
* An example Puppetfile with various module references.
* An example Hiera configuration file and data directory with pre-created common.yaml and nodes directory.
  * These match the default hierarchy that ships with PE.
* An [environment.conf](https://puppet.com/docs/puppet/5.3/config_file_environment.html) that correctly implements:
  * A site-modules directory for roles, profiles, and any custom modules for your organization.
  * A config\_version script.
* An example [config\_version](https://puppet.com/docs/puppet/5.3/config_file_environment.html#configversion) script that outputs the git commit ID of the code that was used during a Puppet run.

Here's a visual representation of the structure of this repository:

```
puppet/
├── data/                                 # Hiera data directory.
│   ├── nodes/                            # Node-specific data goes here.
│   └── common.yaml                       # Common data goes here.
├── manifests/
│   └── site.pp                           # The "main" manifest that contains a default node definition.
├── scripts/
│   ├── code_manager_config_version.rb    # A config_version script for Code Manager.
│   ├── config_version.rb                 # A config_version script for r10k.
│   └── config_version.sh                 # A wrapper that chooses the appropriate config_version script.
├── site-modules/                         # This directory contains site-specific modules and is added to $modulepath.
│   ├── profile/                          # The profile module.
│   └── role/                             # The role module.
├── LICENSE
├── Puppetfile                            # A list of external Puppet modules to deploy with an environment.
├── README.md
├── environment.conf                      # Environment-specific settings. Configures the modulepath and config_version.
└── hiera.yaml                            # Hiera's configuration file. The Hiera hierarchy is defined here.
```

## Copy This Repo Into Your Own Git Server

To get started with using the control-repo template in your own environment and git server, we've provided steps for the three most common servers we see: [GitLab](#gitlab), [BitBucket](#bitbucketstash), and [GitHub](#github).

### GitHub

Follow [GitHub's documentation](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-repository-from-a-template) to create your control repository starting from this template.

<img width="429" alt="template button" src="https://user-images.githubusercontent.com/1392917/117215366-f4eeb280-adb2-11eb-9108-1bd45c4d98f3.png">


### GitHub Enterprise

1. Prepare your local git client to authenticate with a **local GitHub Enterprise instance**.
    * <https://help.github.com/articles/generating-ssh-keys/>
    * <https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/>
1. Create a repository called `control-repo` in your user account or organization. Ensure that "Initialize this repository with a README" is not selected.
    * <https://help.github.com/articles/creating-a-new-repository/>
1. Make a note of your repository URL (HTTPS or SSH, depending on your security configuration).
1. Clone this control repository to your laptop/workstation:
    * `git clone https://github.com/Develop-Repository/puppet`
    * `cd control-repo`
1. Remove this repository as the origin remote:
    * `git remote remove origin`
1. Add your internal repository as the origin remote:
    * `git remote add origin <url of your github repository>`
2. Push the production branch of the repository from your machine up to your git server
    * `git push origin production`

## Code Manager Setup

If you use Puppet Enterprise and have not yet enabled and configured Code Manager, in addition to reading the official [documentation](https://puppet.com/docs/pe/latest/code_mgr.html) for enabling it, you may want to look at the Ramp-Up Program's control repository instead of this one. It's similar to this repo except that it has batteries included, so to speak. There are pre-built profiles for configuring Code Manager, generating SSH keys, and setting up your Git server to work with Code Manager.

* <https://github.com/Puppet-RampUpProgram/control-repo>
