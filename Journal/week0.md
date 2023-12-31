# Terraform Beginner Bootcamp 2023 - Week 0

- [Semantic Versioning :image:](#semantic-versioning--image-)
- [Install the Terraform CLI](#install-the-terraform-cli)
  * [Considerations with the Terraform CLI chnmages](#considerations-with-the-terraform-cli-chnmages)
  * [Condieration for Linux Distribution](#condieration-for-linux-distribution)
  * [Refactoring into Bash Scripts](#refactoring-into-bash-scripts)
    + [Shebang](#shebang)
- [Excecution Considerations](#excecution-considerations)
    + [Linux Permissions Considerations](#linux-permissions-considerations)
- [Github Lifecycle](#github-lifecycle-before-inti-command)
  * [Working Env Vars](#working-env-vars)
    + [env command](#env-command)
    + [Seting and Usetting Env Vars](#seting-and-usetting-env-vars)
    + [Printing Vars](#printing-vars)
    + [Scoping of ENv Vars](#scoping-of-env-vars)
    + [Persisting Env Vars in Gitpod](#persisting-env-vars-in-gitpod)
  * [AWS CLI Installation](#aws-cli-installation)
    + [Get AWS Keys](#get-aws-keys)
- [Terraform Basics](#terraform-basics)
  * [Terraform Registry](#terraform-registry)
    + [Terraform Console](#terraform-console)
    + [Terraform init](#terraform-init)
    + [Terraform Plan](#terraform-plan)
    + [Terraform Apply](#terraform-apply)
    + [Terraform Destroy](#terraform-destroy)
    + [Terraform Lock Files](#terraform-lock-files)
    + [Terraform state Files](#terraform-state-files)
    + [Terraform Directory](#terraform-directory)
- [Issues with Terraform Cloud Login and Gitpod Workpspace](#issues-with-terraform-cloud-login-and-gitpod-workpspace)


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

## Github Lifecycle

We need to be careful when using the Init because it will not return of we restart an existing workspace. 
https://www.gitpod.io/docs/configure/workspaces/tasks



### Working Env Vars


#### env command


we can list out all Enviroment Variables (Env Vars) using the `env` command 

We can filter specific env vars using grep eg `env | grep AWS_`


#### Seting and Usetting Env Vars 

In the terminal we can set using `export HELLO= 'world`

In the terminal we unset using `unset HEllO`

we can set an env var temporarily when just running a command 


```sh
HELLO= 'world' ./bin/print_message
```
Within a bash scriopt we can set env without writing export eg. 

```sh
#!/usr/bin/env bash


HELLO= 'world'

echo $HELLO
```

#### Printing Vars

we can print an env var using echo eg. `echo $HELLO`

#### Scoping of ENv Vars 

WHen you open up new bash terminals in VSCode it will not be aware of env vars that you have set in another windows. 

If you want to EWNV Vars to persist across all future bash terminals that are open you need to set ev vars in your bash profile. eg. `.bash_profile`

#### Persisting Env Vars in Gitpod 

We can persist env vars into gitpod by storing them in Gitpod Secrets Storgae 

```
gp[ env HELLO='world']
```

All futrue workspace launhced will set env vars for all bsh terminals opened in those workspaces.

You can also set en vrs in the `.gitpod.yml` but this can only contian non-senstive env vars


### AWS CLI Installation

AWS CLI is installed for the project via the bash script [`.bin/install_aws_cli`](./bin/install_aws_cli)

[Getting Started Install (AWS. CLI)](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

[AWS CLI Env Vars](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html)

We can check if our aws credentials is configured correctly by running the following AWS CLI command: 

```sh
aws sts get-caller-identity
```
if it successful you should see a json payload return that looks like this: 

```json
{
    "UserId": "AIEA9DB6ZN52MS43EMB6V",
    "Account": "123456789012",
    "Arn": "arn:aws:iam::123456789012:user/kenny"
}

```


We'll need to generate AWS CLI crdits from IAM User in order to use AWS CLI
#### Get AWS Keys 

$ env | grep aws_

## Terraform Basics


### Terraform Registry 

Terraform sources their providers and modules from the Terraform registry which loacted at [registry terrform.io](https://registry.terraform.io/)

- **Providers** is an interface to API that will allow to create  resources in terraform 
- **Modules** are a way to make large amount of terraform code modular, portable and sharable. 

[Random Terraform](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/string)

#### Terraform Console 

We can see a list of all the Terraform commands by simply typing `terraform`

#### Terraform init

At the start of a new terraform project we will run `terraform init` to download the binaries for the terraform providers that we'll use in this project.

#### Terraform Plan

`terraform plan`
This will generate out a changeset, about the state of our infratructure and what will be changed. 

We can output this changeset ie. "plan" to be passed to an apple, but often you can just ignore outputting.

#### Terraform Apply

This will run a plan and pass the changeset to be executed by terraform. Apply should prompt yes or no. 

If we want automatically approve an apply, we can provide the auto approve flag eg. `terraform apply --auto-approve`

#### Terraform Destroy 

`terraform destroy`
This will destroy resources

You can alsao use the auto approve flag t skip the approve prompt eg.
`terraform apply --autoapprove`

#### Terraform Lock Files 

`.terraform.lock.hcl` containd the locked versioning for the providers or modules that should be used with this project.

The Terraform Lock files should be committed to your Version Control System (VSC) eg. Github

#### Terraform state Files 

`.terraform.tfstate` contains information about the current state of your infrastructure. 

This file **should not be commnited88 to your VCS. 

This file can contian sensitive data. 

If you lose this file, you lose knowing the state of your infrastructure. 

`.terraform.tfstate.backup` is the previous state file state. 

#### Terraform Directory 

`.terraform` directiry contains binaries of terraform providers.

## Issues with Terraform Cloud Login and Gitpod Workpspace

When attempting to run `terraform login` it will launch bash a wishing view ti generate a token. However it does not work expected in Gitpod VsCODE in the browser.

The workaround is manually generated a token in Terraform Cloud 

```
https://app.terraform.io/app/settings/tokens
```

Then create the file manually here: 

```sh
touch /home/gitpod/.terraform.d/credentials.tfrc.json
open /home/gitpod/.terraform.d/credentials.tfrc.json
```
Provider the following code (replace  your token in the file):

```json
{
  "credentials": {
    "app.terraform.io": {
      "token": "YOUR_API_TOKEN"
  }
}
```

We have automated this workaround with the following bash script [./bin/generate_tfrc_credentials](bin/generate_tfrc_credentials)
