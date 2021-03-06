# ApplicationInsights

> see https://aka.ms/autorest

This is the AutoRest configuration file for ApplicationInsights.



---
## Getting Started
To build the SDK for ApplicationInsights, simply [Install AutoRest](https://aka.ms/autorest/install) and in this folder, run:

> `autorest`

To see additional help and options, run:

> `autorest --help`
---

## Configuration



### Basic Information
These are the global settings for the ApplicationInsights API.

``` yaml
title: ApplicationInsightsManagementClient
description: Composite Swagger for Application Insights Management Client
openapi-type: arm
tag: package-2015-05
```

## Suppression
``` yaml
directive:
  - suppress: LongRunningOperationsWithLongRunningExtension
    where:
      - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/purge"].post
    reason: Original creation of the service did not comply with current ARM schema standards. The team is aware of it and any future updates should rectify the issue.
    
  - suppress: TrackedResourceListByImmediateParent
    where:
      - $.definitions
    reason:
      - we do have list operations available for our operations on individual instances of objects returned. False positives.

  - suppress: PutRequestResponseScheme
    reason: This api was existing there from 2015, it will break existing client if we change the request/response format
    #where:
    #  - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration/{exportId}"].put

  - suppress: ListInOperationName
    reason: The return value is an object, not an array. Looks like a false positive of the validation tool.
    #where:
    #  - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/currentbillingfeatures"].get.operationId

  - suppress: PutInOperationName
    reason: We are not doing create on this api, it is only doing update in this PUT api call.
    #where:
    #  - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration/{exportId}"].put.operationId
    #  - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/currentbillingfeatures"].put.operationId

  - suppress: XmsResourceInPutResponse
    reason: This api was existing there from 2015, it will break existing client if we change the request/response format
    #where:
    #  - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration/{exportId}"].put
    #  - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/currentbillingfeatures"].put

  - suppress: RequiredPropertiesMissingInResourceModel
    reason: This api was existing there from 2015, it will break existing client if we change the response format
    #where:
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration
    #  - $.definitions.ApplicationInsightsComponentBillingFeatures

  - suppress: BodyTopLevelProperties
    reason: This api was existing there from 2015, it will break existing client if we change the response format
    #where:
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties
    #  - $.definitions.ApplicationInsightsComponentBillingFeatures.properties

  - suppress: EnumInsteadOfBoolean
    reason: This api was existing there from 2015, it will break existing client if we change the type
    #where:
    #  - $.definitions.WebTestProperties.properties.Enabled
    #  - $.definitions.WebTestProperties.properties.RetryEnabled
    #  - $.definitions.ApplicationInsightsComponentDataVolumeCap.properties.StopSendNotificationWhenHitThreshold
    #  - $.definitions.ApplicationInsightsComponentDataVolumeCap.properties.StopSendNotificationWhenHitCap
    #  - $.definitions.ApplicationInsightsComponentQuotaStatus.properties.ShouldBeThrottled

  - suppress: DescriptionAndTitleMissing
    reason: Error addresses missing description/title in inner reference. Referenced model contains title and description. Redundant.
    from: componentAnnotations_API.json
    where:
      - $.definitions.AnnotationError.properties.innererror

  - suppress: DescriptionAndTitleMissing
    reason: Error addresses missing description/title in inner reference. Referenced model contains title and description. Redundant.
    from: componentWorkItemConfigs_API.json
    where:
      - $.definitions.WorkItemConfigurationError.properties.innererror

  - suppress: LROStatusCodesReturnTypeSchema
    reason: The response for 200 does define a schema in place. The test likely expects a 'ref' member. False failure.
    from: componentAnnotations_API.json
    where:
      - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/Annotations"].put.responses["200"]

  - suppress: DefinitionsPropertiesNamesCamelCase
    reason: This api was existing there from 2015, it will break existing client if we change the name
    # where:
    #  - $.definitions.ApplicationInsightsComponentProperties.properties.ApplicationId
    #  - $.definitions.ApplicationInsightsComponentProperties.properties.AppId
    #  - $.definitions.ApplicationInsightsComponentProperties.properties.Application_Type
    #  - $.definitions.ApplicationInsightsComponentProperties.properties.Flow_Type
    #  - $.definitions.ApplicationInsightsComponentProperties.properties.Request_Source
    #  - $.definitions.ApplicationInsightsComponentProperties.properties.InstrumentationKey
    #  - $.definitions.ApplicationInsightsComponentProperties.properties.CreationDate
    #  - $.definitions.ApplicationInsightsComponentProperties.properties.TenantId
    #  - $.definitions.ApplicationInsightsComponentProperties.properties.HockeyAppId
    #  - $.definitions.ApplicationInsightsComponentProperties.properties.HockeyAppToken
    #  - $.definitions.ApplicationInsightsComponentProperties.properties.SamplingPercentage
    #  - $.definitions.WebTestProperties.properties.SyntheticMonitorId
    #  - $.definitions.WebTestProperties.properties.Name
    #  - $.definitions.WebTestProperties.properties.Description
    #  - $.definitions.WebTestProperties.properties.Enabled
    #  - $.definitions.WebTestProperties.properties.Frequency
    #  - $.definitions.WebTestProperties.properties.Timeout
    #  - $.definitions.WebTestProperties.properties.Kind
    #  - $.definitions.WebTestProperties.properties.RetryEnabled
    #  - $.definitions.WebTestProperties.properties.Locations
    #  - $.definitions.WebTestProperties.properties.Configuration
    #  - $.definitions.WebTestGeolocation.properties.Id
    #  - $.definitions.ApplicationInsightsComponentExportRequest.properties.RecordTypes
    #  - $.definitions.ApplicationInsightsComponentExportRequest.properties.DestinationType
    #  - $.definitions.ApplicationInsightsComponentExportRequest.properties.DestinationAddress
    #  - $.definitions.ApplicationInsightsComponentExportRequest.properties.IsEnabled
    #  - $.definitions.ApplicationInsightsComponentExportRequest.properties.NotificationQueueEnabled
    #  - $.definitions.ApplicationInsightsComponentExportRequest.properties.NotificationQueueUri
    #  - $.definitions.ApplicationInsightsComponentExportRequest.properties.DestinationStorageSubscriptionId
    #  - $.definitions.ApplicationInsightsComponentExportRequest.properties.DestinationStorageLocationId
    #  - $.definitions.ApplicationInsightsComponentExportRequest.properties.DestinationAccountId
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties.ExportId
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties.InstrumentationKey
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties.RecordTypes
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties.ApplicationName
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties.SubscriptionId
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties.ResourceGroup
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties.DestinationStorageSubscriptionId
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties.DestinationStorageLocationId
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties.DestinationAccountId
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties.DestinationType
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties.IsUserEnabled
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties.LastUserUpdate
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties.NotificationQueueEnabled
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties.ExportStatus
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties.LastSuccessTime
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties.LastGapTime
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties.PermanentErrorReason
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties.StorageName
    #  - $.definitions.ApplicationInsightsComponentExportConfiguration.properties.ContainerName
    #  - $.definitions.ApplicationInsightsComponentBillingFeatures.properties.DataVolumeCap
    #  - $.definitions.ApplicationInsightsComponentBillingFeatures.properties.CurrentBillingFeatures
    #  - $.definitions.ApplicationInsightsComponentDataVolumeCap.properties.Cap
    #  - $.definitions.ApplicationInsightsComponentDataVolumeCap.properties.ResetTime
    #  - $.definitions.ApplicationInsightsComponentDataVolumeCap.properties.WarningThreshold
    #  - $.definitions.ApplicationInsightsComponentDataVolumeCap.properties.StopSendNotificationWhenHitThreshold
    #  - $.definitions.ApplicationInsightsComponentDataVolumeCap.properties.StopSendNotificationWhenHitCap
    #  - $.definitions.ApplicationInsightsComponentDataVolumeCap.properties.MaxHistoryCap
    #  - $.definitions.ApplicationInsightsComponentQuotaStatus.properties.AppId
    #  - $.definitions.ApplicationInsightsComponentQuotaStatus.properties.ShouldBeThrottled
    #  - $.definitions.ApplicationInsightsComponentQuotaStatus.properties.ExpirationTime
    #  - $.definitions.ApplicationInsightsComponentProactiveDetectionConfiguration.properties.Name
    #  - $.definitions.ApplicationInsightsComponentProactiveDetectionConfiguration.properties.Enabled
    #  - $.definitions.ApplicationInsightsComponentProactiveDetectionConfiguration.properties.SendEmailsToSubscriptionOwners
    #  - $.definitions.ApplicationInsightsComponentProactiveDetectionConfiguration.properties.CustomEmails
    #  - $.definitions.ApplicationInsightsComponentProactiveDetectionConfiguration.properties.LastUpdatedTime
    #  - $.definitions.ApplicationInsightsComponentProactiveDetectionConfiguration.properties.RuleDefinitions
    #  - $.definitions.ApplicationInsightsComponentProactiveDetectionConfiguration.properties.Name
    #  - $.definitions.ApplicationInsightsComponentProactiveDetectionConfiguration.properties.Name
    #  - $.definitions.ApplicationInsightsComponentWebTestLocation.properties.Tag
    #  - $.definitions.ApplicationInsightsComponentWebTestLocation.properties.DisplayName
    #  - $.definitions.ApplicationInsightsComponentFavorite.properties.UserId
    #  - $.definitions.ApplicationInsightsComponentFavorite.properties.IsGeneratedFromTemplate
    #  - $.definitions.ApplicationInsightsComponentFavorite.properties.Category
    #  - $.definitions.ApplicationInsightsComponentFavorite.properties.Tags
    #  - $.definitions.ApplicationInsightsComponentFavorite.properties.TimeModified
    #  - $.definitions.ApplicationInsightsComponentFavorite.properties.SourceType
    #  - $.definitions.ApplicationInsightsComponentFavorite.properties.FavoriteType
    #  - $.definitions.ApplicationInsightsComponentFavorite.properties.FavoriteId
    #  - $.definitions.ApplicationInsightsComponentFavorite.properties.Version
    #  - $.definitions.ApplicationInsightsComponentFavorite.properties.Config
    #  - $.definitions.ApplicationInsightsComponentFavorite.properties.Name
    #  - $.definitions.ApplicationInsightsComponentFeatureCapability.properties.MeterRateFrequency
    #  - $.definitions.ApplicationInsightsComponentFeatureCapability.properties.MeterId
    #  - $.definitions.ApplicationInsightsComponentFeatureCapability.properties.Unit
    #  - $.definitions.ApplicationInsightsComponentFeatureCapability.properties.Value
    #  - $.definitions.ApplicationInsightsComponentFeatureCapability.properties.Description
    #  - $.definitions.ApplicationInsightsComponentFeatureCapability.properties.Name
    #  - $.definitions.ApplicationInsightsComponentFeature.properties.SupportedAddonFeatures
    #  - $.definitions.ApplicationInsightsComponentFeature.properties.IsMainFeature
    #  - $.definitions.ApplicationInsightsComponentFeature.properties.Title
    #  - $.definitions.ApplicationInsightsComponentFeature.properties.Capabilities
    #  - $.definitions.ApplicationInsightsComponentFeature.properties.IsHidden
    #  - $.definitions.ApplicationInsightsComponentFeature.properties.ResouceId
    #  - $.definitions.ApplicationInsightsComponentFeature.properties.MeterRateFrequency
    #  - $.definitions.ApplicationInsightsComponentFeature.properties.MeterId
    #  - $.definitions.ApplicationInsightsComponentFeature.properties.FeatureName
    #  - $.definitions.ApplicationInsightsComponentAvailableFeatures.properties.Result
    #  - $.definitions.ApplicationInsightsComponentFeatureCapabilities.properties.ThrottleRate
    #  - $.definitions.ApplicationInsightsComponentFeatureCapabilities.properties.DailyCapResetTime
    #  - $.definitions.ApplicationInsightsComponentFeatureCapabilities.properties.DailyCap
    #  - $.definitions.ApplicationInsightsComponentFeatureCapabilities.properties.TrackingType
    #  - $.definitions.ApplicationInsightsComponentFeatureCapabilities.properties.ApiAccessLevel
    #  - $.definitions.ApplicationInsightsComponentFeatureCapabilities.properties.SupportExportData
    #  - $.definitions.ApplicationInsightsComponentFeatureCapabilities.properties.BurstThrottlePolicy
    #  - $.definitions.ApplicationInsightsComponentFeatureCapabilities.properties.MetadataClass
    #  - $.definitions.ApplicationInsightsComponentFeatureCapabilities.properties.LiveStreamMetrics
    #  - $.definitions.ApplicationInsightsComponentFeatureCapabilities.properties.ApplicationMap
    #  - $.definitions.ApplicationInsightsComponentFeatureCapabilities.properties.WorkItemIntegration
    #  - $.definitions.ApplicationInsightsComponentFeatureCapabilities.properties.PowerBIIntegration
    #  - $.definitions.ApplicationInsightsComponentFeatureCapabilities.properties.OpenSchema
    #  - $.definitions.ApplicationInsightsComponentFeatureCapabilities.properties.ProactiveDetection
    #  - $.definitions.ApplicationInsightsComponentFeatureCapabilities.properties.AnalyticsIntegration
    #  - $.definitions.ApplicationInsightsComponentFeatureCapabilities.properties.MultipleStepWebTest
    #  - $.definitions.ApplicationInsightsComponentAnalyticsItem.properties.Id
    #  - $.definitions.ApplicationInsightsComponentAnalyticsItem.properties.Name
    #  - $.definitions.ApplicationInsightsComponentAnalyticsItem.properties.Content
    #  - $.definitions.ApplicationInsightsComponentAnalyticsItem.properties.Version
    #  - $.definitions.ApplicationInsightsComponentAnalyticsItem.properties.Scope
    #  - $.definitions.ApplicationInsightsComponentAnalyticsItem.properties.Type
    #  - $.definitions.ApplicationInsightsComponentAnalyticsItem.properties.TimeCreated
    #  - $.definitions.ApplicationInsightsComponentAnalyticsItem.properties.TimeModified
    #  - $.definitions.ApplicationInsightsComponentAnalyticsItem.properties.Properties

  - suppress: R2066
    reason: There are a bug in this rule. "ExportConfigurations_Create" is a valid operation id.
```

### Tag: package-2015-05

These settings apply only when `--tag=package-2015-05` is specified on the command line.

``` yaml $(tag) == 'package-2015-05'
input-file:
- Microsoft.Insights/stable/2015-05-01/aiOperations_API.json
- Microsoft.Insights/stable/2015-05-01/componentAnnotations_API.json
- Microsoft.Insights/stable/2015-05-01/componentApiKeys_API.json
- Microsoft.Insights/stable/2015-05-01/componentContinuousExport_API.json
- Microsoft.Insights/stable/2015-05-01/componentFeaturesAndPricing_API.json
- Microsoft.Insights/stable/2015-05-01/componentProactiveDetection_API.json
- Microsoft.Insights/stable/2015-05-01/components_API.json
- Microsoft.Insights/stable/2015-05-01/componentWorkItemConfigs_API.json
- Microsoft.Insights/stable/2015-05-01/favorites_API.json
- Microsoft.Insights/stable/2015-05-01/webTestLocations_API.json
- Microsoft.Insights/stable/2015-05-01/webTests_API.json
- microsoft.insights/stable/2015-05-01/analyticsItems_API.json
- Microsoft.Insights/stable/2015-05-01/workbooks_API.json
```

### Tag: package-2017-10

These settings apply only when `--tag=package-2017-10` is specified on the command line.

``` yaml $(tag) == 'package-2017-10'
input-file:
- Microsoft.Insights/preview/2017-10-01/eaSubscriptionMigration_API.json
- Microsoft.Insights/preview/2017-10-01/componentFeaturesAndPricing_API.json
```

### Tag: package-2018-06-17-preview

These settings apply only when `--tag=package-2018-06-17-preview` is specified on the command line.

``` yaml $(tag) == 'package-2018-06-17-preview'
input-file:
- Microsoft.Insights/preview/2018-06-17-preview/workbooks_API.json
```
---
# Code Generation


## Swagger to SDK

This section describes what SDK should be generated by the automatic system.
This is not used by Autorest itself.

``` yaml $(swagger-to-sdk)
swagger-to-sdk:
  - repo: azure-sdk-for-python
  - repo: azure-sdk-for-java
  - repo: azure-sdk-for-go
  - repo: azure-sdk-for-node
```


## Python

These settings apply only when `--python` is specified on the command line.
Please also specify `--python-sdks-folder=<path to the root directory of your azure-sdk-for-python clone>`.
Use `--python-mode=update` if you already have a setup.py and just want to update the code itself.

``` yaml $(python)
python-mode: create
python:
  azure-arm: true
  license-header: MICROSOFT_MIT_NO_VERSION
  payload-flattening-threshold: 2
  namespace: azure.mgmt.applicationinsights
  package-name: azure-mgmt-applicationinsights
  package-version: 0.1.0
  clear-output-folder: true
```
``` yaml $(python) && $(python-mode) == 'update'
python:
  no-namespace-folders: true
  output-folder: $(python-sdks-folder)/azure-mgmt-applicationinsights/azure/mgmt/applicationinsights
```
``` yaml $(python) && $(python-mode) == 'create'
python:
  basic-setup-py: true
  output-folder: $(python-sdks-folder)/azure-mgmt-applicationinsights
```


## C#

These settings apply only when `--csharp` is specified on the command line.
Please also specify `--csharp-sdks-folder=<path to "SDKs" directory of your azure-sdk-for-net clone>`.

``` yaml $(csharp)
csharp:
  azure-arm: true
  payload-flattening-threshold: 1
  license-header: MICROSOFT_MIT_NO_VERSION
  namespace: Microsoft.Azure.Management.ApplicationInsights.Management
  output-folder: $(csharp-sdks-folder)/ApplicationInsights/Management.ApplicationInsights/Generated
  clear-output-folder: true
```
## Go

These settings apply only when `--go` is specified on the command line.

``` yaml $(go)
go:
  license-header: MICROSOFT_APACHE_NO_VERSION
  namespace: insights
  clear-output-folder: true
```

### Go mult-api

``` yaml $(go) && $(multiapi)
batch:
  - tag: package-2015-05
```

### Tag: package-2015-05 and go

These settings apply only when `--tag=package-2015-05 --go` is specified on he command line.
Please also specify `--go-sdk-folder=<path to the root directory of your azure-sdk-for-go clone>`.

``` yaml $(tag) == 'package-2015-05' && $(go)
output-folder: $(go-sdk-folder)/services/appinsights/mgmt/2015-05-01/insights
```

### Tag: schema-2015-05-preview

These settings apply only when `--tag=schema-2015-05-01` is specified on the
command line.

This section contains the input swagger files that are used when generating
resource manager schemas for version 2015-05-01. Note that many of our
pre-existing APIs are note currently compatible with ARM schemas, upon any
updates applied to our services we will bring them up to compliance.

``` yaml $(tag) == 'schema-2015-05-01'
input-file:
 - ./Microsoft.Insights/stable/2015-05-01/aiOperations_API.json
 - ./Microsoft.Insights/stable/2015-05-01/components_API.json
 - ./Microsoft.Insights/stable/2015-05-01/webTests_API.json
 - ./Microsoft.Insights/stable/2015-05-01/workbooks_API.json

override-info:
  title: ApplicationInsightsManagementClient
```

## Java

These settings apply only when `--java` is specified on the command line.
Please also specify `--azure-libraries-for-java-folder=<path to the root directory of your azure-libraries-for-java clone>`.

``` yaml $(java)
  azure-arm: true
  fluent: true
  namespace: com.microsoft.azure.management.applicationinsights
  license-header: MICROSOFT_MIT_NO_CODEGEN
  payload-flattening-threshold: 1
  output-folder: $(azure-libraries-for-java-folder)/azure-mgmt-applicationinsights
```

### Java multi-api

``` yaml $(java) && $(multiapi)
batch:
  - tag: package-2015-05
```

### Tag: package-2015-05 and java

These settings apply only when `--tag=package-2015-05 --java` is specified on the command line.
Please also specify `--azure-libraries-for-java=<path to the root directory of your azure-sdk-for-java clone>`.

``` yaml $(tag) == 'package-2015-05' && $(java) && $(multiapi)
java:
  namespace: com.microsoft.azure.management.applicationinsights.v2015_05_01
  output-folder: $(azure-libraries-for-java-folder)/applicationinsights/resource-manager/v2015_05_01
regenerate-manager: true
generate-interface: true
```

### Tag: schema-2018-06-17-preview

These settings apply only when `--tag=schema-2018-06-17-preview` is specified on the command line.

``` yaml $(tag) == 'schema-2018-06-17-preview'
input-file:
- Microsoft.Insights/preview/2018-06-17-preview/workbooks_API.json
```