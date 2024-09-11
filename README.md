# ``EdgeCore``

mimik Client Library for iOS provides a programmatic way to work with the edgeEngine Runtime to access information about the mobile device on which the application is running.

@Metadata {
    @CallToAction(purpose: link, url: "https://github.com/mimikgit/cocoapod-EdgeCore")
    @PageKind(article)
    @PageColor(purple)
}


## Overview

The purpose of the **mimik Client Library for iOS** is to provide a programmatic way to work with the edgeEngine Runtime to access information about the mobile device on which the application is running, as well as mobile devices running within a cluster of mobile devices that are hosting the edgeEngine Runtime. Also, to allow developers to use edge microservices running within a particular cluster.

The **mimik Client Library for iOS suite** consists of these individual cocoapod components:

    - EdgeCore
    - EdgeEngineDeveloper (for developer projects) 
    - EdgeEngine (for enterprise projects) 

By leveraging the **`EdgeCore cocoapod`**, developers can build applications compatible with the edgeEngine Runtime.

Additionally, this component provides utility APIs that help developers with core operations such as Authentication, edgeEngine Runtime Setup, deployment of edge microservices and handling of network calls.

Furthermore, the **`EdgeEngineDeveloper (or EdgeEngine for enterprise projects) cocoapod`** provides edgeEngine Runtime lifecycle control API, as well as vendoring the actual edgeEngine Runtime binary into the iOS project.

Expanding the client library ecosystem is the **`EdgeService` cocoapod**, providing API for integrating mimik edge and backend microservices.


## Supported Platforms, Targets
* `iOS Devices running iOS 15+`
* `iOS Simulators running iOS 15+`
* `iOS Mac Catalyst running macOS 12.0`


## Requirements
```
iOS 15.0+
```

## Installation

To install `EdgeCore` and `EdgeEngineDeveloper (or EdgeEngine for enterprise solutions)` cocoapods simply add the following lines to your Podfile:

> **_NOTE:_** Developers wanting to use their **developer edge license** from [mimik developer console](https://developer.mimik.com/console) should specify [EdgeEngineDeveloper](https://github.com/mimikgit/cocoapod-EdgeEngineDeveloper) cocoapod in their `Podfile`.

> **_NOTE:_** Enterprise project developers should specify [EdgeEngine](https://github.com/mimikgit/cocoapod-EdgeEngine) cocoapod in their `Podfile` and use the **full edge license** they received from [mimik support](https://developer.mimik.com/support/).


```swift
platform :ios, '15.0'
source 'https://github.com/CocoaPods/Specs.git'
source 'https://github.com/mimikgit/cocoapod-edge-specs.git'

use_frameworks!
inhibit_all_warnings!

def mimik
  pod 'EdgeCore'
  pod 'EdgeEngineDeveloper'
  ### or pod 'EdgeEngine' (for enterprise projects, see the two notes above)
end

target '{target}' do
  mimik()
end

post_install do |installer|
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      config.build_settings['ENABLE_BITCODE'] = 'NO'
      config.build_settings['VALID_ARCHS'] = '$(ARCHS_STANDARD_64_BIT)'
      config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = '15.0'
      config.build_settings['BUILD_LIBRARY_FOR_DISTRIBUTION'] = 'YES'
    end
  end
end
```

## Tutorials

After installation, try the following tutorials:

- [Integrating the mimik Client Library into an iOS project](https://devdocs.mimik.com/tutorials/11-index)
- [Working with edgeEngine in an iOS project](https://devdocs.mimik.com/tutorials/12-index)
- [Working with edge microservices in an iOS project](https://devdocs.mimik.com/tutorials/13-index)
- [Creating a Simple iOS Application that Uses an edge microservice](https://devdocs.mimik.com/tutorials/10-index)


## Documentation

`EdgeCore/EdgeClient` API reference documentation can be found  [online](https://mimikgit.github.io/cocoapod-EdgeCore/documentation/edgecore/edgeclient). Alternatively a docc archive file can be downloaded as a [zip file](https://github.com/mimikgit/cocoapod-EdgeCore/tree/main/EdgeCore.doccarchive.zip) and opened locally in Xcode.

`EdgeEngineClient` platform protocol API reference documentation can also be found [online](https://mimikgit.github.io/cocoapod-EdgeCore/documentation/edgecore/edgeengineclient).

`EdgeService` API reference documentation is also [online](https://mimikgit.github.io/cocoapod-EdgeService/documentation/).

## EdgeClient

### Authentication

- ``EdgeClient/authorizeDeveloper(developerIdToken:edgeEngineIdToken:)``
- ``EdgeClient/authorizeUser(email:password:edgeEngineIdToken:service:)``
- ``EdgeClient/authorizeUser(phoneNumber:edgeEngineIdToken:service:)``
- ``EdgeClient/validateUser(codes:edgeEngineIdToken:service:)``
- ``EdgeClient/signup(email:password:edgeEngineIdToken:service:)``
- ``EdgeClient/validateSignup(codes:password:edgeEngineIdToken:service:)``
- ``EdgeClient/authorizeBackendUse(authorization:service:)``
- ``EdgeClient/authorizeBackendUse(federatedToken:policyId:edgeEngineIdToken:service:)``
- ``EdgeClient/authenticationScopes(serverUrl:)``

### Account Management

- ``EdgeClient/accountInformation(service:authorization:)``
- ``EdgeClient/passwordReset(email:edgeEngineIdToken:service:)``
- ``EdgeClient/validatePasswordReset(codes:newPassword:edgeEngineIdToken:service:)``
- ``EdgeClient/passwordChange(email:currentPassword:newPassword:edgeEngineIdToken:service:)``
- ``EdgeClient/deleteAccount(email:password:edgeEngineIdToken:service:)``
- ``EdgeClient/validateDeleteAccount(codes:password:edgeEngineIdToken:service:)``
- ``EdgeClient/executeDeleteAccount(authorization:service:)``

### Environment

- ``EdgeClient/edgeEngineIdToken()``
- ``EdgeClient/edgeEngineInfo()``
- ``EdgeClient/externalEdgeEngineIsRunning()``
- ``EdgeClient/edgeEngineFullPathUrl()``

### Edge microservices

- ``EdgeClient/deployUseCase(accessToken:configUrl:dynamicConfig:)``
- ``EdgeClient/deployMicroservice(edgeEngineAccessToken:config:imageTarPath:)``
- ``EdgeClient/microservices(edgeEngineAccessToken:)``
- ``EdgeClient/microservice(containerName:edgeEngineAccessToken:)``
- ``EdgeClient/updateMicroserviceEnv(edgeEngineAccessToken:microservice:envVariables:)``
- ``EdgeClient/undeployMicroservice(edgeEngineAccessToken:microservice:)``

### EdgeClient Type

- ``EdgeClient/activateExternalEdgeEngine(host:port:)``
- ``EdgeClient/deactivateExternalEdgeEngine()``
- ``EdgeClient/edgeEngineWorkingDirectory()``
- ``EdgeClient/externalEdgeEngineIsActivated()``
- ``EdgeClient/setLoggingLevel(module:level:privacy:)``


## EdgeClient/AI

- ``EdgeClient/integrateAI(accessToken:apiKey:configUrl:model:downloadHandler:requestHandler:)``
- ``EdgeClient/downloadAIModel(accessToken:apiKey:model:useCase:downloadHandler:requestHandler:)``
- ``EdgeClient/askAI(modelId:accessToken:apiKey:question:useCase:streamHandler:requestHandler:)``
- ``EdgeClient/availableModels(accessToken:apiKey:useCase:)``


## EdgeClient/Authorization/AccessToken

- ``EdgeClient/Authorization/AccessToken/clientId(token:)``
- ``EdgeClient/Authorization/AccessToken/decodeToJWT(token:)``
- ``EdgeClient/Authorization/AccessToken/decodeToJson(token:)``
- ``EdgeClient/Authorization/AccessToken/expiresIn(token:)``
- ``EdgeClient/Authorization/AccessToken/subscriber(token:)``
- ``EdgeClient/Authorization/AccessToken/validate(token:simpleCheck:)``
- ``EdgeClient/Authorization/AccessToken/validate(token:simpleCheck:)``
- ``EdgeClient/Authorization/AccessToken/valueFrom(key:)``

## EdgeClient/Document
- ``EdgeClient/Document/filenameExtensionFor(type:)``
- ``EdgeClient/Document/filenameExtentionFor(mimeType:)``
- ``EdgeClient/Document/mimeTypeFor(filenameExtension:)``
- ``EdgeClient/Document/mimeTypeFor(type:)``
- ``EdgeClient/Document/uttypeFor(filenameExtension:)``
- ``EdgeClient/Document/uttypeFor(mimeType:)``


## EdgeClient/Log
- ``EdgeClient/Log/log(level:function:line:items:module:marker:)``
- ``EdgeClient/Log/logDebug(function:line:items:module:marker:)``
- ``EdgeClient/Log/logError(function:line:items:module:marker:)``
- ``EdgeClient/Log/logFault(function:line:items:module:marker:)``
- ``EdgeClient/Log/logInfo(function:line:items:module:marker:)``
- ``EdgeClient/Log/loggingLevel(module:)``
- ``EdgeClient/Log/loggingPrivacy(module:)``


## EdgeClient/Microservice
- ``EdgeClient/Microservice/basePath()``
- ``EdgeClient/Microservice/call(config:)``
- ``EdgeClient/Microservice/call(config:type:)``
- ``EdgeClient/Microservice/callStream(config:streamHandler:requestHandler:)``
- ``EdgeClient/Microservice/callStream(config:type:streamHandler:requestHandler:)``
- ``EdgeClient/Microservice/callStreamSSE(config:streamHandler:requestHandler:)``
- ``EdgeClient/Microservice/fullPathUrl()``
- ``EdgeClient/Microservice/fullPathUrl(withEndpoint:)``
- ``EdgeClient/Microservice/expectedDeployedBasePath(path:clientId:)``
- ``EdgeClient/Microservice/expectedDeployedImageId(imageName:clientId:)``
- ``EdgeClient/Microservice/expectedDeployedContainerId(containerName:clientId:)``
- ``EdgeClient/Microservice/preferredBasePath(path:)``
- ``EdgeClient/Microservice/preferredConfig(imageName:containerName:basePath:edgeEngineFullPathUrl:clientId:envVariables:signatureKey:ownerCode:)``
- ``EdgeClient/Microservice/preferredContainerName(name:)``
- ``EdgeClient/Microservice/preferredImageName(name:)``

## EdgeClient/Microservice/Container
- ``EdgeClient/Microservice/Container/basePath()

## EdgeClient/Microservice/Request
- ``EdgeClient/Microservice/Request/microserviceRequest(url:method:httpBody:microservice:authorization:httpHeaders:timeoutInterval:cachePolicy:simpleCheck:)``


## EdgeClient/Node
- ``EdgeClient/Node/effectiveUrl()``
- ``EdgeClient/Node/preferredNodeName()``


## EdgeClient/Request
- ``EdgeClient/Request/downloadContent(sourceUrl:destinationFileUrl:progressHandler:)``
- ``EdgeClient/Request/downloadImageContent(sourceUrl:)``
- ``EdgeClient/Request/exportVideo(session:outputURL:outFileType:)``
- ``EdgeClient/Request/uploadContent(sourceFileUrl:destinationUrl:mimeType:progressHandler:)``
- ``EdgeClient/Request/authorizedRequest(url:method:authorization:httpHeaders:httpBody:contentType:)``
- ``EdgeClient/Request/call(config:)``
- ``EdgeClient/Request/call(config:type:)``
- ``EdgeClient/Request/decode(_:from:)``

## EdgeClient/Request/URLComponentsBuilder
- ``EdgeClient/Request/URLComponentsBuilder/append(path:)``
- ``EdgeClient/Request/URLComponentsBuilder/create()``
- ``EdgeClient/Request/URLComponentsBuilder/set(fragment:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(host:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(password:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(path:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(port:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(query:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(scheme:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(queryItems:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(scheme:host:port:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(scheme:host:port:path:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(service:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(user:)``


## EdgeClient/Service
- ``EdgeClient/Service/healthCheck()``
- ``EdgeClient/Service/urlComponents()``
- ``EdgeClient/Service/versionCheck(requireMatch:)``


## EdgeEngineClient protocol
    
Provides edgeEngine controls and vendors the actual edgeEngine binary into the project.

> **To enable EdgeEngineClient** protocol API in the project, add [EdgeEngineDeveloper](https://github.com/mimikgit/cocoapod-EdgeEngineDeveloper) or [EdgeEngine](https://github.com/mimikgit/cocoapod-EdgeEngine) to the `Podfile`.

- ``EdgeEngineClient/startEdgeEngine(parameters:)``
- ``EdgeEngineClient/stopEdgeEngine()``
- ``EdgeEngineClient/restartEdgeEngine()``
- ``EdgeEngineClient/resetEdgeEngine()``
- ``EdgeEngineClient/edgeEngineIsRunning()``
- ``EdgeEngineClient/edgeEngineLifecycleIsManaged()``
- ``EdgeEngineClient/edgeEngineParameters()``
- ``EdgeEngineClient/manageEdgeEngineLifecycle(manage:)``
- ``EdgeEngineClient/expectedEdgeEngineVersion()``
- ``EdgeEngineClient/setCustomPort(number:)``

## mimik client libraries

Explore all mimik client libraries [available on Github](https://github.com/search?q=cocoapod-Edge).

Cocoapod sets:

* [EdgeClientLibraryDeveloper = (EdgeCore + EdgeEngineDeveloper)](https://github.com/mimikgit/cocoapod-EdgeClientLibraryDeveloper)
* [EdgeClientLibrary = (EdgeCore + EdgeEngine)](https://github.com/mimikgit/cocoapod-EdgeClientLibrary)
 
Cocoapod individual pods:
 
* [EdgeCore](https://github.com/mimikgit/cocoapod-EdgeCore)
* [EdgeEngineDeveloper](https://github.com/mimikgit/cocoapod-EdgeEngineDeveloper)
* [EdgeEngine](https://github.com/mimikgit/cocoapod-EdgeEngine)
* [EdgeService](https://github.com/mimikgit/cocoapod-EdgeService)


## Author

[mimik Technology, Inc.](https://mimik.com)

More details about how the edgeEngine platform revolutionizes computing with the hybrid-cloud approach are at [mimik Developer Documentation](https://devdocs.mimik.com).


## License

Developers can get their developer edge license by following this [tutorial](https://devdocs.mimik.com/tutorials/02-index).

For details about a full edge license please contact [mimik support](https://mimik.com/contact-us/).
