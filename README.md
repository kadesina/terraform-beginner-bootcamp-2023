# Terraform Beginner Bootcamp 2023

## Semantic Versioning :image:

This project is going utiize semantic versioning for its tagging.
[semver.org](https://semver.org/)

The general format:

**MAJOR.MINOR.PATCH**, eg. `1.0.1`

- **MAJOR** version when you make incompatible API changes
- **MINOR** version when you add functionality in a backward compatible manner
- **PATCH** version when you make backward compatible bug fixes
            Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.

## Install the Terraform CLI 

### Considerations with the Terraform CLI chnmages
The Terrafor CLI installation instruction have changed due to gpg keyring changes. So we needed refer to the latest install CLI instructions via Terraform Documenttion and change the scripting for install

[Install Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

### Condieration for Linux Distribution 

This project is built against ubuntu 
Please consider checking your Linux Disttubtion and change accordingly to distrubtion needs. 

[How to check OS Version in linux](
https://www.cyberciti.biz/faq/how-to-check-os-version-in-linux-command-line/)


Example of Checking OS version
```bash
$ cat /etc/os-release
PRETTY_NAME="Ubuntu 22.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.3 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy

```

### Refactoring into Bash Scripts 

While fixing the Terraform CLI gpg depreciation issues we notice the bash scripts steps were a considerable amount more code so we decided to create a bash script to install the Terraform CLI 

This bash script is located here: [./bin/install_terraforma_cli](./bin/install_terraform_cli)

- This will keep the Gitpode Task ([.gitpod.yml](.gitpod.yml)) file tidy 
- This allow us an easier to debug and excute manually Terraform CLI install 
- This will allow better portability for other projects that need to install Terraform CLI 

#### Shebang 

A Sheband  (pronounced Sha-bang) tells the bash script what program that will interpret the script 

ChatGPT recommended this format for bash: `#!/usr/bin/env bash`

- for portability for different os distributions 
- will search the user's Path for the bas executable 


https://en.wikipedia.org/wiki/Shebang_(Unix)

## Excecution Considerations

When executing the bash script we can use the `./` shorthand notiation to execute the bash script. 

eg. `./bin/install_terraform_cli`

If we are using a script in .gitpod.ymal we need to point the script to a program to interperit it. 

#### Linux Permissions Considerations 

In ordert to make our bash scriopts executable we need to change linux permission for the fix to be executable at the user mode.

```sh
chmod u+x ./bin/install_terraform_cli
```

alternatively: 

```sh
chmod 744 ./bin/install_terraform_cli 

```


https://en.wikipedia.org/wiki/Chmod

### Github Lifecycle (Before, Inti, Command)

We need to be careful when using the Init because it will not return of we restart an existing workspace. 
https://www.gitpod.io/docs/configure/workspaces/tasks



