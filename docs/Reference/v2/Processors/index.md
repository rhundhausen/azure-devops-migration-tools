## Processors

>**_This documentation is for a preview version of the Azure DevOps Migration Tools._ If you are not using the preview version then please head over to the main [documentation](https://nkdagility.github.io/azure-devops-migration-tools).**

[Overview](.././index.md) > [Reference](../index.md) > *Processors*

We provide a number of Processors that can be used to migrate diferent sorts of data.

| Processor                                                         | Data Type      | Description                                                              |
| :---------------------------------------------------------------- | :------------- | :----------------------------------------------------------------------- |
| [WorkItemTrackingProcessor](./WorkItemTrackingProcessor.md)       | Work Items     | Migrated any number of work items, their revisions, links, & attachments |
| [TfsTeamSettingsProcessor](./TfsTeamSettingsProcessor.md)         | Teams          | Migrate Teams and Team Settings to a new environment                     |
| [TfsSharedQueryProcessor](./TfsSharedQueryProcessor.md)           | Shared Queries | Migrates all of the Shared Queries from one Project to Another.          |
| [AzureDevOpsPipelineProcessor](./AzureDevOpsPipelineProcessor.md) | Pipelines      | Migrates Taskgroups, Build and Release Pipelines.                        |

| Processors | Status | Target    | Usage                              |
|------------------------|---------|---------|------------------------------------------|
| [AzureDevOpsPipelineProcessor](/docs/Reference/v2/Processors/AzureDevOpsPipelineProcessor.md) | Beta | Pipelines | Azure DevOps Processor that migrates Taskgroups, Build- and Release Pipelines. |
| [ProcessDefinitionProcessor](/docs/Reference/v2/Processors/ProcessDefinitionProcessor.md) | Beta | Pipelines | Process definition processor used to keep processes between two orgs in sync |
| [TfsAreaAndIterationProcessor](/docs/Reference/v2/Processors/TfsAreaAndIterationProcessor.md) | Beta | Work Items | The `TfsAreaAndIterationProcessor` migrates all of the Area nd Iteraion paths. |
| [TfsSharedQueryProcessor](/docs/Reference/v2/Processors/TfsSharedQueryProcessor.md) | Beta | Queries | The TfsSharedQueryProcessor enabled you to migrate queries from one locatio nto another. |
| [TfsTeamSettingsProcessor](/docs/Reference/v2/Processors/TfsTeamSettingsProcessor.md) | Beta | Teams | Native TFS Processor, does not work with any other Endpoints. |
| [WorkItemTrackingProcessor](/docs/Reference/v2/Processors/WorkItemTrackingProcessor.md) | missng XML code comments | missng XML code comments | This processor is intended, with the aid of [ProcessorEnrichers](../ProcessorEnrichers/index.md), to allow the migration of Work Items between two [Endpoints](../Endpoints/index.md). |


### Processor Options

 All processors have a minimum set of options that are required to run. 

#### Minimum Options to run
The `Enabled` options is common to all processors.


```JSON
    {
      "ObjectType": "ProcessorOptions",
      "Enabled": true,
    }
```