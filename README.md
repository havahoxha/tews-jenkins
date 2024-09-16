# PoC Jenkins CICD pipeline with patch version upgrading

## Workflow

The high-level idea of this PoC is to set up a simple instance of Jenkins which has a pipeline configuration for building a flutter project and
incrementing the patch version of the project.

This version would usually have to be inferred from an artifactory where the build is pushed but since this is simply a PoC, we will infer it from the code
itself and just increment it, save it and build the project.

Sharing the jobs directory with the host machine in order to keep jobs build artifacts in version control. Otherwise, script declarations should be kept within their
respective repositories. In our case, example-flutter-project has its own Jenkinsfile.

## How to run

1. Start server with `docker compose up`
1. The logs will display what's the initial password for the admin account
1. Create a new account
1. Install suggested plugins
1. Run job
