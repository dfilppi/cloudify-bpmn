# cloudify-bpmn
Components for using Cloudify in Camunda workflows

## projects
This project contains a java Camunda delegates project and a java client for Cloudify project.

### Camunda delegates project
As of this writing, there are three delegates one for installation of Cloudify blueprints, one for uninstallation, and one for running arbitrary workflows on a pre-existing Cloudify deployment.  Each delegate accepts arguments as described below.  In the project, these are hard coded in the sample BPMN flows for a simple test.  It is intended that the values of inputs are replaced with expressions from the hosting workflow.  The example BPMN flows are in the `resources/bpmn` directory, one for each delegate.  Note that there is a `Test` class that starts the Camunda engine for demonstration.

#### Install Delegate
The `CloudifyInstallBlueprintDelegate` class performs a complete blueprint upload, deployment creation, and install workflow execution sequence.  The blueprint must be a single YAML file.  Also, the deployment name used in the installation will be the same as the blueprint name/id.

Inputs:
* `InputCfy_credentials` - (Map) that provides password based authentication to the Cloudify server.
* `InputCfy_blueprint` - (String) the actual blueprint to upload.
* `InputCfy_blueprint_yaml` - (String) the name of the blueprint in the generated package.
* `InputCfy_blueprint_name` - (String) the name of the blueprint and deployment on the Cloudify server.

#### Uninstall Delegate
The `CloudifyUninstallBlueprintDelegate` class runs the uninstall workflow on a target deployment.  Optionally it will also delete the related deployment and blueprint.  This delegate assumes that the deployment name and blueprint name are the same.

Inputs:
* `InputCfy_credentials` - (Map) that provides password based authentication to the Cloudify server.
* `InputCfy_deployment` - (String) the deployment id.
* `InputCfy_delete_deployment`- (String) a boolean (true or false) indicating whether to delete the deployment.
* `InputCfy_delete_blueprint`- (String) a boolean (true or false) indicating whether to delete the blueprint.

#### Run Workflow Delegate
The `CloudifyRunWorkflowDelegate` class runs an arbitrary workflow on a pre-existing deployment id.

Inputs:
* `InputCfy_credentials` - (Map) that provides password based authentication to the Cloudify server.
* `InputCfy_deployment` - (String) the target deployment id
* `InputCfy_workflow` - (String) the workflow to run
