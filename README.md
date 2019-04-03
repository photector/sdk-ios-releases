# Photector iOS SDK releases

This repo contains only the binary releases of the Photector iOS SDK.

To get started with the Photector iOS SDK, perform the following steps:

1. Add the Photector podspec repo to your local cocoapod repos: 
```
$ pod repo add Photector https://github.com/photector/Podspecs.git
```

2. Create a Podfile for your Xcode project with at least the following contents:
```
source 'https://github.com/CocoaPods/Specs.git'
source 'https://github.com/Photector/Podspecs.git'

use_frameworks!

platform :ios, '11.0'

target 'MyApp' do
        pod 'Photector', '1.0.0'
end
```
*__PLEASE NOTE:__ the minimum supported iOS version is 11.0.*

3. Install the pods: 
```
$ pod install
```

For more information on the Photector iOS SDK, read the Photector iOS SDK docs.
