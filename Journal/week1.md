# Terraform Beginner Bootcamp 2023 - Week 1

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