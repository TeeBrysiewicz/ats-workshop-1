# All Things Swift
## Workshop #1 - Scratch, Pods, Http Requests
---
Summary: This workshop will teach you how to start a iOS application from scratch using Swift 3, how to install Swift packages, and how to make HTTP requests to a 3rd party API.

Requirements: Mac computer with Xcode up-to-date

### Step 1: Starting The Project
* Open Xcode
* Create Single View Application
* Edit .plist
	* App Transport Security Settings
		* Allow Arbitrary Loads: YES

### Step 2: Pods
* Create Podfile

```
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '9.0'
use_frameworks!

target 'weather-app' do


end
```
* Add Pods

```
  pod 'Alamofire', '~>4.3'

```
* Install Pods

```
run: pod install
```

### Step 3: Make HTTP Request
* Import Alamofire
* Add API Key
* Alamofire Request

```
Alamofire.request("http://api.openweathermap.org/data/2.5/weather?q=chicago",
                  parameters: ["apiid": apiKey],
                  headers: ["X-API-KEY" : apiKey]
                  ).responseJSON { response in
            print("Original URL:", response.request as Any)  // original URL request
            print("HTTP URL Response:", response.response as Any) // HTTP URL response
            print("Sever Data:", response.data as Any)     // server data
            print("Result:", response.result)   // result of response serialization
            
            if let JSON = response.result.value {
                print("JSON: \(JSON)")
            }
        }

``` 

### Step 4: Populate 
* Create Labels
	* Constrain Labels
	* Format Labels
* Connect Labels
* Populate Labels

```
    print("JSON: \(JSON)")
                
    print("City Name: \(JSON["name"] as! String)")
    self.city_name.text = JSON["name"] as! String
                
                
    print("Temp: \(JSON["main"]?["temp"] as! Float)")
    self.temp.text = String(JSON["main"]?["temp"] as! Float)
                
                
    print("Weather: \(JSON["weather"] as! [[String:AnyObject]])")
    let weather = JSON["weather"] as! [[String:AnyObject]]
    print("Description: \(weather[0]["description"] as! String)")
    self.weather.text = weather[0]["description"] as! String
```

