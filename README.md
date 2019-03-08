# Photector iOS SDK releases

This repo contains only the binary releases of the Photector iOS SDK.

To get started with the Photector iOS SDK, perform the following steps:

1. Add the Photector podspec repo to your local cocoapod repos: 
```
$ pod repo add photector https://github.com/photector/Podspecs.git
```

2. Create a Podfile for your Xcode project with at least the following contents:
```
source 'https://github.com/CocoaPods/Specs.git'
source 'https://github.com/photector/Podspecs.git'

use_frameworks!

platform :ios, '11.0'

target 'PhotectorTest' do
        pod 'Photector', '0.9.0'
end
```

Please note the minimum supported iOS version is 11.0.

3. Install the pods: 
```
$ pod install
```

For more information on the Photector iOS SDK, read the Photector iOS SDK docs.
