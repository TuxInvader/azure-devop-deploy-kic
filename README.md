# azure-devops-deploy-kic
Deploy NGINX Plus KIC from Azure DevOps

## Azure Service Connections
This pipeline requires connections to an Docker Registry for hosting the KIC images,
and also a connection to the Azure Resource Manager. You will need to create both of these 
in your project settings under `pipeline` -> `service connections`

For each connection click the `New service connection` button in the `Service connections` page
and then create an `Azure Resource Manager` connection and a `Docker Registry`. Make a note of
the connection names for use in pipeline variables.

## Creating the pipeline
You will first need to fork this repository on Github, then in you Azure DevOps Project
goto pipelines and click the add `New Pipeline` button. 

Select GitHub as the location of the code. You will need to link your ADO account with GitHub
if you haven't already and then select your fork of this project.

Azure will detect the pipeline and display it for you. The next step is to setup the required
variables.

## Adding Variables
You will need to add some variables to the pipeline before you can use it. In the review/edit
page for the pipeline you will have a `Variables` button. This button opens a new pane in which
you can create or edit the variables. The required variable are:

### Service Connections
1. containerServiceConn - This is the name of the `Docker Registry` service connection
2. azureSubscription - This is the name of the service connection to your `Azure Resource Manager`

### AKS/Container Settings
1. azureRegistry - This is the FQDN of the registry that is accessed through `containerServiceConn`
2. azureAKS - The name of the the AKS cluster
3. azureResGroup - The Azure resource group where the AKS cluster lives

### Kubernetes/Helm options
1. aksNamespace - The kubernetes namespace to deploy the KIC into
2. helmRelease - The release name used in the helm deployment
3. replicaCount - The number of KICs to deploy

### NGINX Plus License
1. nginxRepoKey - Your private key for the NGINX Plus repository
2. nginxRepoCert - Your certificate for the NGINX Plus repository

### Pipeline control
1. pipelineBuild - set to `true` if you want this pipeline run to build the container image
2. pipelineDeploy - set to `true` if you want this pipeline run to deploy the KIC with Helm
3. pipelineCleanup - set to `true` if you want this pipeline run to remove a deployed KIC

## Running the pipeline
The pipeline tasks are controlled by the `pipeline[Build|Deploy|Cleanup]` variables. You only need Build set
to `true` when you need to build and publish a new container image. The deploy action is used to deploy the
KIC into your AKS cluster and so will usually need to be set to `true`, and the cleanup action is only needed
when you want to remove the KIC.
