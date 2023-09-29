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
