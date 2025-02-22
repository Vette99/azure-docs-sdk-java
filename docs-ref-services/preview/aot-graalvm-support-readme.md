---
title: Azure GraalVM Support client library for Java
keywords: Azure, java, SDK, API, azure-aot-graalvm-support, aot
author: joshfree
ms.author: jfree
ms.date: 04/08/2022
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: aot
---
# Azure GraalVM Support client library for Java - Version 1.0.0-beta.1 


The Azure GraalVM Support client library provides support for applications using [Azure client libraries](https://azure.
github.io/azure-sdk/releases/latest/java.html) to be built as [GraalVM native 
images](https://www.graalvm.org/22.0/reference-manual/native-image/). The library contains all the necessary 
[configuration files](https://www.graalvm.org/22.0/reference-manual/native-image/BuildConfiguration/) and [GraalVM 
features](https://www.graalvm.org/sdk/javadoc/index.html?org/graalvm/nativeimage/hosted/Feature.html) required to build 
a native image of an application that uses Azure client libraries.

## Getting started

### Prerequisites
- A [Java Development Kit (JDK)][jdk_link], version 8 or later.
- [Azure Subscription][azure_subscription]
- [GraalVM](https://www.graalvm.org/downloads/) version 22 or later.
- [GraalVM Native Image](https://www.graalvm.org/22.0/reference-manual/native-image/)

For more details, please refer to [Getting started with GraalVM](https://www.graalvm.org/22.0/docs/getting-started/) 
documentation.

### Include the package

[//]: # ({x-version-update-start;com.azure:azure-aot-graalvm-support;current})
```xml
<dependency>
    <groupId>com.azure</groupId>
    <artifactId>azure-aot-graalvm-support</artifactId>
    <version>1.0.0-beta.1</version>
</dependency>
```

Add the above dependency to your Maven project along with any other Azure client libraries you may want to use. If 
you are using client libraries that depend on `azure-core-http-netty`, add the `azure-aot-graalvm-support-netty` 
dependency too. For more details on this library, please refer to [this README](https://github.com/Azure/azure-sdk-for-java/blob/azure-aot-graalvm-support_1.0.0-beta.1/sdk/aot/azure-aot-graalvm-support-netty/README.md).

## Key concepts

### Native Image creation

Native Image is a technology to compile your Java application ahead of time into a native image which can run as a 
standalone application. The native image created through this ahead-of-time compilation will include all the 
necessary classes from the application, it's dependencies and any other natively linked JDK code. For more details 
on creating the native image please refer to [building a native image](https://www.graalvm.org/22.0/reference-manual/native-image/#build-a-native-image) documentation.

### GraalVM configuration files

GraalVM is a high-performance runtime that creates native images by compiling the Java code ahead of time. Due to 
this ahead-of-time compilation into a native image, the native image creation requires statically analyzing all 
classes of the application and their dependencies to determine which classes and methods are reachable during the 
application execution. However, there are scenarios where Java allows looking up classes, methods and fields at 
runtime through reflection. While GraalVM does a best-effort discovery of all classes ahead of time, it will not be 
able to detect all classes that are reflectively accessed. So, developers can provide configuration files that 
contain details of all necessary classes that are reflectively accessed. This supplementary information is then used 
to create the native image and make these classes available at runtime. 

This library provides all the necessary configuration files for using Azure client libraries.

## Examples

#### [App Configuration](https://github.com/Azure/azure-sdk-for-java/tree/azure-aot-graalvm-support_1.0.0-beta.1/sdk/appconfiguration/azure-data-appconfiguration)
- [Sample demonstrating the creation and use of App Configuration client](https://github.com/Azure/azure-sdk-for-java/blob/azure-aot-graalvm-support_1.0.0-beta.1/sdk/aot/azure-aot-graalvm-samples/src/main/java/com/azure/aot/graalvm/samples/appconfiguration/AppConfigurationSample.java)

#### [Key Vault](https://github.com/Azure/azure-sdk-for-java/tree/azure-aot-graalvm-support_1.0.0-beta.1/sdk/keyvault)
- [Sample demonstrating the creation and use of Key Vault Certificates client](https://github.com/Azure/azure-sdk-for-java/blob/azure-aot-graalvm-support_1.0.0-beta.1/sdk/aot/azure-aot-graalvm-samples/src/main/java/com/azure/aot/graalvm/samples/keyvault/certificates/KeyVaultCertificatesSample.java)
- [Sample demonstrating the creation and use of Key Vault Keys client](https://github.com/Azure/azure-sdk-for-java/blob/azure-aot-graalvm-support_1.0.0-beta.1/sdk/aot/azure-aot-graalvm-samples/src/main/java/com/azure/aot/graalvm/samples/keyvault/keys/KeyVaultKeysSample.java)
- [Sample demonstrating the creation and use of Key Vault Secrets client](https://github.com/Azure/azure-sdk-for-java/blob/azure-aot-graalvm-support_1.0.0-beta.1/sdk/aot/azure-aot-graalvm-samples/src/main/java/com/azure/aot/graalvm/samples/keyvault/secrets/KeyVaultSecretsSample.java)

#### [Storage Blob](https://github.com/Azure/azure-sdk-for-java/tree/azure-aot-graalvm-support_1.0.0-beta.1/sdk/storage/azure-storage-blob)
- [Sample demonstrating the creation and use of Storage Blob client](https://github.com/Azure/azure-sdk-for-java/blob/azure-aot-graalvm-support_1.0.0-beta.1/sdk/aot/azure-aot-graalvm-samples/src/main/java/com/azure/aot/graalvm/samples/storage/blob/StorageBlobSample.java)

#### [Cosmos](https://github.com/Azure/azure-sdk-for-java/tree/azure-aot-graalvm-support_1.0.0-beta.1/sdk/cosmos/azure-cosmos)
- [Sample demonstrating the creation and use of Cosmos client](https://github.com/Azure/azure-sdk-for-java/blob/azure-aot-graalvm-support_1.0.0-beta.1/sdk/aot/azure-aot-graalvm-samples/src/main/java/com/azure/aot/graalvm/samples/cosmos/CosmosSample.java)

#### [Event Hubs](https://github.com/Azure/azure-sdk-for-java/tree/azure-aot-graalvm-support_1.0.0-beta.1/sdk/eventhubs/azure-messaging-eventhubs)
- [Sample demonstrating the creation and use of Event Hubs producer client](https://github.com/Azure/azure-sdk-for-java/blob/azure-aot-graalvm-support_1.0.0-beta.1/sdk/aot/azure-aot-graalvm-samples/src/main/java/com/azure/aot/graalvm/samples/eventhubs/EventHubsSample.java)

#### [Form Recognizer](https://github.com/Azure/azure-sdk-for-java/tree/azure-aot-graalvm-support_1.0.0-beta.1/sdk/formrecognizer/azure-ai-formrecognizer)
- [Sample demonstrating the creation and use of Form Recognizer client](https://github.com/Azure/azure-sdk-for-java/blob/azure-aot-graalvm-support_1.0.0-beta.1/sdk/aot/azure-aot-graalvm-samples/src/main/java/com/azure/aot/graalvm/samples/formrecognizer/FormRecognizerSample.java)

#### [Text Analytics](https://github.com/Azure/azure-sdk-for-java/tree/azure-aot-graalvm-support_1.0.0-beta.1/sdk/textanalytics/azure-ai-textanalytics)
- [Sample demonstrating the creation and use of Text Analytics client](https://github.com/Azure/azure-sdk-for-java/blob/azure-aot-graalvm-support_1.0.0-beta.1/sdk/aot/azure-aot-graalvm-samples/src/main/java/com/azure/aot/graalvm/samples/textanalytics/TextAnalyticsSample.java)

## Troubleshooting

## Next steps
The [azure-aot-graalvm-samples](https://github.com/Azure/azure-sdk-for-java/tree/azure-aot-graalvm-support_1.0.0-beta.1/sdk/aot/azure-aot-graalvm-samples)
library consists of all above samples bundled into a single Maven project that can be compiled with `mvn clean 
install -Pnative` to build the native image and execute all the samples. 

## Contributing

This project welcomes contributions and suggestions. Most contributions require you to agree to a Contributor License
Agreement (CLA) declaring that you have the right to, and actually do, grant us the rights to use your contribution.
For details, visit [https://cla.microsoft.com](https://cla.microsoft.com).

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide a CLA and decorate the
PR appropriately (e.g., label, comment). Simply follow the instructions provided by the bot. You will only need to do this
once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact
[opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

<!-- LINKS -->
[cla]: https://cla.microsoft.com
[coc]: https://opensource.microsoft.com/codeofconduct/
[coc_faq]: https://opensource.microsoft.com/codeofconduct/faq/
[coc_contact]: mailto:opencode@microsoft.com
[jdk_link]: https://docs.microsoft.com/java/azure/jdk/?view=azure-java-stable
[azure_subscription]: https://azure.microsoft.com/free

![Impressions](https://azure-sdk-impressions.azurewebsites.net/api/impressions/azure-sdk-for-java%2Fsdk%2Faot%2Fazure-aot-graalvm-support%2FREADME.png)

