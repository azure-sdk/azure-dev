# JSON Schema

## Properties

- **`name`** *(string)*
- **`resourceGroup`** *(string)*: When specified will override the resource group name used for infrastructure provisioning.
- **`metadata`** *(object)*
  - **`template`** *(string)*

    Examples:
    ```json
    "todo-nodejs-mongo@0.0.1-beta"
    ```

- **`infra`** *(object)*: Optional. Provides additional configuration for Azure infrastructure provisioning. Can contain additional properties.
  - **`provider`** *(string)*: Optional. The infrastructure provisioning provider used to provision the Azure resources for the application. (Default: bicep). Must be one of: `['bicep', 'terraform']`.
  - **`path`** *(string)*: Optional. The relative folder path to the Azure provisioning templates for the specified provider. (Default: infra).
  - **`module`** *(string)*: Optional. The name of the Azure provisioning module used when provisioning resources. (Default: main).
- **`services`** *(object)*: Can contain additional properties.
  - **Additional Properties** *(object)*: Cannot contain additional properties.
    - **`resourceName`** *(string)*: By default, the CLI will discover the Azure resource with tag 'azd-service-name' set to the current service's name. When specified, the CLI will instead find the Azure resource with the matching resource name.
    - **`project`** *(string)*
    - **`host`** *(string)*: If omitted, App Service will be assumed. Must be one of: `['', 'appservice', 'containerapp', 'function', 'staticwebapp']`.
    - **`language`** *(string)*: If omitted, .NET will be assumed. Must be one of: `['', 'dotnet', 'csharp', 'fsharp', 'py', 'python', 'js', 'ts', 'java']`.
    - **`module`** *(string)*: If omitted, the CLI will assume the module name is the same as the service name.
    - **`dist`** *(string)*
    - **`docker`** *(object)*: This is only applicable when `host` is `containerapp`. Cannot contain additional properties.
      - **`path`** *(string)*: Path to the Dockerfile is relative to your service. Default: `./Dockerfile`.
      - **`context`** *(string)*: When specified overrides the default context. Default: `.`.
      - **`platform`** *(string)*: Default: `amd64`.
      - **`tag`** *(string)*: If omitted, a unique tag will be generated based on the format: {appName}/{serviceName}-{environmentName}:azdev-deploy-{unix time (seconds)}. Use environment variable substitution to generate unique tags for a given release. For example, myapp/myimage:${DOCKER_IMAGE_TAG}.
- **`pipeline`** *(object)*
  - **`provider`** *(string)*: Optional. The pipeline provider to be used for continuous integration. (Default: github). Must be one of: `['github', 'azdo']`.
