# azure-devop-deploy-kic
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

1. containerServiceConn - This is the name of the `Docker Registry` service connection
2. 
2. azureRegistry - This is the FQDN of the registry that is access through `containerServiceConn`
3. azureSubscription - This is the service connection to your Azure Subscription
