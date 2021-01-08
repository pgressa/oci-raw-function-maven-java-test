## Micronaut 2.3.0-SNAPSHOT Documentation

- [User Guide](https://docs.micronaut.io/snapshot/guide/index.html)
- [API Reference](https://docs.micronaut.io/snapshot/api/index.html)
- [Configuration Reference](https://docs.micronaut.io/snapshot/guide/configurationreference.html)
- [Micronaut Guides](https://guides.micronaut.io/index.html)
---

## Feature oracle-function documentation

- [Micronaut Oracle Function Support documentation](https://micronaut-projects.github.io/micronaut-oracle-cloud/latest/guide/#functions)

- [https://docs.cloud.oracle.com/en-us/iaas/Content/Functions/Concepts/functionsoverview.htm](https://docs.cloud.oracle.com/en-us/iaas/Content/Functions/Concepts/functionsoverview.htm)

## Handler

[AWS Lambda Handler](https://docs.aws.amazon.com/lambda/latest/dg/java-handler.html)

Handler: com.example.BookRequestHandler

## Oracle Functions GitHub Workflow

Workflow file: [`.github/workflows/oci-functions.yml`](.github/workflows/oci-functions.yml)

### Workflow description
For pushes to the `master` branch, the workflow will:
1. Setup the build environment with respect to the selected java or GraalVM version.
1. Login to the [Oracle Cloud Infrastructure Registry (OCIR)](https://docs.cloud.oracle.com/en-us/iaas/Content/Registry/Concepts/registryoverview.htm).
1. Install and configure [Oracle Cloud Infrastructure CLI](https://docs.cloud.oracle.com/en-us/iaas/Content/API/Concepts/cliconcepts.htm).
1. Build, tag and push Docker image with Micronaut application to the OCIR.
1. Create or update [Oracle Cloud Functions](https://docs.cloud.oracle.com/en-us/iaas/Content/Functions/Concepts/functionsoverview.htm) with name `oci-raw-function-maven-java-test` using built Docker container image.

### Dependencies on other GitHub Actions
- [Setup GraalVM `DeLaGuardo/setup-graalvm`](https://github.com/DeLaGuardo/setup-graalvm)

### Setup
Add the following GitHub secrets:

| Name | Description |
| ---- | ----------- |
| OCI_AUTH_TOKEN | OCI account auth token. |
| OCI_OCIR_REPOSITORY | (Optional) Docker image repository in OCIR. For image `iad.ocir.io/[tenancy name]/foo/bar:0.1`, the `foo` is an _image repository_. |
| OCI_USER_OCID | OCI user ocid. |
| OCI_TENANCY_OCID | OCID of the tenancy. |
| OCI_KEY_FILE | OCI api signing private key file. See more on [Setup of API signing key](https://docs.cloud.oracle.com/en-us/iaas/Content/Functions/Tasks/functionssetupapikey.htm). |
| OCI_FINGERPRINT | OCI Api signing key file fingerprint. |
| OCI_PASSPHRASE | Passphrase to the private key file. Required only when passphrase is needed by the private key file. |
| OCI_FUNCTION_APPLICATION_OCID | Oracle function application OCID. See more on [Creating Applications](https://docs.cloud.oracle.com/en-us/iaas/Content/Functions/Tasks/functionscreatingapps.htm). |

The workflow file `.github/workflows/graalvm.yml` also contains additional configuration options that are now configured to:
| Name | Description | Default value |
| ---- | ----------- | ------------- |
| OCI_REGION | Oracle Infrastructure Cloud region. See more on [Regions and Availability Domains](https://docs.cloud.oracle.com/en-us/iaas/Content/General/Concepts/regions.htm).  | `us-ashburn-1` |
| OCI_OCIR_URL | Oracle Cloud Infrastructure Registry region endpoint. See more on [Regional availability](https://docs.cloud.oracle.com/en-us/iaas/Content/Registry/Concepts/registryprerequisites.htm#regional-availability). | `iad.ocir.io` |
| OCI_FUNCTION_MEMORY_IN_MBS | Maximum memory threshold for a function. See more on [Changing Oracle Functions Default Behavior](https://docs.cloud.oracle.com/en-us/iaas/Content/Functions/Tasks/functionscustomizing.htm) | `128` |
| OCI_FUNCTION_TIMEOUT_IN_SECONDS | Timeout for executions of the function. Value in seconds. | `120` |

### Verification
Copy the function ID from the workflow's `Deploy Function` step.

For example output below it is `ocid1.fnfunc.oc1.iad.______5ds7`:
Action completed. Waiting until the resource has entered state: ('ACTIVE',)
```
{
  "data": {
    ....
    "display-name": "oci-function-gradle-test",
    "freeform-tags": {},
    "id": "ocid1.fnfunc.oc1.iad.______5ds7",
    "lifecycle-state": "ACTIVE",
    "memory-in-mbs": 128,
    "timeout-in-seconds": 30
    ....
    }
}
```

Invoke the function using Oracle Cloud Infrastructure CLI:
```
oci fn function invoke --function-id [FUNCTION-ID]  --file "-" --body ""
```

For more invocation options visit [Invoking Functions](https://docs.cloud.oracle.com/en-us/iaas/Content/Functions/Tasks/functionsinvokingfunctions.htm).

## Feature oracle-function documentation

- [Micronaut Oracle Function Support documentation](https://micronaut-projects.github.io/micronaut-oracle-cloud/latest/guide/#functions)

- [https://docs.cloud.oracle.com/en-us/iaas/Content/Functions/Concepts/functionsoverview.htm](https://docs.cloud.oracle.com/en-us/iaas/Content/Functions/Concepts/functionsoverview.htm)

## Feature aws-lambda documentation

- [Micronaut AWS Lambda Function documentation](https://micronaut-projects.github.io/micronaut-aws/latest/guide/index.html#lambda)

## Feature github-workflow-oracle-oci-functions documentation

- [https://docs.github.com/en/free-pro-team@latest/actions](https://docs.github.com/en/free-pro-team@latest/actions)

