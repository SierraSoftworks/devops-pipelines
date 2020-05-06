# Azure DevOps Pipelines
**Templates to simplify common Azure DevOps pipelines**

This repository contains templates which can be used in Azure DevOps
pipelines to manage the deployment of common application types.

You can read more about how to use these templates on the official
[Azure DevOps documentation][docs], but broadly it boils down to
adding the following into your `azure-pipelines.yml` file.

```yaml
trigger:
 - master

resources:
    repositories:
        - repository: templates
          type: github
          name: SierraSoftworks/devops-pipelines
        
          # You might need to create a service connection to access GitHub
          endpoint: SierraSoftworks

extends:
    # Specify the template you wish to use
    template: kubernetes/app.yml@templates

    # Fill in the parameters which apply to the template you're using
    parameters: {}
```

## Templates

### `kubernetes/app.yml`
This template provides some nice functionality for automatically deploying
Kubernetes manifests for your application. You can tailor the way this template
behaves to suit a wide range of use cases, but you'll find some good examples
below.

 - [SierraSoftworks/bender](https://github.com/SierraSoftworks/bender/blob/master/azure-pipelines.yml)
 - [SierraSoftworks/rex-csharp](https://github.com/SierraSoftworks/rex-csharp/blob/master/azure-pipelines.yml)
 - [SierraSoftworks/rex-ui](https://github.com/SierraSoftworks/rex-ui/blob/master/azure-pipelines.yml)

### `kubernetes/cluster.yml`
This template is designed to manage the bootstrapping and configuration of your
Kubernetes cluster. Internally we use it to do things like configuring Traefik
and CertManager, setting up ingress routes for our applications etc.

This works well in conjunction with the `kubernetes/app.yml` template to ensure
that applications are easily updated while infrastructure changes can be made
in one central location.

[docs]: https://docs.microsoft.com/en-us/azure/devops/pipelines/process/templates?view=azure-devops#use-other-repositories