# Azure_Docker_AcrPush
Use this template to push Docker images, log in or log out, start or stop containers, or run a Docker command. It deals with ACR as registry

## Parameters:

The pipeline requires the following parameters to be defined:


| Name  | Displayname | type | Default | Values | Opional/Required | Comments |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| serviceConnection | Azure Service Connection for acr registry or azure resource manager in your Azure pipeline | string | | | Required | This helps the module to authenticate with registry or azure cli |
| imageRepository | acr docker repostiroy | string | | | Required | docker registry imagename to be created |
| tags | Version or tag for image | string |  | | Required | when multiple tags pass in following way: **"1.2.3,latest"** |
| dockerPushArgs | arguments for push step | string | | | Optional | except *--all-tags* either pass --disable-content-trust or --quiet |
| addPipelineData  | pipeline data: source branch, build ID| boolean | true | true / false | Optional | helps to inspect error of image built |
| addBaseImageData | base image data: image name, digest | boolean | true | true / false | Optional |helps in traceability |
--------------------------------------------------------------------------------------------------------------------------------------------------

These parameters provide multiple use case options for the template, enable/disable flags for the utilization of different templates as per the requirements.


## Use Cases

You can directly call a particular template as per the requirement. for example: 

  ```yaml
  # azure-pipeline.yml
  resources:
  repositories:
    - repository: Template
      type: github
      name: your_username/Azure_Docker_AcrPush
      ref: <respective branch name>
      endpoint: 'githubServiceConnectioNname'

  steps:
  # passing the parameters
  - template: Azure_Docker_AcrPush.yaml
    parameters:
          serviceConnection: '${{parameters.serviceConnection}}'
          imageRepository: '${{parameters.imageRepository}}'
          tags: ${{parameters.tags}}
          dockerPushArgs: ${{parameters.dockerPushArgs}}
        
  
Make sure to adjust the repository name, branch name, and parameter values according to your project's requirements.

  ```
