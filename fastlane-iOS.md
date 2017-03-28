# recipe-fastlane-ios
This recipe demonstrates how to ditribute an app to [tesflight](https://developer.apple.com/testflight/) through [fastlane](https://github.com/fastlane/fastlane).  

We'll, first, setup fastlane for our project then setup travi-ci.

## Pre-Requisite
- A [github](https://github.com/) account
- A [travi-ci.org](https://travis-ci.org/) account.
- An [Apple developer account]((https://idmsa.apple.com/IDMSWebAuth/login?appIdKey=891bd3417a7776362562d2197f89480a8547b108fd934911bcbea0110d07f757&path=%2Faccount%2F&rv=1))
- Create your certificate, App ID and provissioning profiles in your [Apple developer account](https://idmsa.apple.com/IDMSWebAuth/login?appIdKey=891bd3417a7776362562d2197f89480a8547b108fd934911bcbea0110d07f757&path=%2Faccount%2F&rv=1)
- Create your app in [iTunesConnect](https://itunesconnect.apple.com/login) in order to distribute to App Store

## fastlane

### Install
You'll find on [fastlane documentation](https://docs.fastlane.tools/getting-started/ios/setup/) all you need to setup fastlane on your Mac.

### Initialize your iOS project with fastlane

You'll need 3 informations in order to initiate your project with fastlane :   
	* Developer account username  
	* App ID  
	* Team ID  

* On project root create a ```fastlane``` directory and an ```Appfile``` in it. Fill in your App ID, apple ID and team ID.
This file define the fastlane default parameters.

```shell
app_identifier "your appid" # The bundle identifier of your app
apple_id "your Apple developer account" # Your Apple email address

team_id "your team id"  # Developer Portal Team ID

# you can even provide different app identifiers, Apple IDs and team names per lane:
# More information: https://github.com/fastlane/fastlane/blob/master/fastlane/docs/Appfile.md
``` 

* Create a FastFile with 2 lanes - `increment` and `upload`.  
* Increment's lane will :
	1. Retrieve last build number uploaded on Testflight
	2. Add 1 to last build number.  
_This lane avoid to change and commit the build number in Xcode each time you need to build._

* Upload's lane will upload the ipa to testflight.


```ruby
# Avoid to recreate the README.md in fastlane Directory
skip_docs

# This is the minimum version number required.
# Update this, if you use features of a newer version
fastlane_version "2.18.3"

default_platform :ios

# Fastfile actions accept additional configuration, but
# don't worry, fastlane will prompt you for required
# info which you can add here later

lane :increment do
	increment_build_number({
  		build_number: latest_testflight_build_number + 1
	})
	end

lane :upload do
	pilot(skip_waiting_for_build_processing: true)
	end
```

You're all set. You can now run 

1. `fastlane increment`, it will incrmeent your build number locally.
2. `fastlane upload`, it will upload the ipa file to testflight. It will ask for you Apple Dev account password.

Proceed to [travis setup](./travis-iOS.md) to automate it.