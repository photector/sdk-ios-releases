# Photector SDK for iOS

## Introduction

Before making use of the Photector SDK it's important to understand some key concepts / terminology, in short order:
- An event is a data set that contains some meta data (e.g. a location, a description, a list of tags, etc...) and up to 20 records. 
- A record contains at the very least a photo.

The Photector SDK provides an easy way to store events on the Photector block chain. 

## Requirements

The SDK supports at the very minimum iOS 11. In order to create events both location services and access to the camera is required. An access token is also required and can be obtained through [Photector](https://photector.com).

## Installation

The Photector iOS SDK is available through [CocoaPods](https://cocoapods.org). The Photector SDK is not available through the public cocoapods repository. Instead one has to add the Photector private repo as such:
```bash
$ pod repo add Photector https://github.com/photector/Podspecs.git
```

To install the SDK, simply add the following lines add the top of your Podfile:
```ruby
source 'https://github.com/photector/Podspecs.git'
```

Then add the Photector pod to your desired target, e.g.:
```ruby
target 'MyApp' do
    pod 'Photector'
end

```

## Implementation Guide

### Update info.plist

Update your apps' `info.plist` file to include the `NSCameraUsageDescription` and `NSCameraUsageDescription` keys. 

### Initialize Photector

In order to implement the SDK, first initialize the SDK as early as possible in your apps' lifecycle. We recommend initializing Photector in your app delegate after the app has launched:
```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
    // Override point for customization after application launch.
    
    ...
    
    do {
        let clientId = // your client id as provided by Photector
        let clientSecret = // your client secret as provided by Photector
        let accessToken = // your access token as provided by Photector
        try Photector.shared.configure(clientId: clientId, clientSecret: clientSecret, accessToken: accessToken)
    } catch let error {
        print("error: \(error)")
    }

    return true
}
```

### Create An Event

In order to create an event, just call the `createEvent()` method:
```swift
let description: String? = null // Optionally add a description
let tags: [String] = [] // Optionally add a list of tags
do {
    try Photector.shared.createEvent(description: description, tags: tags)
} catch let error {
    print("error: \(error)")
}
```

### List Events

In order to retrieve a list of previously stored events, call the `getEvents()` method:
```swift
let force = false // If force is true, cached event data will be ignored
Photector.shared.getEvents(force: force, completionHandler: { (events, error) in
    // Do something with the events on success or display the error on failure
})
```

### Handle SDK Notifications

The SDK provides notifications on some Event lifecycle state changes:
- `didCreateEvent()`: Called after an event is created, but before the upload has started
- `didStartUpload()`: Called when an event upload has started
- `didChangeUploadProgress()`: Called when an event upload's progress is changed
- `didFinishUpload`: Called when an event upload has completed

Implement the `PhotectorDelegate` interface to handle the above notifications. Subscribe to receive notifications and unsubscribe when you are no longer interested in receiving those notifications:

```swift
// To subscribe ...
Photector.shared.addListener(this);

// To unsubscribe ...
Photector.shared.removeListener(this);
```
