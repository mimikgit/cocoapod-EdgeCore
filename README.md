# mimik Client Library

The **mimik Client Library** provides a programmatic interface for the mim OE Runtime (formerly edgeEngine), enabling its integration into iOS projects.

## Overview

The **mimik Client Library** enables developers to interact with the mim OE Runtime (formerly known as edgeEngine), providing access to mobile device clusters, on-device RESTful API microservices, and optional integration with mimik AI components.

It offers APIs for setting up the runtime, authenticating developers, deploying edge microservices, integrating with [mimik ai](https://devdocs.mimik.com/tutorials/02-submenu/02-submenu/01-index) and more.

## mimik Client Library cocoapods

Bundle configurations: Developers can choose from new bundling options for more tailored deployments, with the flexibility to include or exclude the AI Runtime. Integrate mim OE into your project based on your application’s needs, selecting whether to include the AI Runtime as part of the integration or not.

* [EdgeCore](https://github.com/mimikgit/cocoapod-EdgeCore) (required)
* [mim-OE-ai-SE-iOS-developer](https://github.com/mimikgit/cocoapod-mim-OE-ai-SE-iOS-developer) (with AI Runtime)
* [mim-OE-SE-iOS-developer](https://github.com/mimikgit/cocoapod-mim-OE-SE-iOS-developer) (no AI)
* [EdgeService](https://github.com/mimikgit/cocoapod-EdgeService) (optional)

Generally speaking, developers only need to add the **`mim-OE-ai-SE-iOS-developer`** and **EdgeCore** cocoapods to their projects.


## Supported Platforms, Targets
* `iOS Devices running iOS 16+`
* `iOS Simulators running iOS 16+`
* `iOS Mac Catalyst running macOS 14.0`


## Requirements
```
iOS 16.0+
```

## Installation

To get started, simply incorporate a configuration such as this to your Podfile:


```swift
platform :ios, '16.0'
source 'https://github.com/CocoaPods/Specs.git'
source 'https://github.com/mimikgit/cocoapod-edge-specs.git'

use_frameworks!
inhibit_all_warnings!

def mimik
  pod 'EdgeCore'
  pod 'mim-OE-ai-SE-iOS-developer'
end

target '{target}' do
  mimik()
end

post_install do |installer|
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      config.build_settings['VALID_ARCHS'] = '$(ARCHS_STANDARD_64_BIT)'
      config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = '16.0'
      config.build_settings['BUILD_LIBRARY_FOR_DISTRIBUTION'] = 'YES'
    end
  end
end
```

> **_NOTE:_** Developers can get their **mim OE (Edge)** for initializing [mim-OE-ai-SE-iOS-developer](https://github.com/mimikgit/cocoapod-mim-OE-ai-SE-iOS-developer) at the [mimik developer console](https://developer.mimik.com/console).

> **_NOTE:_** Enterprise project developers can request an **enterprise mim OE (Edge) license** from [mimik support](https://developer.mimik.com/support/).


## Documentation

`EdgeCore/EdgeClient` API reference documentation is available [here](https://mimikgit.github.io/cocoapod-EdgeCore/documentation/edgecore/edgeclient), as well as in Xcode, where it is included as built-in documentation for all methods and structs.

`EdgeEngineClient` protocol API reference documentation is accessible from [here](https://mimikgit.github.io/cocoapod-EdgeCore/documentation/edgecore/edgeengineclient).

`EdgeService/EdgeServiceClient` API reference documentation can be found [here](https://mimikgit.github.io/cocoapod-EdgeService/documentation/edgeservice/).


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

- ``EdgeClient/deployUseCase(accessToken:config:dynamicConfig:)``
- ``EdgeClient/deployUseCase(accessToken:configUrl:dynamicConfig:)``
- ``EdgeClient/deployMicroservice(edgeEngineAccessToken:config:imageTarPath:)``
- ``EdgeClient/deployImage(accessToken:imageTarPath:)``
- ``EdgeClient/deployContainer(accessToken:config:)``
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

- ``EdgeClient/integrateAI(accessToken:apiKey:config:model:downloadHandler:requestHandler:)``
- ``EdgeClient/integrateAI(accessToken:apiKey:configUrl:model:downloadHandler:requestHandler:)``
- ``EdgeClient/downloadAI(model:accessToken:apiKey:useCase:downloadHandler:requestHandler:)``
- ``EdgeClient/chatAI(request:requestHandler:)``
- ``EdgeClient/chatAI(request:streamHandler:requestHandler:)``
- ``EdgeClient/aiModels(accessToken:apiKey:useCase:)``
- ``EdgeClient/aiModel(id:accessToken:apiKey:useCase:)``
- ``EdgeClient/deleteAIModel(id:accessToken:apiKey:useCase:)``
- ``EdgeClient/warmUpAI(request:)``


## EdgeClient/Authorization/AccessToken

- ``EdgeClient/Authorization/AccessToken/clientId(token:)``
- ``EdgeClient/Authorization/AccessToken/decodeToJWT(token:)``
- ``EdgeClient/Authorization/AccessToken/decodeToJson(token:)``
- ``EdgeClient/Authorization/AccessToken/expiresIn(token:)``
- ``EdgeClient/Authorization/AccessToken/expiresIn(token:)``
- ``EdgeClient/Authorization/AccessToken/subscriber(token:)``
- ``EdgeClient/Authorization/AccessToken/validate(token:)``
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
- ``EdgeClient/Microservice/call(config:requestHandler:)``
- ``EdgeClient/Microservice/call(config:type:requestHandler:)``
- ``EdgeClient/Microservice/callStream(config:streamHandler:requestHandler:)``
- ``EdgeClient/Microservice/callStream(config:type:streamHandler:requestHandler:)``
- ``EdgeClient/Microservice/callStreamSSE(config:streamHandler:requestHandler:)``
- ``EdgeClient/Microservice/urlComponents()``
- ``EdgeClient/Microservice/urlComponents(withEndpoint:)``
- ``EdgeClient/Microservice/expectedDeployedBasePath(path:clientId:)``
- ``EdgeClient/Microservice/expectedDeployedImageId(imageName:clientId:)``
- ``EdgeClient/Microservice/expectedDeployedContainerId(containerName:clientId:)``
- ``EdgeClient/Microservice/preferredBasePath(path:)``
- ``EdgeClient/Microservice/preferredConfig(imageName:containerName:basePath:edgeEngineFullPathUrl:clientId:envVariables:signatureKey:ownerCode:)``
- ``EdgeClient/Microservice/preferredContainerName(name:)``
- ``EdgeClient/Microservice/preferredImageName(name:)``

## EdgeClient/Microservice/Container
- ``EdgeClient/Microservice/Container/basePath()``

## EdgeClient/Microservice/Request
- ``EdgeClient/Microservice/Request/microserviceRequest(microservice:path:method:queryItems:authorization:httpBody:httpHeaders:timeoutInterval:cachePolicy:)``


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
- ``EdgeClient/Request/URLComponentsBuilder/create()``
- ``EdgeClient/Request/URLComponentsBuilder/set(components:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(scheme:host:port:path:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(scheme:host:port:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(scheme:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(host:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(password:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(path:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(port:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(query:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(queryItems:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(user:)``
- ``EdgeClient/Request/URLComponentsBuilder/set(fragment:)``
- ``EdgeClient/Request/URLComponentsBuilder/append(path:)``


## EdgeClient/Service
- ``EdgeClient/Service/healthCheck()``
- ``EdgeClient/Service/urlComponents()``
- ``EdgeClient/Service/versionCheck(requireMatch:)``


## EdgeEngineClient protocol
    
Provides mim OE (edgeEngine) controls and vendors the actual mim OE (edgeEngine) binary into the project.

> **To enable EdgeEngineClient** protocol API in the project, add [mim-OE-ai-SE-iOS-developer](https://github.com/mimikgit/cocoapod-mim-OE-ai-SE-iOS-developer) to your `Podfile`.

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


## Tutorials

After installation, try the following tutorials:

- [Understanding the mimik Client Library for iOS](https://devdocs.mimik.com/key-concepts/10-index).
- [Creating a Simple iOS Application that Uses an edge microservice](https://devdocs.mimik.com/tutorials/01-submenu/02-submenu/01-index).
- [Integrating the mimik Client Library into an iOS project](https://devdocs.mimik.com/tutorials/01-submenu/02-submenu/02-index).
- [Working with mimOE in an iOS project](https://devdocs.mimik.com/tutorials/01-submenu/02-submenu/03-index).
- [Working with edge microservices in an iOS project](https://devdocs.mimik.com/tutorials/01-submenu/02-submenu/04-index).


## Author

[mimik Technology, Inc.](https://mimik.com)

More details about how the edgeEngine platform revolutionizes computing with the hybrid-cloud approach are at [mimik Developer Documentation](https://devdocs.mimik.com).


## License

Developers can get their mim OE (Edge) license for initializing [mim-OE-ai-SE-iOS-developer](https://github.com/mimikgit/cocoapod-mim-OE-ai-SE-iOS-developer) at the [mimik developer console](https://developer.mimik.com/console).

For details about an enterprise mim OE (Edge) license please contact [mimik support](https://mimik.com/contact-us/).
