# LocationManager
Location Manager is a library written in Swift 3.0 for iOS which handles the location features provided by Apple. It is fairly simple to use where you can just get your current location, current address, custom location and custom address by just a single method call.

#Requirements

iOS 9.0+<br>
Xcode 8.0+<br>
Swift 3.0+

How to use it.<br>
Just add ```LocationManager.swift``` into your project

In order to just get your current Latitude and Longitute

```swift
LocationManager.sharedInstance.getLocation { (location:CLLocation?, error:NSError?) in
            if error != nil {
                print(error?.localizedDescription)
                return
            }
            guard let _ = location else {
                return
            }
            print("Latitude: \((location?.coordinate.latitude)!) Longitude: \((location?.coordinate.longitude)!)")
        }
```

For getting the current address we can call the ```getCurrentReverseGeoCodedLocation``` method

```swift
LocationManager.sharedInstance.getCurrentReverseGeoCodedLocation { (location:CLLocation?, placemark:CLPlacemark?, error:NSError?) in
            
            if error != nil {
                print(error?.localizedDescription)
                return
            }
            guard let _ = location else {
                print("Unable to fetch location")
                return
            }
            //We get the complete placemark and can fetch anything from CLPlacemark
            print(placemark?.addressDictionary?.description)
        }
```

You can also reverse geocode any address just by providing latitude and longitude in a CLLocation object coming from Google/ Apple or by your API.

```swift
let customLocation = CLLocation(latitude: 22.76456, longitude: 77.42323)
        
LocationManager.sharedInstance.getReverseGeoCodedLocation(location: customLocation) { (location:CLLocation?, placemark:CLPlacemark?, error:NSError?) in
            if error != nil {
                print(error?.localizedDescription)
                return
            }
            guard let _ = location else {
                print("Unable to fetch location")
                return
            }
            //We get the complete placemark and can fetch anything from CLPlacemark
            print(placemark?.addressDictionary?.description)
        }
```
We can also modify the amount of time given for the callback while fetching the location. Currenly the default value is 1 second. You can use ```setTimerForLocation``` method.

```swift
LocationManager.sharedInstance.setTimerForLocation(seconds: 2.0)
```
Generally recommend to keep it to 1 second in order to avoid extra delay.

CocoaPods and Carthage support coming soon!!
