## v1 Reference Overview

>**_This documentation is for a preview version of the Azure DevOps Migration Tools._ If you are not using the preview version then please head over to the main [documentation](https://nkdagility.github.io/azure-devops-migration-tools).**


[Overview](.././index.md) > **Reference**

The system works by setting one or more [Processors](../v1/Processors/index.md) in the json 
configuration file. You can configure one or more [FieldMaps](../v1/FieldMaps/index.md) to 
manipulate the data during a migration.

### What types of things do we have

- **[Processors](../v1/Processors/index.md)** - Processors allow you to move different types of data between `Endpoints` and does not care what `Endpoint` you have on each end.
- **[FieldMaps](../v1/FieldMaps/index.md)** - 

## Full Config File

This config is for reference only. It has things configured that you will not need, and that may conflict with each other.

```
{
  "ChangeSetMappingFile": null,
  "Source": {
    "$type": "TfsTeamProjectConfig",
    "Collection": "https://dev.azure.com/nkdagility-preview/",
    "Project": "myProjectName",
    "ReflectedWorkItemIDFieldName": "Custom.ReflectedWorkItemId",
    "AllowCrossProjectLinking": false,
    "AuthenticationMode": "Prompt",
    "PersonalAccessToken": "",
    "PersonalAccessTokenVariableName": "",
    "LanguageMaps": {
      "AreaPath": "Area",
      "IterationPath": "Iteration"
    }
  },
  "Target": {
    "$type": "TfsTeamProjectConfig",
    "Collection": "https://dev.azure.com/nkdagility-preview/",
    "Project": "myProjectName",
    "ReflectedWorkItemIDFieldName": "Custom.ReflectedWorkItemId",
    "AllowCrossProjectLinking": false,
    "AuthenticationMode": "Prompt",
    "PersonalAccessToken": "",
    "PersonalAccessTokenVariableName": "",
    "LanguageMaps": {
      "AreaPath": "Area",
      "IterationPath": "Iteration"
    }
  },
  "FieldMaps": [
    {
      "$type": "MultiValueConditionalMapConfig",
      "WorkItemTypeName": "*",
      "sourceFieldsAndValues": {
        "Field1": "Value1",
        "Field2": "Value2"
      },
      "targetFieldsAndValues": {
        "Field1": "Value1",
        "Field2": "Value2"
      }
    },
    {
      "$type": "FieldBlankMapConfig",
      "WorkItemTypeName": "*",
      "targetField": "TfsMigrationTool.ReflectedWorkItemId"
    },
    {
      "$type": "FieldValueMapConfig",
      "WorkItemTypeName": "*",
      "sourceField": "System.State",
      "targetField": "System.State",
      "defaultValue": "New",
      "valueMapping": {
        "Approved": "New",
        "New": "New",
        "Committed": "Active",
        "In Progress": "Active",
        "To Do": "New",
        "Done": "Closed",
        "Removed": "Removed"
      }
    },
    {
      "$type": "FieldtoFieldMapConfig",
      "WorkItemTypeName": "*",
      "sourceField": "Microsoft.VSTS.Common.BacklogPriority",
      "targetField": "Microsoft.VSTS.Common.StackRank",
      "defaultValue": null
    },
    {
      "$type": "FieldtoFieldMultiMapConfig",
      "WorkItemTypeName": "*",
      "SourceToTargetMappings": {
        "SourceField1": "TargetField1",
        "SourceField2": "TargetField2"
      }
    },
    {
      "$type": "FieldtoTagMapConfig",
      "WorkItemTypeName": "*",
      "sourceField": "System.State",
      "formatExpression": "ScrumState:{0}"
    },
    {
      "$type": "FieldMergeMapConfig",
      "WorkItemTypeName": "*",
      "sourceFields": [
        "System.Description",
        "Microsoft.VSTS.Common.AcceptanceCriteria"
      ],
      "targetField": "System.Description",
      "formatExpression": "{0} <br/><br/><h3>Acceptance Criteria</h3>{1}",
      "doneMatch": "##DONE##"
    },
    {
      "$type": "RegexFieldMapConfig",
      "WorkItemTypeName": "*",
      "sourceField": "COMPANY.PRODUCT.Release",
      "targetField": "COMPANY.DEVISION.MinorReleaseVersion",
      "pattern": "PRODUCT \\d{4}.(\\d{1})",
      "replacement": "$1"
    },
    {
      "$type": "FieldValuetoTagMapConfig",
      "WorkItemTypeName": "*",
      "sourceField": "Microsoft.VSTS.CMMI.Blocked",
      "pattern": "Yes",
      "formatExpression": "{0}"
    },
    {
      "$type": "TreeToTagMapConfig",
      "WorkItemTypeName": "*",
      "toSkip": 3,
      "timeTravel": 1
    }
  ],
  "GitRepoMapping": null,
  "LogLevel": "Information",
  "CommonEnrichersConfig": null,
  "Processors": [
    {
      "$type": "WorkItemMigrationConfig",
      "Enabled": false,
      "ReplayRevisions": true,
      "PrefixProjectToNodes": false,
      "UpdateCreatedDate": true,
      "UpdateCreatedBy": true,
      "WIQLQueryBit": "AND  [Microsoft.VSTS.Common.ClosedDate] = '' AND [System.WorkItemType] NOT IN ('Test Suite', 'Test Plan','Shared Steps','Shared Parameter','Feedback Request')",
      "WIQLOrderBit": "[System.ChangedDate] desc",
      "LinkMigration": true,
      "AttachmentMigration": true,
      "AttachmentWorkingPath": "c:\\temp\\WorkItemAttachmentWorkingFolder\\",
      "FixHtmlAttachmentLinks": false,
      "SkipToFinalRevisedWorkItemType": true,
      "WorkItemCreateRetryLimit": 5,
      "FilterWorkItemsThatAlreadyExistInTarget": true,
      "PauseAfterEachWorkItem": false,
      "AttachmentMaxSize": 480000000,
      "AttachRevisionHistory": false,
      "LinkMigrationSaveEachAsAdded": false,
      "GenerateMigrationComment": true,
      "WorkItemIDs": null,
      "MaxRevisions": 0,
      "NodeStructureEnricherEnabled": null,
      "UseCommonNodeStructureEnricherConfig": false,
      "StopMigrationOnMissingAreaIterationNodes": true,
      "NodeBasePaths": [
        "Product\\Area\\Path1",
        "Product\\Area\\Path2"
      ],
      "AreaMaps": {},
      "IterationMaps": {},
      "MaxGracefulFailures": 0,
      "SkipRevisionWithInvalidIterationPath": false
    },
    {
      "$type": "TestVariablesMigrationConfig",
      "Enabled": false
    },
    {
      "$type": "TestConfigurationsMigrationConfig",
      "Enabled": false
    },
    {
      "$type": "TestPlansAndSuitesMigrationConfig",
      "Enabled": false,
      "PrefixProjectToNodes": false,
      "OnlyElementsWithTag": null,
      "TestPlanQueryBit": null,
      "RemoveAllLinks": false,
      "MigrationDelay": 0,
      "UseCommonNodeStructureEnricherConfig": false,
      "NodeBasePaths": null,
      "AreaMaps": null,
      "IterationMaps": null,
      "RemoveInvalidTestSuiteLinks": false,
      "FilterCompleted": false
    },
    {
      "$type": "ImportProfilePictureConfig",
      "Enabled": false
    },
    {
      "$type": "ExportProfilePictureFromADConfig",
      "Enabled": false,
      "Domain": null,
      "Username": null,
      "Password": null,
      "PictureEmpIDFormat": null
    },
    {
      "$type": "FixGitCommitLinksConfig",
      "Enabled": false,
      "TargetRepository": "targetProjectName",
      "QueryBit": null,
      "OrderBit": null
    },
    {
      "$type": "WorkItemUpdateConfig",
      "Enabled": false,
      "WhatIf": false,
      "WIQLQueryBit": "AND [TfsMigrationTool.ReflectedWorkItemId] = '' AND  [Microsoft.VSTS.Common.ClosedDate] = '' AND [System.WorkItemType] IN ('Shared Steps', 'Shared Parameter', 'Test Case', 'Requirement', 'Task', 'User Story', 'Bug')",
      "WIQLOrderBit": null,
      "WorkItemIDs": null,
      "FilterWorkItemsThatAlreadyExistInTarget": false,
      "PauseAfterEachWorkItem": false,
      "WorkItemCreateRetryLimit": 0
    },
    {
      "$type": "WorkItemPostProcessingConfig",
      "Enabled": false,
      "WorkItemIDs": [
        1,
        2,
        3
      ],
      "WIQLQueryBit": "AND [TfsMigrationTool.ReflectedWorkItemId] = '' ",
      "WIQLOrderBit": null,
      "FilterWorkItemsThatAlreadyExistInTarget": false,
      "PauseAfterEachWorkItem": false,
      "WorkItemCreateRetryLimit": 0
    },
    {
      "$type": "WorkItemDeleteConfig",
      "Enabled": false,
      "WIQLQueryBit": "AND  [Microsoft.VSTS.Common.ClosedDate] = '' AND [System.WorkItemType] NOT IN ('Test Suite', 'Test Plan')",
      "WIQLOrderBit": "[System.ChangedDate] desc",
      "WorkItemIDs": null,
      "FilterWorkItemsThatAlreadyExistInTarget": false,
      "PauseAfterEachWorkItem": false,
      "WorkItemCreateRetryLimit": 0
    },
    {
      "$type": "WorkItemQueryMigrationConfig",
      "Enabled": false,
      "PrefixProjectToNodes": false,
      "SharedFolderName": "Shared Queries",
      "SourceToTargetFieldMappings": {
        "SourceFieldRef": "TargetFieldRef"
      }
    },
    {
      "$type": "TeamMigrationConfig",
      "Enabled": false,
      "PrefixProjectToNodes": false,
      "EnableTeamSettingsMigration": true,
      "FixTeamSettingsForExistingTeams": false
    }
  ],
  "Version": "0.0",
  "workaroundForQuerySOAPBugEnabled": false,
  "WorkItemTypeDefinition": {
    "sourceWorkItemTypeName": "targetWorkItemTypeName"
  },
  "Endpoints": {
    "InMemoryWorkItemEndpoints": [
      {
        "Name": "Source",
        "EndpointEnrichers": null
      },
      {
        "Name": "Target",
        "EndpointEnrichers": null
      }
    ]
  }
}
```