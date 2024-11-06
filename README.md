<div align="center">

[![](images/introduction.png)](https://github.com/jfrog/jfrog-azure-devops-extension)

# JFrog Azure DevOps Extension

|                                                                                                           Azure DevOps Extension                                                                                                           | Installs                                                                                                                                                                                                                                                                                                    |                                                                                                                                   Tests (Master)                                                                                                                                    |                                                                                                                                           Tests (Dev)                                                                                                                                           |
|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| [![JFrog Extension Marketplace](https://img.shields.io/static/v1?label=%20&color=blue&style=for-the-badge&logo=azuredevops&message=JFrog%20(New))](https://marketplace.visualstudio.com/items?itemName=JFrog.jfrog-azure-devops-extension) | [![JFrog Extension Marketplace Installs](https://img.shields.io/visual-studio-marketplace/azure-devops/installs/total/JFrog.jfrog-azure-devops-extension?label=Total&color=blue&style=for-the-badge)](https://marketplace.visualstudio.com/items?itemName=JFrog.jfrog-azure-devops-extension)               | [![Tests](https://github.com/jfrog/jfrog-azure-devops-extension/actions/workflows/tests.yml/badge.svg)](https://github.com/jfrog/jfrog-azure-devops-extension/actions/workflows/tests.yml)  |     [![Tests](https://github.com/jfrog/jfrog-azure-devops-extension/actions/workflows/tests.yml/badge.svg?branch=dev)](https://github.com/jfrog/jfrog-azure-devops-extension/actions/workflows/tests.yml)      |
|  [![JFrog Extension Marketplace](https://img.shields.io/static/v1?label=%20&color=blue&style=for-the-badge&logo=azuredevops&message=Artifactory)](https://marketplace.visualstudio.com/items?itemName=JFrog.jfrog-azure-devops-extension)  | [![Artifactory Extension Marketplace Installs](https://img.shields.io/visual-studio-marketplace/azure-devops/installs/total/JFrog.jfrog-artifactory-vsts-extension?label=Total&color=blue&style=for-the-badge)](https://marketplace.visualstudio.com/items?itemName=JFrog.jfrog-artifactory-vsts-extension) | [![Build status](https://ci.appveyor.com/api/projects/status/ki6edykufqy9h5bl/branch/v1?svg=true&passingText=v1%20-%20passing&failingText=dev%20-%20failing&pendingText=dev%20-%20pending)](https://ci.appveyor.com/project/jfrog-ecosystem/jfrog-azure-devops-extension/branch/v1) | [![Build status](https://ci.appveyor.com/api/projects/status/ki6edykufqy9h5bl/branch/dev-v1?svg=true&passingText=dev-v1%20-%20passing&failingText=dev%20-%20failing&pendingText=dev%20-%20pending)](https://ci.appveyor.com/project/jfrog-ecosystem/jfrog-azure-devops-extension/branch/dev-v1) |

</div>

# Overview

[JFrog](https://jfrog.com/) provides tight integration with [Azure DevOps](https://azure.microsoft.com/en-us/services/devops/) through the _[JFrog Extension](https://marketplace.visualstudio.com/items?itemName=JFrog.jfrog-azure-devops-extension)_
Beyond managing efficient deployment of your artifacts to [JFrog Artifactory](https://jfrog.com/artifactory), the extension lets you capture information about
artifacts deployed, dependencies resolved, environment data associated with the build runs and more,
that effectively facilitates fully traceable builds.
JFrog brings continuous integration to [Azure DevOps](https://azure.microsoft.com/en-us/services/devops/) through the _JFrog_ extension.

The _[JFrog Extension](https://marketplace.visualstudio.com/items?itemName=JFrog.jfrog-azure-devops-extension)_ for Azure DevOps supports:

- Running your builds while using [JFrog Artifactory](https://jfrog.com/artifactory) as the binary repository manager.
- Gaining full traceability of your builds by capturing your build-info from your builds and publishing it to [JFrog Artifactory](https://jfrog.com/artifactory).
- Managing your binaries lifecycle with [JFrog Artifactory](https://jfrog.com/artifactory).
- Auditing your projects and scanning your builds with [JFrog Xray](https://jfrog.com/xray).
- Distributing your artifacts with [JFrog Distribution](https://jfrog.com/distribution/).

## Table of contents

- [JFrog Azure DevOps Extension](#jfrog-azure-devops-extension)
- [Overview](#overview)
  - [Table of contents](#table-of-contents)
  - [Download and Installation](#download-and-installation)
    - [Installing the Extension](#installing-the-extension)
    - [Installing the Build Agent](#installing-the-build-agent)
      - [Automatic Installation](#automatic-installation)
      - [Custom tools Installation](#custom-tools-installation)
      - [Manual Installation](#manual-installation)
        - [Installing JFrog CLI](#installing-jfrog-cli)
        - [Installing the Maven Extractor](#installing-the-maven-extractor)
        - [Installing the Gradle Extractor](#installing-the-gradle-extractor)
        - [Installing Conan](#installing-conan)
        - [Using TFS 2015](#using-tfs-2015)
  - [Configuring the Service Connections](#configuring-the-service-connections)
  - [Using OpenID Connect (OIDC) Authentication](#using-openid-connect-oidc-authentication)
      - [Configure OpenID Connect Integration](#configure-openid-connect-integration)
      - [Configure Identity Mappings](#configure-identity-mappings)
      - [Configure the Service Connection](#configure-the-service-connection)
  - [Executing JFrog CLI Commands](#executing-jfrog-cli-commands)
      - [JFrog CLI V2 Task](#jfrog-cli-v2-task)
  - [Managing Generic Artifacts](#managing-generic-artifacts)
    - [Generic artifacts handling](#generic-artifacts-handling)
    - [Downloading generic build dependencies from Artifactory](#downloading-generic-build-dependencies-from-artifactory)
    - [Uploading generic build artifacts to Artifactory](#uploading-generic-build-artifacts-to-artifactory)
    - [Setting / Deleting properties on files in Artifactory](#setting--deleting-properties-on-files-in-artifactory)
    - [Moving / Copying / Deleting artifacts in Artifactory](#moving--copying--deleting-artifacts-in-artifactory)
  - [Build tools Tasks](#build-tools-tasks)
      - [JFrog Maven Task](#jfrog-maven-task)
      - [JFrog Gradle Task](#jfrog-gradle-task)
      - [JFrog Npm Task](#jfrog-npm-task)
      - [JFrog Nuget and .NET Core Task](#jfrog-nuget-and-net-core-task)
      - [JFrog Pip Task](#jfrog-pip-task)
      - [JFrog Conan Task](#jfrog-conan-task)
      - [JFrog Go Task](#jfrog-go-task)
  - [Build Tasks](#build-tasks)
      - [JFrog Collect Build Issues](#jfrog-collect-build-issues)
        - [Configuration properties](#configuration-properties)
      - [JFrog Publish Build Info](#jfrog-publish-build-info)
      - [JFrog Build Promotion](#jfrog-build-promotion)
        - [Using Build Promotion in a Release](#using-build-promotion-in-a-release)
      - [Discarding Published Builds from Artifactory](#discarding-published-builds-from-artifactory)
  - [JFrog Xray tasks](#jfrog-xray-tasks)
      - [Audit project's dependencies for Security Vulnerabilities](#audit-projects-dependencies-for-security-vulnerabilities)
      - [Scanning Published Builds for Security Vulnerabilities](#scanning-published-builds-for-security-vulnerabilities)
  - [JFrog Docker tasks](#jfrog-docker-tasks)
      - [Pushing and Pulling Docker Images to and from Artifactory](#pushing-and-pulling-docker-images-to-and-from-artifactory)
      - [Scanning Local Docker Images with JFrog Xray](#scanning-local-docker-images-with-jfrog-xray)
  - [Using Published Artifacts in a Release](#using-published-artifacts-in-a-release)
      - [Using JFrog Generic Artifacts task](#using-jfrog-generic-artifacts-task)
      - [Using Azure Artifact source](#using-azure-artifact-source)
  - [Managing and Distributing Release Bundles](#managing-and-distributing-release-bundles)
      - [JFrog Distribution V2 Task](#jfrog-distribution-v2-task)
  - [Contribution](#contribution)
    - [Building](#building)
    - [Testing](#testing)
      - [Skipping Tests](#skipping-tests)
  - [Reporting issues](#reporting-issues)

## Download and Installation

### Installing the Extension

To install the _[JFrog Extension](https://marketplace.visualstudio.com/items?itemName=JFrog.jfrog-azure-devops-extension)_, execute the following steps:

- Go to
    the [Visual Studio Marketplace Jfrog Extension Page](https://marketplace.visualstudio.com/items?itemName=JFrog.jfrog-azure-devops-extension)
    and sign in to your account.

                  <img src="./images/extension-install.png" alt=""/>

- Click on _Get It Free_

                  <img width="400px" src="./images/get-it-free.png" alt="">

- Select the account to which you want to apply the extension and confirm installation.

- In the JFrog Extension page, click _Install_.

                  <img width="400px" src="./images/organization-install.png" alt="">

### Installing the Build Agent

To run the JFrog tasks, the build agents use three tools:

- JFrog CLI: Runs all the JFrog tasks.
- Maven Extractor (Used by the [JFrog Maven](#jfrog-maven-task) task)
- Gradle Extractor (Used by the [JFrog Gradle](#jfrog-gradle-task) task)
- Conan client (Used by the [JFrog Conan](#jfrog-conan-task) task)

<details>
    <summary>

#### Automatic Installation

</summary>

If the build agent has access to the internet, JFrog CLI along with the Maven and Gradle Extractors are downloaded and
installed automatically on the agent, the first time they are required.

</details>

<details>
    <summary>

#### Custom tools Installation

</summary>

You can configure the pipeline to download JFrog CLI and the Maven Extractor from a JFrog Artifactory instance, which is
configured to proxy the download repositories.

- Create two remote repositories in Artifactory:
- Create a remote repository in Artifactory for downloading _JFrog CLI_. Name the repository _jfrog-cli-remote_ and
    set its URL
    to [https://releases.jfrog.io/artifactory/jfrog-cli/v2-jf/](https://releases.jfrog.io/artifactory/jfrog-cli/v2-jf/)
- Create a remote repository in Artifactory for downloading the _Maven and Gradle Extractors_. Name the URL _extractors_ and set its URL
    to: [https://releases.jfrog.io/artifactory/oss-release-local/](https://releases.jfrog.io/artifactory/oss-release-local/)
- Make sure to configure the Artifactory server with the _jfrog-cli-remote_ and _extractors_ repositories in as a
    [service connection](#configuring-the-service-connections) in Azure DevOps of type _JFrog Artifactory V2_.
- Add the _JFrog Tools Installer_ task to your build or release pipeline.
- Select the Artifactory service you configured.
- Select _jfrog-cli-remote_ as the target repository to download the JFrog CLI.
- If your pipeline uses the [JFrog Maven](#jfrog-maven-task) or [JFrog Gradle](#jfrog-gradle-task) tasks, select _extractors_ as the repository to
    download the Maven Extractor.

![tool-installer.png](images/tool-installer.png)

```YAML
- task: JFrogToolsInstaller@1
  inputs:
    artifactoryConnection: 'jfrog artifactory'
    cliInstallationRepo: 'jfrog-cli-remote'
    installExtractors: true
    extractorsInstallationRepo: 'extractors'
```

</details>

<details>
    <summary>

#### Manual Installation

</summary>

##### Installing JFrog CLI

The extension runs JFrog CLI in the background to run many of its operations.
The extension automatically downloads and installs the JFrog CLI on the build agent the first time it's required.
However, if your build agent does not have access to the internet, the build will fail when attempting to download JFrog
CLI, and you'll need to download and install it manually.

To install JFrog CLI on an agent with no internet access:

1. Create the directory structure on your agent's `file-system: $(Agent.ToolsDirectory)/_jf/current/`
2. Download the latest JFrog CLI version from [here](https://releases.jfrog.io/artifactory/jfrog-cli/v2-jf/).
3. Please make sure to download the executable matching your agent's operating system. Make sure to download the _jf_
   executable of JFrog CLI and not the legacy _jfrog_ executable.
4. Copy the downloaded _jf_ executable to the _current_ directory you created.

##### Installing the Maven Extractor

When triggering the [JFrog Maven](#jfrog-maven-task) task, JFrog CLI automatically downloads the Maven Extractor jar to the build agent
the first time it's required.
However, if your build agent does not have access to the internet, the build will fail when attempting to download the
file.
You'll therefore need to download and install it manually.

To install the Maven Extractor jar on an agent with no internet access:

1. Create the directory structure on your agent's
   file-system: `~/.jfrog/dependencies/maven/2.x.x`
2. Download
   the latest [build-info-extractor-maven3-2.x.x-uber.jar](https://search.maven.org/artifact/org.jfrog.buildinfo/build-info-extractor)
   and place it inside the "maven" directory you created.

##### Installing the Gradle Extractor

When triggering the [JFrog Gradle](#jfrog-gradle-task) task, JFrog CLI automatically downloads the Gradle Extractor jar to the build
agent the first time it's required.
However, if your build agent does not have access to the internet, the build will fail when attempting to download the
file. You'll therefore need to download and install it manually.

To install the Gradle Extractor jar on an agent with no internet access:

1. Create the directory structure on your agent's
   file-system: `~/.jfrog/dependencies/gradle/4.x.x`
2. Download
   the latest [build-info-extractor-gradle-4.x.x-uber.jar](https://plugins.gradle.org/plugin/com.jfrog.artifactory)
   and place it inside the "gradle" directory you created.

##### Installing Conan

For the build agent to be able to run conan builds, do the following:

1. Access the agent and install conan by following [these steps](https://docs.conan.io/en/latest/installation.html).
2. Confirm that the conan executable is available in the Path environment variable of the user which runs the build on
   the agent.

> The JFrog Conan task uses the Conan client. The Conan client cannot be installed
> using the Automatic Installation or the JFrog Tools Installer but is required to be manually installed.

##### Using TFS 2015

Node.JS version 8 and above.

The build agent requires using Node.JS version 8 and above. To check which version of Node.JS is running on the build
agent:

1. Navigate to the `Worker\Handlers\Node` folder located under the Agent home.
2. From the terminal, run _node -v_

To upgrade Node.JS on the build agent:

- Replace the existing node.exe file on the agent with the node.exe file with the required version located in
    the `Worker\Handlers\Node` folder under the agent home.

</details>

## Configuring the Service Connections

To allow the JFrog tasks to work with your JFrog environment, you'll need to configure the following service connections
in Azure DevOps.

|                     Service connection                      | Used by tasks                                                                                                                                                                                                                                                                     |
| :---------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|   <img width="200px" src="./images/service-platform.png">   | JFrog CLI V2                                                                                                                                                                                                                                                                      |
| <img width="200px" src="./images/service-artifactory.png">  | JFrog Tools Installer<br>JFrog Generic Artifacts<br>JFrog Nuget<br>JFrog .NET Core<br>JFrog npm<br>JFrog Pip<br>JFrog Maven<br>JFrog Gradle<br>JFrog Go<br>JFrog Conan<br>JFrog Collect Build Issues<br>JFrog Discard Builds<br>JFrog Build Promotion<br>JFrog Publish Build Info |
|     <img width="200px" src="./images/service-xray.png">     | JFrog Audit<br>JFrog Build Scan                                                                                                                                                                                                                                                   |
| <img width="200px" src="./images/service-distribution.png"> | JFrog Distribution                                                                                                                                                                                                                                                                |
<details>
  <summary>Not Using a Public CA (Certificate Authority)?</summary>

This section is relevant for you, if you're not using a public CA (Certificate Authority) to issue the SSL certificate
used to connect to your JFrog instance domain.
You may not be using a public CA either because you're using self-signed certificates or you're running your own PKI
services in-house (often by using a Microsoft CA).
In this case, you'll need to make those certificates available for JFrog CLI, which is used by most of JFrog tasks.
To make the certificates available for JFrog CLI, you'll need to place them inside the security/certs directory, which
is under JFrog CLI's home directory.
The home directory default location is `$(Agent.ToolsDirectory)/_jf/`

Read more about this in the [JFrog CLI](https://jfrog.com/help/r/jfrog-cli/jfrog-cli).

</details>

<details>
  <summary>Can't Access your JFrog instance?</summary>

For security reasons, the JFrog SaaS service supports only TLS 1.2. Since not all TFS versions support TLS 1.2, you may
need to enable TLS 1.2 on TFS.
To enable TLS 1.2 on TFS:

1. Create a file and name and name it: `Microsoft.PowerShell_profile.ps1`
2. Add the following line to the file: `[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12`
3. Place the file in the following location on the TFS machine: `C:\Users\<username>\Documents\WindowsPowerShell`

> Note: Make sure <username> matches the name of the user running TFS and the build agents.

</details>

<br>

## Using OpenID Connect (OIDC) Authentication

Using OpenID Connect (OIDC) to authenticate your pipelines eliminates the need for long lived static credentials providing a whole range of [security and practical benefits](https://jfrog.com/help/r/jfrog-platform-administration-documentation/openid-connect-integration-benefits).   
You can read more about the [JFrog OpenID Connection Integration](https://jfrog.com/help/r/jfrog-platform-administration-documentation/openid-connect-integration) in the documentation.

Setting up OpenID Connect has 3 separate parts:
- Setting up an OpenID Connect Integration inside of the JFrog Platform.
- Configuring Identity Mappings with Claim rules, matching to Projects & Service Connections.
- Configuring Service Connections as OpenID Connect in the Projects in your Azure Devops Instance.

Follow the guides below to configure each part.

<details>
    <summary>

#### Configure OpenID Connect Integration

</summary>


First you must configure your JFrog instance to have an OpenID Connect integration to your Azure DevOps server.
Login to your JFrog instance as an Administrator, then as [described in the documentation:](https://jfrog.com/help/r/jfrog-platform-administration-documentation/openid-connect-configurations-overview)

1. Go to the Administrator panel.
2. Select General Management.
3. Choose Manage Integrations.
4. Select New Integration - OpenID Connect

Now fill out the integration with the parameters of your Azure DevOps instance.

| Property name | Description                                                                             |
| ------------- | --------------------------------------------------------------------------------------- |
| Provider Name | A name for your provider, this name is used in the Azure DevOps tasks in the pipelines. |
| Provider Type | Must be set to `Generic OpenID Connect`                                                 |
| Description   | A description of what this provider is for.                                             |
| Provider URL  | `https://vstoken.dev.azure.com/{ORG_GUID}` (see how to get the {ORG_GUID} below).       |
| Audience      | Must be set to `api://AzureADTokenExchange`.                                            |
| Token Issuer  | If the issuer is different from the provider, for Azure DevOps this can be left blank.  |

As an example the final integration configuration will look like:

![oidc-integration.png](images/oidc-integration.png)

In order to obtain your Azure DevOps Organization GUID (`{ORG_GUID}`) you can simply run a pipeline in your Azure DevOps organization using any of the JFrog Task setup using a Service Connection configured with the `OpenID Connect Integration` authentication method, see the [Configure the Service Connection](#configure-the-service-connection) section. Even if the task fails due to you not yet having configured the Integration in JFrog, it will output the relevant information as part of the pipeline.

In the Pipeline Output, look for the `OIDC Token Issuer`, this value is what you must put in as your `Provider URL`.
The rest of the information can also be helpful for you to configure the Identity Mappings as described in the section below.

```
OIDC Token Subject: sc://<DevopsOrgName>/<ProjectName>/<ServiceConnectionName>
OIDC Token Claims: {"sub": "sc://<DevopsOrgName>/<ProjectName>/<ServiceConnectionName>"}
OIDC Token Issuer: https://vstoken.dev.azure.com/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
OIDC Token Audience: api://AzureADTokenExchange
```
</details>

<details>
    <summary>

#### Configure Identity Mappings

</summary>

When the `OpenID Connect Integration` has been configured, you must now configure `Identity Mappings` for your projects and service connections to allow them to utilize the integration.
You can find the full documentation for configuring [Identity Mappings in the Documentation](https://jfrog.com/help/r/jfrog-platform-administration-documentation/identity-mappings).
For this part we will focus on how to setup the JSON Claim which is used to map the JWT request of the pipeline to the access rights in your mapping.

When working with OpenID Connect, we must look at the `ID Token` that our provider (Azure DevOps) outputs. 
Based on the information in the token, we can map properties into rules in our `Identity Mappings` JSON Claim.
The `ID Token` from the Azure DevOps token provider looks like this:

```json
{
  "jti": "<guid>",
  "sub": "sc://<DevopsOrgName>/<ProjectName>/<ServiceConnectionName>",
  "aud": "api://AzureADTokenExchange",
  "iss": "https://vstoken.dev.azure.com/<ORG_GUID>",
  "nbf": 1708639268,
  "exp": 1708640467,
  "iat": 1708639868
}
```
Relative to most other `ID Token` providers, our options are fairly sparse, the only sensible option is using the subject (`"sub"`) field.
The claim mapping does support wildcards with the `*` operator.

A sample JSON Claim mapping which maps a specified ServiceConnection in a specified Project in your Organization would look like this:

```json
{ "sub": "sc://MyOrg/MyProject/MyServiceConnection" }
```
![oidc-json-mapping.png](images/oidc-json-mapping.png)

To allow all projects in your Organization with a ServiceConnection with a specified name, you could replace MyProject with `*`. 
Just make sure to never replace your Organization name with a `*` operator as that would allow any Azure DevOps Organization to gain access to your instance.

</details>

<details>
    <summary>

#### Configure the Service Connection

</summary>

You must configure a `ServiceConnection` setting the `Authentication method` to `OpenID Connect Integration`.
All four types of Service Connections are supported, they will all require the same input regardless of the type.

This requires you to fill in the following inputs: 

| Property name                | Description                                                                                            |
| ---------------------------- | ------------------------------------------------------------------------------------------------------ |
| Server URL                   | The URL of your JFrog instance with the `/artifactory` path fx. (`https://my.jfrog.io/artifactory`) |
| OpenID Connect Provider Name | The `Provider Name` you configured in the `Configure OpenID Connect Integration` step                  |
| Platform URL                 | The URL of your JFrog instance fx. (`https://my.jfrog.io/`)                                         |
| Service connection name      | The name of the Service Connection, must match the values put into the `JSON Claims mapping`           |
| Description (optional)       | A short of the purpose of this ServiceConnection                                                       |

A sample configuration would look like this:

![oidc-service-connection.png](images/oidc-service-connection.png)

Now this Service Connection can be used for any of JFrog tasks as normal, authenticating with a temporary access token each time the pipeline runs.

</details>


## Executing JFrog CLI Commands

<details>
    <summary>

#### JFrog CLI V2 Task

</summary>

The extension support a generic [JFrog CLI](https://jfrog.com/help/r/jfrog-cli/jfrog-cli) task, named _JFrog CLI V2_,
which allows executing _[JFrog CLI](https://jfrog.com/help/r/jfrog-cli/jfrog-cli)_ commands.
The command will use the connection details provided by the selected _JFrog Platform_ service connection configured in
Azure DevOps,
so there's no need to provide the connection details as command options.

![cli-v2-task.png](images/cli-v2-task.png)

Single command example:

```YAML
- task: JfrogCliV2@1
  inputs:
    jfrogPlatformConnection: 'JFrog Platform V2'
    command: |
- task: JfrogCliV2@1
  inputs:
    jfrogPlatformConnection: 'JFrog Platform V2'
    command: |
      jf go-config --repo-resolve=go-remote --repo-deploy=go-local
      jf go build
      jf go-publish v1.0.0
      jf rt bce $(Build.DefinitionName) $(Build.BuildNumber)
      jf rt build-publish $(Build.DefinitionName) $(Build.BuildNumber)
```

Multiple commands example:

```YAML
- task: JfrogCliV2@1
  inputs:
    jfrogPlatformConnection: 'JFrog Platform V2'
    command: |
      jf rt ping
      jf terraform-config --repo-deploy=terraform-remote
      jf terraform publish --namespace=example --provider=aws --tag=v0.0.1
```

</details>

<br>

## Managing Generic Artifacts

<details>
  <summary>JFrog Generic Artifacts task</summary>

The _JFrog Generic Artifacts_ task supports following operations with JFrog Artifactory:

- Uploading artifacts to Artifactory
- Downloading artifacts from Artifactory
- Copying artifacts in Artifactory
- Moving artifacts in Artifactory
- Deleting artifacts in Artifactory
- Setting properties on artifacts in Artifactory
- Deleting properties from artifacts in Artifactory

The task triggers [JFrog CLI](https://jfrog.com/help/r/jfrog-cli/jfrog-cli) to perform these actions
using [File Specs](https://jfrog.com/help/r/jfrog-integrations-documentation/using-file-specs).
When the task is used for uploading and downloading artifacts, it can also be configured to capture the build-info,
which can be later published to Artifactory using the _JFrog Publish Build Info_ task.

When configuring the task, do the following:

1. Select your configured _JFrog Artifactory V2_ service connection.

2. Specify whether you'd like define the File Spec through the task UI or have the task read the spec from a file.

3. Set the File Spec content or a path to the File Spec.

4. Set the other task options.

5. Check the _Advanced_ section for additional options.

### Generic artifacts handling

The _JFrog Generic Artifacts_ task allows performing generic actions on artifacts, such as:

1. Downloading and uploading from/to Artifactory
2. Setting or deleting properties on artifacts in Artifactory
3. Moving, copying and deleting artifacts in Artifactory

### Downloading generic build dependencies from Artifactory

The task supports downloading your build dependencies from Artifactory to the build agent.
The downloaded dependencies are defined
using [File Specs](https://jfrog.com/help/r/jfrog-integrations-documentation/using-file-specs)
and can be also configured to capture the build-info.
It will store the downloaded files as dependencies in the build-info which can later be published to Artifactory using
the _JFrog Publish Build-Info_ task.

![GenericDownload](images/marketplace/generic-download.png)

### Uploading generic build artifacts to Artifactory

The task also supports uploading your generated build artifacts from the build agent's local file system to Artifactory.
The artifacts are defined
using [File Specs](https://jfrog.com/help/r/jfrog-integrations-documentation/using-file-specs).
The task can be also configured to capture build-info and stores the uploaded files as artifacts in the build-info. The
captured build-info can be later published to Artifactory using the _JFrog Publish Build-Info_ task.

![GenericUpload](images/marketplace/generic-upload.png)

### Setting / Deleting properties on files in Artifactory

The JFrog Generic Artifacts task also allows both setting and deleting properties on artifacts in Artifactory.

![Props](images/marketplace/props.png)

### Moving / Copying / Deleting artifacts in Artifactory

Same task also allows performing generic actions on artifacts in Artifactory.

![Copy](images/marketplace/move-copy-delete.png)

YAML Example:

```YAML
- task: JFrogGenericArtifacts@1
  inputs:
    command: 'Upload'
    connection: 'jfrog artifactory'
    specSource: 'taskConfiguration'
    fileSpec: |
      {
        "files": [
          {
            "pattern": "libs-generic-local/*.zip",
            "target": "dependencies/files/"
          }
        ]
      }
    collectBuildInfo: true
    buildName: '$(Build.DefinitionName)'
    buildNumber: '$(Build.BuildNumber)'
    projectKey: 'proj'
    includeEnvVars: true
    failNoOp: true
```

</details>

<br>

## Build tools Tasks

<details>
  <summary>

#### JFrog Maven Task

</summary>

![mvn.png](images/marketplace/mvn.png)

The _JFrog Maven_ task allows triggering Maven builds, while resolving dependencies and deploying artifacts from and
to Artifactory.
The task uses the configured _JFrog Artifactory V2_ service connection.
The task can also be configured to capture build-info and store the downloaded and uploaded artifacts as build
dependencies and build artifacts.
The captured build-info can be later published to Artifactory using the _[JFrog Publish Build-Info](#jfrog-publish-build-info)_ task.

![mvn.png](images/maven-task.png)

You also have the option of filtering out some of the Maven artifacts that will be deployed to Artifactory.
You do this by defining one or more include patterns. You can also define one or more exclude patterns.
The patterns can include wildcards and should be separated by a comma followed by a white-space as shown below.

![mvn.png](images/maven-filter.png)

```YAML
- task: JFrogMaven@1
  inputs:
    mavenPomFile: 'pom.xml'
    goals: 'install'
    artifactoryResolverService: 'jfrog artifactory'
    targetResolveReleaseRepo: 'libs-release'
    targetResolveSnapshotRepo: 'libs-snapshot'
    artifactoryDeployService: 'jfrog artifactory'
    targetDeployReleaseRepo: 'libs-release'
    targetDeploySnapshotRepo: 'libs-snapshot'
    filterDeployedArtifacts: true
    includePatterns: 'artifact-*.jar,artifact-*.pom'
    excludePatterns: 'artifact-*-test.jar,artifact-*-test.pom'
    collectBuildInfo: true
    buildName: '$(Build.DefinitionName)'
    buildNumber: '$(Build.BuildNumber)'
    includeEnvVars: true
```

For more information about Maven repositories,
see [Artifactory Maven Repository](https://jfrog.com/help/r/jfrog-artifactory-documentation/maven-repository)

</details>

<details>
  <summary>

#### JFrog Gradle Task

</summary>

![gradle.png](images/marketplace/gradle.png)

The _JFrog Gradle_ task allows triggering Gradle builds, while resolving dependencies and deploying artifacts from and
to Artifactory.
The task uses the configured _JFrog Artifactory V2_ service connection.

The task can also be configured to capture build-info and store the downloaded and uploaded artifacts as build
dependencies and build artifacts.
The captured build-info can be later published to Artifactory using the _[JFrog Publish Build-Info](#jfrog-publish-build-info)_ task.

Behind the scenes, the _JFrog Gradle_ task uses
the [Gradle Artifactory Plugin](https://jfrog.com/help/r/jfrog-integrations-documentation/gradle-artifactory-plugin) to
integrate with the Gradle build.
In case your Gradle script already applies
the [Gradle Artifactory Plugin](https://jfrog.com/help/r/jfrog-integrations-documentation/gradle-artifactory-plugin),
set the _Use Artifactory Plugin_ option, to let the task know that it shouldn't apply the plugin in the Gradle script.

You should set _artifactoryPublish_ as one of the Gradle tasks in the task(s) fields.
_artifactoryPublish_ is a task that is exposed by the Gradle Artifactory Plugin, and is used for deploying artifacts
as well as publishing build-info to Artifactory.

![gradle.png](images/gradle-task.png)

```YAML
- task: JFrogGradle@1
  inputs:
    gradleBuildFile: 'build.gradle'
    tasks: 'artifactoryPublish'
    artifactoryResolverService: 'jfrog artifactory'
    sourceRepo: 'gradle-virtual'
    artifactoryDeployerService: 'jfrog artifactory'
    targetRepo: 'gradle-local'
```

</details>

<details>
  <summary>

#### JFrog Npm Task

</summary>

![npm.png](images/marketplace/npm.png)

The _JFrog Npm_ task allows triggering npm builds, while resolving npm dependencies and deploying npm packages from
and to Artifactory.
The task uses the configured _JFrog Artifactory V2_ service connection.

The task can be also configured to capture build-info and store the uploaded files as artifacts in it.
The captured build-info can be later published to Artifactory using the _[JFrog Publish Build-Info](#jfrog-publish-build-info)_ task.

![npm.png](images/npm-task.png)

```YAML
- task: JFrogNpm@1
  inputs:
    command: 'install'
    artifactoryConnection: 'jfrog artifactory'
    sourceRepo: 'npm-virtual'
    collectBuildInfo: true
    threads: '1'
    buildName: '$(Build.DefinitionName)'
    buildNumber: '$(Build.BuildNumber)'
    includeEnvVars: true
```

For information on npm repositories,
see [Artifactory npm Registry](https://jfrog.com/help/r/jfrog-artifactory-documentation/npm-registry)

</details>

<details>
  <summary>

#### JFrog Nuget and .NET Core Task

</summary>

![nuget.png](images/marketplace/nuget.png)

The _JFrog Nuget_ and _JFrog .NET Core_ tasks allow restoring NuGet packages from Artifactory.
These tasks also allow publishing NuGet packages to Artifactory.
The task uses the configured _JFrog Artifactory V2_ service connection.
The tasks can be configured to capture build-info.
The build-info stores the restored packages as build dependencies and uploaded packages as build artifacts.
The captured build-info can be later published to Artifactory using the _[JFrog Publish Build-Info](#jfrog-publish-build-info)_ task.

![nuget.png](images/nuget-task.png)

```YAML
- task: JFrogDotnetCore@1
  inputs:
    command: 'restore'
    artifactoryConnection: 'jfrog artifactory'
    targetResolveRepo: 'nuget-virtual'
    rootPath: '*/*.sln'
    collectBuildInfo: true
    buildName: '$(Build.DefinitionName)'
    buildNumber: '$(Build.BuildNumber)'
    includeEnvVars: true
```

For more information about Nuget repositories,
see [Artifactory NuGet Repositories](https://jfrog.com/help/r/jfrog-artifactory-documentation/nuget-repositories)

</details>

<details>
  <summary>

#### JFrog Pip Task

</summary>

![pip.png](images/marketplace/pip.png)

The _JFrog Pip_ task allows installing Pip packages from Artifactory.
The task uses the configured _JFrog Artifactory V2_ service connection.
The tasks can also be configured to capture build-info. The build-info stores the installed packages as build
dependencies.
The captured build-info can be later published to Artifactory using
the [Publishing Build Info to Artifactory](http://www.jfrog.com#PublishingBuildInfotoArtifactory) task.

![pip.png](images/pip-task.png)

```YAML
- task: JFrogPip@1
  inputs:
    artifactoryConnection: 'jfrog artifactory'
    command: 'install'
    targetResolveRepo: 'pypi'
    collectBuildInfo: true
    buildName: '$(Build.DefinitionName)'
    buildNumber: '$(Build.BuildNumber)'
```

_Recording all dependencies as part of the build-info_
When running the _JFrog Pip_ task inside a Python environment, which already has some of the packages installed, the
installed packages will not be included as part of the build-info, if they were not originally installed from
Artifactory. A warning message will be added to the build log in this case.

_How to include all packages in the build-info?_
Running the task for the first time with the _Disable local pip cache_ option checked,
should re-download and install these packages, and they will therefore be included in the build-info.
It is also recommended to run the command from inside
a [virtual environment](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/).
The _Virtual environment setup command_ field allows this.

![pip-advanced.png](images/pip-advanced.png)

Behind the scenes, the task uses JFrog CLI as a wrapper for pip.
JFrog CLI also includes a caching mechanism, which stores the details of the dependencies locally, making sure they are
included in the build-info, even if they are already cached locally.

</details>

<details>
  <summary>

#### JFrog Conan Task

</summary>

![conan.png](images/marketplace/conan.png)

[Conan](https://conan.io/) is a package manager for C and C++.

The _JFrog Conan_ task allows triggering a conan build while resolving conan dependencies from a conan repository in
Artifactory.
The task uses the configured _JFrog Artifactory V2_ service connection.
It also allows publishing conan packages to an Artifactory conan repository.
The task can be also configured to capture build-info and store the downloaded and uploaded packages as build
dependencies and artifact.
The captured build-info can be later published to Artifactory using the _[JFrog Publish Build-Info](#jfrog-publish-build-info)_ task.

The task supports the _config install_ , _add remote_ , _create_ and _upload_ conan commands.
In addition, it supports a _custom_ option, allowing to configure the task to execute any conan command.
The full documentation of Conan is available at the [conan website](https://docs.conan.io/en/latest/).

![conan.png](images/conan-task.png)

```YAML
- task: JFrogConan@1
  inputs:
    conanCommand: 'Install'
    pathOrReference: './'
    buildName: '$(Build.DefinitionName)'
    buildNumber: '$(Build.BuildNumber)'
```

For more information about Conan repositories,
see [Artifactory Conan Repositories](https://jfrog.com/help/r/jfrog-artifactory-documentation/conan-repositories)

</details>

<details>
  <summary>

#### JFrog Go Task

</summary>

The _JFrog Go_ task allows triggering a go build, while resolving go dependencies from a go repository in Artifactory.
The task uses the configured _JFrog Artifactory V2_ service connection.
It also allows publishing go packages to an Artifactory go repository.
The task can be also configured to capture build-info and store the downloaded and uploaded packages as build
dependencies and artifact.
The captured build-info can be later published to Artifactory using the _JFrog Publish Build-Info_ task.

![go.png](images/go-task.png)

```YAML
- task: JFrogGo@1
  inputs:
    command: 'build'
    artifactoryConnection: 'jfrog artifactory'
    resolutionRepo: 'go'
    collectBuildInfo: true
    buildName: '$(Build.DefinitionName)'
    buildNumber: '$(Build.BuildNumber)'
    includeEnvVars: true
    workingDirectory: 'golang-example/hello'
```

For more information about Go repositories,
see [Artifactory Go Repositories](https://jfrog.com/help/r/jfrog-artifactory-documentation/go-registry)

</details>

<br>

## Build Tasks

<details>
  <summary>

#### JFrog Collect Build Issues

</summary>

Being able to look at the build which was published to Artifactory, and see all JIRA issues associated with it, is one
of the most powerful capabilities of Artifactory when it comes to managing metadata about artifacts builds.

The _JFrog Collect Build Issues_ task collects the list of tracked project issues (for example, issues stored in JIRA,
GitHub or any other bug tracking systems, and adds these issues to the build-info.
The task uses the configured _JFrog Artifactory V2_ service connection. The issues are collected by reading the git
commit messages from the local git log.
Each commit message is matched against a pre-configured regular expression, which retrieves the issue ID and issue
summary.
The information required for collecting the issues is retrieved from a yaml configuration, which is set as part for the
task.

![collect-issues.png](images/collect-issues.png)

Here's the yaml configuration structure.

```YAML
version: 1
issues:
  trackerName: JIRA
  regexp: (.+-[0-9]+)\s-\s(.+)
  keyGroupIndex: 1
  summaryGroupIndex: 2
  trackerUrl: https://my-jira.com/issues
  aggregate: true
  aggregationStatus: RELEASED
```

##### Configuration properties

| Property name     | Description                                                                                                                                                                                                                                                                                                             |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Version           | The schema version is intended for internal use. Do not change!                                                                                                                                                                                                                                                         |
| trackerName       | The name (type) of the issue tracking system. For example, JIRA. This property can take any value.                                                                                                                                                                                                                      |
| regexp            | A regular expression used for matching the git commit messages. The expression should include two capturing groups - for the issue key (ID) and the issue summary. In the example above, the regular expression matches the commit messages as displayed in the following example:<br>HAP-1007 - This is a sample issue |
| keyGroupIndex     | The capturing group index in the regular expression used for retrieving the issue key. In the example above, setting the index to "1" retrieves HAP-1007 from this commit message:<br>HAP-1007 - This is a sample issue                                                                                                 |
| summaryGroupIndex | The capturing group index in the regular expression for retrieving the issue summary. In the example above, setting the index to "2" retrieves the sample issue from this commit message:<br>HAP-1007 - This is a sample issue                                                                                          |
| trackerUrl        | The issue tracking URL. This value is used for constructing a direct link to the issues in the Artifactory build UI.                                                                                                                                                                                                    |
| aggregate         | Set to true, if you wish all builds to include issues from previous builds.                                                                                                                                                                                                                                             |
| aggregationStatus | If aggregate is set to true, this property indicates how far in time should the issues be aggregated. In the above example, issues will be aggregated from previous builds, until a build with a RELEASE status is found. Build statuses are set when a build is promoted using the jfrog rt build-promote command.     |

The yaml configuration can be either be stored as text as part of the task configuration, or stored in a file.
The file can be saved in the source control, and fetched, together with the rest of the sources to the build agent.
It can then be accesses and used by this task.

</details>

<details>
  <summary>

#### JFrog Publish Build Info

</summary>

Most of the JFrog tasks can be configured to collect and store build-info locally.
The task uses the configured _JFrog Artifactory V2_ service connection.
The collected build info can be then published to Artifactory using the _JFrog Publish Build Info_ task.

For more information about Build Info,
see [Artifactory Build Integration](https://jfrog.com/help/r/jfrog-cli/build-integration)

When configuring the task, select your configured Artifactory service endpoints and specify whether you'd like to
collect environment variables from the agent and add them to the build-info.

![collect-issues.png](images/marketplace/build-publish.png)

```YAML
- task: JFrogPublishBuildInfo@1
  inputs:
    buildName: '$(Build.DefinitionName)'
    buildNumber: '$(Build.BuildNumber)'
    excludeEnvVars: '*password*;*psw*;*secret*;*key*;*token*;*auth*;'
```

After the build-info is published to Artifactory, it can be accessed from the _Artifactory_ tab in the Build Results.

![build-results.png](images/marketplace/build-results.png)
![bi-in-artifactory.png](images/marketplace/bi-in-artifactory.png)

</details>

<details>
  <summary>

#### JFrog Build Promotion

</summary>

To support the artifacts life-cycle, Artifactory supports promoting published builds from one repository to another.

The _JFrog Build Promotion_ task promotes a build, by either copying or moving the build artifacts and/or dependencies
to a target repository.

This task can be added as part of a Build or Release pipeline.

Run these steps to configure the _JFrog Build Promotion_ task:

1. Select the configured _JFrog Artifactory V2_ service connection, to which the build has been published.

2. Specify the name of a*target repository* to which the build should be promoted.

3. Set the _status_ of the build and optionally add a _Comment_. These details will be visible as part of the Build
   History in the Artifactory UI.

4. (Optional) Set a _source repository_ for the promotion.

5. Select the _include build dependencies_ if you want the build dependencies to be promoted.

6. To copy and not to move the artifacts to the target repository, select the _Use copy_ option to copy the artifacts
   to the target repository.

7. Select _Dry run_ to test the promotion prior to running the build promotion.

![build-promotion.png](images/marketplace/build-promotion.png)

```YAML
- task: JFrogBuildPromotion@1
  inputs:
    artifactoryConnection: 'jfrog artifactory'
    buildName: '$(Build.DefinitionName)'
    buildNumber: '$(Build.BuildNumber)'
    targetRepo: 'staging-local'
    status: 'Released'
    comment: 'Promoting release candidate'
    sourceRepo: 'Dev1-local'
    includeDependencies: false
    copy: true
    dryRun: false
```

##### Using Build Promotion in a Release

You can control the life cycle of your artifacts by promoting them from one Artifactory repository to another.
Build Promotion can come in handy when embedding it as part of release pipeline in Azure DevOps.
To help you achieve this, follow these steps for creating a release which includes the _JFrog Build Promotion_ task.

1. Create a new Release.
   ![promotion.png](images/promotion1.png)
2. Click _environment_ and select a template for the release.
   ![promotion.png](images/promotion2.png)
3. Click _Artifact_ and select _Build_ as the source type.
4. Fill out the rest of the form details.
5. If you'd like this release to always use the latest build from Artifactory, select specify a specific build number
   as the _Default version_ and select one of the available build number i the _Build number_ list box.
6. If you'd like to promote a specific build number during the release, select specify at the time of release
   creation as the _Default version_:
   ![promotion.png](images/promotion3.png)
7. If you wish to promote the latest build number, select specify a specific build number as the _Default version_
   and then select _any_ build number. Then, click on the _Variables_ tab and add
   the _ARTIFACTORY_RELEASE_BUILD_NUMBER_ pipeline variable with _LATEST_ as the value.
   ![promotion.png](images/promotion4.png)
8. Configure the _Artifactory Build Promotion_ task as one of your release pipeline tasks.
   The task uses a build number which will be selected later on, upon creating a release.
   ![promotion.png](images/promotion5.png)
9. That's it, you're done!
   Now you can create the release. The build number that you'll choose is that one which will be promoted in
   Artifactory.
   ![promotion.png](images/promotion6.png)

</details>

<details>
  <summary>

#### Discarding Published Builds from Artifactory

</summary>

To discard old runs of a build from Artifactory, add the _JFrog Discard Builds_ task to the pipeline.

Run these steps to configure the task.

1. Select the configured _JFrog Artifactory V2_ service connection, on which you'd like the builds to be discarded.

2. Type the name of the build.

3. Optionally set the maximum days to keep build runs. Build runs which are older will be discarded.

4. Optionally set the maximum number of builds to keep.

5. Optionally set of build runs in the form of 10,11,12,... to keep and not to discard.

6. Check the Delete artifacts checkbox, to also delete the build artifacts and not only the build meta-data.

7. Check the Async checkbox, to make the action asynchronous. In this case, the pipeline will not wait for the action to
   finish, but the pipeline will not be notified in case of a failure.
   ![build-discard.png](images/marketplace/discard.png)

```YAML
- task: JFrogDiscardBuilds@1
  inputs:
    artifactoryConnection: 'jfrog artifactory'
    buildName: '$(Build.DefinitionName)'
    maxDays: '60'
    maxBuilds: '400'
    excludeBuilds: '10,11,12'
    deleteArtifacts: true
```

</details>

<br>

## JFrog Xray tasks

<details>
  <summary>

#### Audit project's dependencies for Security Vulnerabilities

</summary>

The _JFrog Audit_ task triggers an audit of your project dependencies for security vulnerabilities with JFrog Xray.
The task uses the configured _JFrog Xray V2_ service connection.
The scan is synchronous, meaning the tasks waits for the scan to finish.
To determine the policy for identifying the vulnerabilities, you can either set a list for Xray Watches or select a
JFrog Project or path in Artifactory associated with the policy.

> This functionality requires version 3.29.0 or above of JFrog Xray.

![audit.png](images/marketplace/audit.png)
![violations-table.png](images/marketplace/violations-table.png)

```YAML
- task: JFrogAudit@1
  inputs:
    xrayConnection: 'jfrog xray token'
    watchesSource: 'watches'
    watches: 'watch1,watch2'
    allowFailBuild: true
```

</details>

<details>
  <summary>

#### Scanning Published Builds for Security Vulnerabilities

</summary>

The _JFrog Build Scan_ task allows triggering a build scan with JFrog Xray.
For the build to be scanned, it first needs to be published to Artifactory using the _[JFrog Publish Build-Info](#jfrog-publish-build-info)_ task.
The task uses the configured _JFrog Xray V2_ service connection.
When the scan is triggered, Xray starts scanning the build artifacts and dependencies.
The scan is synchronous, meaning the tasks waits for the scan to finish.
If the _Allow fail build_ task option is set and Xray is configured to fail the build, the build pipeline will fail,
if vulnerabilities are found.

> This functionality requires version 3.37.0 or above of JFrog Xray.

![build-scan.png](images/marketplace/build-scan.png)

```YAML
- task: JFrogBuildScan@1
  inputs:
    xrayConnection: 'jfrog xray token'
    buildName: '$(Build.DefinitionName)'
    buildNumber: '$(Build.BuildNumber)'
    allowFailBuild: true
    vuln: false
```

After the Xray scan is completed, a vulnerabilities table is printed to the task run logs, along with a link to the
build-info report.

![violations-table.png](images/marketplace/violations-table.png)
![violations-table.png](images/xray-scan-results.png)

</details>

<br>

## JFrog Docker tasks

<details>
  <summary>

#### Pushing and Pulling Docker Images to and from Artifactory

</summary>

The _JFrog Docker_ task allows pushing and pulling docker images to and from a docker repository in Artifactory.
The task can be also configured to capture build-info for the pushed or pulled image.
In addition to details about the build and the build environment, the build info includes the image layers as build
dependencies and build artifacts.
The task stores build info locally on the build agent.
The stored build-info can be later published to Artifactory using the _JFrog Publish Build Info_ task.

> This functionality requires version 7.33.3 or above of Artifactory.

For more information about Docker and Artifactory,
see [Artifactory Docker Registry](https://jfrog.com/help/r/jfrog-artifactory-documentation/docker-registry)

![docker-pull.png](images/marketplace/docker-pull.png)

```YAML
- task: JFrogDocker@1
  inputs:
    command: 'Pull'
    artifactoryConnection: 'jfrog artifactory'
    imageName: 'myjfrog.jfrog.io/docker-local/hello-world:latest'
    collectBuildInfo: true
    buildName: '$(Build.DefinitionName)'
    buildNumber: '$(Build.BuildNumber)'
    skipLogin: false
```

</details>

<details>
  <summary>

#### Scanning Local Docker Images with JFrog Xray

</summary>

The _JFrog Docker_ task allows scanning local docker images using JFrog Xray. The scan results is displayed in the
build log.

By default, the result will include all vulnerabilities found. You may however configure the task to show only
violations configured in Xray.

You do this by configuring the task to use:

1. Your JFrog Project. If there are Xray Watches associated with this Project, these Watches will be used.

2. Xray Watch or a list of Watches.

3. Repository path in Artifactory which has Xray Watches associated with it.

> This functionality requires version 3.40.0 or above of JFrog Xray.

![docker-scan.png](images/marketplace/docker-scan.png)

```YAML
- task: JFrogDocker@1
  inputs:
    command: 'Scan'
    xrayConnection: 'jfrog xray token'
    watchesSource: 'none'
    licenses: true
    allowFailBuild: true
    threads: '3'
    skipLogin: false
```

</details>

<br>

## Using Published Artifacts in a Release

Artifacts which were published to Artifactory can be made available for a Release Pipeline.
There are two ways to achieve this:

<details>
    <summary>

#### Using JFrog Generic Artifacts task

</summary>

The first way is to use the [JFrog Generic Artifacts](#managing-generic-artifacts) task to download the files during the
release. Read more about this in
the Downloading Generic Dependencies from Artifactory section.

</details>

<details>
    <summary>

#### Using Azure Artifact source

</summary>

You can also set Artifactory as an artifact source for the release.
This allows downloading the artifacts for a build which was previously published to Artifactory.
Read more about publishing builds to Artifactory in the Publishing Build
Info to Artifactory section.

Follow these steps to add Artifactory as an artifact source to a Release.

1. Create a new Release and click on _Artifacts Add_

    ![release1.png](images/release1.png)

2. Select the _Artifactory_ source type.

    ![release2.png](images/release2.png)

3. Select an Artifactory service, a build name, and the default version to use.

    ![release3.png](images/release3.png)

    That's it! You're done.

    Now, when initiating the Release, the artifacts associated with the defined build are downloaded to the release
    agent.

</details>

<br>

## Managing and Distributing Release Bundles

<details>
  <summary>

#### JFrog Distribution V2 Task

</summary>

[JFrog Distribution](https://jfrog.com/help/r/jfrog-distribution-documentation) is a centralized platform that lets you
provision software release distribution.
It is a core part of JFrog Enterprise+,
managing [Release Bundles](https://jfrog.com/help/r/jfrog-distribution-documentation/distributing-release-bundles) and
their distribution processes,
including release content, permission levels, and target destinations.
Distribution provides a secure and structured platform to distribute release binaries to multiple remote locations and
update them as new release versions are produced.
As part of the release flow, release bundles are verified by the target destination to ensure that they are signed
correctly and safe to use.
JFrog DistributionDistributing Release Bundles

The _JFrog Distribution_ task allows creating, updating, signing and deleting release bundles.
It also allows distributing the release to the edge nodes.

- The task requires configuring your _JFrog Distribution V2_ instance as a service connection in Azure DevOps.
- You can then set the instance you configured as the Distribution service value in the task.
- The task triggers [JFrog CLI](https://jfrog.com/help/r/jfrog-cli/jfrog-cli) to execute the distribution actions.
- When creating or updating a release bundle, you need to
    provide [File Specs](https://jfrog.com/help/r/jfrog-integrations-documentation/using-file-specs) defining the
    artifacts to be included in the release bundle.
- When distributing a release bundle, you can control the distribution destinations by defining rules distribution rules
    in a JSON format.

_Distribution Rules JSON structure_ Here's an example:

```JSON
   {
  "distribution_rules": [
    {
      "site_name": "DC-1",
      "city_name": "New-York",
      "country_codes": [
        "1"
      ]
    },
    {
      "site_name": "DC-2",
      "city_name": "Tel-Aviv",
      "country_codes": [
        "972"
      ]
    }
  ]
}
```

The Distribution Rules format also supports wildcards. For example:

```JSON
   {
  "distribution_rules": [
    {
      "site_name": "*",
      "city_name": "*",
      "country_codes": [
        "*"
      ]
    }
  ]
}
```

![distribution.png](images/marketplace/distribution.png)

```YAML
- task: JFrogDistribution@1
  inputs:
    command: 'distribute'
    distributionConnection: 'distCon'
    rbName: 'myReleaseBundle'
    rbVersion: '$(Build.BuildNumber)'
    distRulesSource: 'taskConfiguration'
    distSync: true
    maxWaitSync: '40'
```

</details>

<br>

## Contribution

We welcome pull requests from the community!

<details>
    <summary>Building</summary>

### Building

To build and run the extension sources, please follow these steps:

1. Clone the code from git.
2. To Build and create the JFrog Artifactory extension `vsix` file, run the following command.

    ```
    npm i
    npm run create
    ```

After the build process is completed, you'll find the `vsix` file in the project directory.
The `vsix` file can be loaded into Azure DevOps and TFS.

</details>

<details>
    <summary>Testing</summary>

### Testing

To run the tests, please make sure you are using node 14 or above.

Use the following commands to run from terminal:

1. Set the ADO_JFROG_PLATFORM_URL, ADO_JFROG_PLATFORM_USERNAME and ADO_JFROG_PLATFORM_PASSWORD environment variables
   with your JFrog Platform URL, username and password:

    ```
    export ADO_JFROG_PLATFORM_URL='https://myrepo.jfrog.io/'
    export ADO_JFROG_PLATFORM_USERNAME=admin
    export ADO_JFROG_PLATFORM_PASSWORD=password
    ```

2. Run the following commands:

    ```
    npm i -g jfrog-cli-v2-jf
    npm t
    ```

Note: If you are running tests via your IDE, make sure you are registering tests with
ts-node: `mocha -r ts-node/register tests.ts -t 1000000`.

#### Skipping Tests

In order to skip tests, set the ADO*SKIP_TESTS environment variable with the tests you wish to skip, separated by
commas.
The supported values are: \_maven*, _gradle_, _npm_, _go_, _nuget_, _dotnet_, _conan_, _pip_, _proxy_,
_distribution_, _unit_, _installer_ and _generic_.

For example, for skipping the nuget and dotnet tests:

```
export ADO_SKIP_TESTS=nuget,dotnet
```

</details>

<details>
    <summary>Pull request guidelines</summary>

- Pull requests should be created on the _dev_ branch.
- Please make sure the code is covered by tests.
- Please run `npm run format` for formatting the code before submitting the pull request.
- Please run `npm run lint` and make sure no new tslint warnings were introduced.

</details>

## Reporting issues

Please help us improve jfrog-azure-devops-extension by [reporting issues](https://github.com/jfrog/jfrog-azure-devops-extension/issues/new/choose) you encounter.
