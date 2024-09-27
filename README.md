# PoC Jenkins CICD pipeline with patch version upgrading

## Workflow

The high-level idea of this PoC is to set up a simple instance of Jenkins which has a pipeline configuration for building a flutter project and
incrementing the patch version of the project.

This version would usually have to be inferred from an artifactory where the build is pushed but since this is simply a PoC, we will infer it from the code
itself and just increment it, save it and build the project.

Sharing the jobs directory with the host machine in order to keep job configs in version control. Otherwise, script declarations should be kept within their
respective repositories. In our case, example-flutter-project has its own Jenkinsfile.

## How to run

1. Start server with `docker compose up`
1. The logs will display what's the initial password for the admin account
1. Create a new account
1. Install suggested plugins
1. Run job

In order to validate successful pipeline run, you should go to workspace and run the binary found at this path - `./jobs/Increment patch and build app (PoC)/workspace/build/linux/x64/release/bundle`. The binary should display as text the incremented version of the build. This update won't be reflected in the code managed by the VCS.

## Bugs

> fatal: detected dubious ownership in repository at '/var/jenkins_home/jobs/Increment patch and build app (PoC)/workspace/flutter'
To add an exception for this directory, call:

The workflow creates a hierarchy of git repositories with different permission levels which in turn in creates conflicts in the SDK resolutions (Flutter can't resolve its own version). 


```bash
git config --global --add safe.directory '*'
```

This will probably not be an issue if we set a docker agent running a flutter image but for the moment being this could turn out to be a severe security issue.

