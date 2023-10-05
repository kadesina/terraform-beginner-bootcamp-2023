# Terraform Beginner Bootcamp 2023 - Week 1

## Fixing Tags 

[How to Delete local and remote Tags on Git](https://devconnected.com/how-to-delete-local-and-remote-tags-on-git/)

Locall delete a tag
```sh
$ git tag -d <tag_name>
```

Remotely delete tag
```sh
$ git push --delete origin tagname
```
Checkout the commit that you want to retag. Grab the sha from your Github history 

```sh
git checkout <SHA>
git tag M.M.P
git psuh --tags
git checkout main
```

## Root Module Structure 

Our root module structure is as follows:

```
Projects_ROOT
|
|-- variable.tf         # stores the structure of input variables
|-- main.tf             # everything else
|-- providers.tf        # define required providers and their configuration
|-- outputs.tf          # stores our outputs
|-- terraform.tfvars    # the data of variables we want to load in our Terraform project
|-- README.md           # required for root modules
```

[Standard Module Structure](https://developer.hashicorp.com/terraform/language/modules/develop/structure)

## Terraform Cloud Variables 

In terraform we can set two kind of variables:
- Enviroment Variables - those you would set in your bash terminal eg. AWS
credentials
- Terraform Variables - those that you would normally set in your tfvars files 

We can set Terraform Clouyd vatiables to be sensitive so they care not shown visibliy in the UI. 

### Loading Terraform Input Variables 

[Terraform Input Variables](https://developer.hashicorp.com/terraform/language/values/variables)

we can use the `-var` flag to set an input variable or override a variable in the tfvars file eg. `terraform -var user_ud="my-user_id"`

### var-file flag

- TODO: document research this flag

### terraform.tvfars

This is the default file to load in terraform variables in blunk 

### auto.tfvars

- TODO: document this functionality for terraform cloud 

### order of terraform variables 

- TODO: document which terraform variables take presedence

## Dealing With Configuration Drift 


## What happens if we lose our state file? 

If you lose your statefil, you most likely have to tear dwon all your cloud infrastructure manually. 

You can use terraform port but it wont work for all cloud resurces. You need to check the terraform providers documentation for which resources support import. 

### Fix Missing Resource with Terraform Import 

`terrafrom import aws_s3_bucket.example`

[Terrafrom Import](https://developer.hashicorp.com/terraform/cli/import)

[AWS S3 Bucket Import](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket#import)

### Fix Manual Configuration 

If someone goes and deletes or modifies cloud resource manually through Clickops. 

If we run Terraform plan is with attempt to put our infrastuctre back into the expected state fixing configuration Drift 

## Fix using Terraform Refresh 

```sh
terraform apply -refresh-only -auto-approve
```
## Terraform  Modules 

### Terrafrom Module Structure 

It is recommend to place modules in a `modules` directoy when locally developing modules but you can name it whatever you like. 

 
### Passing Input Variables 

We can pass input variable to our module 

The module has to declater the terraform variables in its own variable.tf

```tf
module "terrahouse_aws"{
  source = "./modules/terrahouse_aws"
  user_uuid = var.user_uuid
  bucket_name = var.bucket_name
}
```

### Modules Sources 

Using the source we can import the modules from various places ed:
- Locally 
- Github 
- Terrafrom Registry 

```tf
module "terrahouse_aws"{
  source = "./modules/terrahouse_aws"
}
```


[Module Sources](https://developer.hashicorp.com/terraform/language/modules/sources#github)

## Considerations when using ChatGPT to write Terraform 


Large language Modules such as ChatGpt may not be trained on the latest documentation or information about Terraform.

It may likely produce older examples that could be deprecated. Often affecting providers. 

## Working with files in Terraform 

### File Exits function

This is a builtin terraform function to check the existance of a file. 

```tf
condition = fileexists(var.error_html_filepath)
```
https://developer.hashicorp.com/terraform/language/functions/fileexists

### Filemd5

https://developer.hashicorp.com/terraform/language/functions/filemd5

### Path Variable

In terraform there is a special variable called `path` that allows us to reference local paths:
- path.module = get the path for thee current module 
- path.root = get the path for the root module 
[Special Path VAriable](https://developer.hashicorp.com/terraform/language/expressions/references)


resource "aws_s3_object" "index_html" {
  bucket = "terrabyken"
  key    = "index.html"
  source = "{path.root}/public/index.html"
}

