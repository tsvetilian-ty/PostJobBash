
<p align="center">
  <img width="128" height="128" src="https://github.com/tsvetilian-ty/PostJobBash/raw/main/images/extension-icon.png">
</p>

## Description
`PostJobBash` is `Bash@3` based task that allows you to executes bash scripts (across platforms) in the `post-job` phase of the job!

> [!NOTE]  
> The `PostJobBash` is based on Microsoft's `Bash@3` (https://github.com/microsoft/azure-pipelines-tasks/tree/master/Tasks/BashV3) version `3.237.0` therefore supports the same APIs (https://learn.microsoft.com/en-us/azure/devops/pipelines/tasks/reference/bash-v3?view=azure-pipelines)

## Examples
> Exiting job
```yml
- task: PostJobBash@1
  displayName: Exit log
  inputs:
    targetType: 'inline'
    script: |
      echo "Exiting the job!"
```
> Clean workspace after the pipeline executes
```yml
- task: PostJobBash@1
  displayName: Clean workspace
  env:
    PIPELINE_WORKSPACE: $(Pipeline.Workspace)
    AGENT_WORK_FOLDER: $(Agent.WorkFolder)
  inputs:
    targetType: 'inline'
    script: |
      pipelineWorkspace=$PIPELINE_WORKSPACE
      agentWorkFolder=$AGENT_WORK_FOLDER

      if [ -d "$pipelineWorkspace" ]; then
          echo "Pipeline workspace folder still exists ($pipelineWorkspace), deleting..."
          cd $agentWorkFolder
          rm -r $pipelineWorkspace
      else
          echo "Pipeline workspace folder does not exist."
      fi
```