# AppiumSetup
Commands and links for installing Appium 

## Basic Setup for iOS/Android platform

Install Xcode (https://stackoverflow.com/questions/10335747/how-to-download-xcode-dmg-or-xip-file).

Terminal commands for tools installation :

Install brew
 
 ```bash
 /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
Install JAVA using brew
 ```bash
 brew cask install java
 brew cask info java
 brew tap caskroom/cask
 /usr/libexec/java_home
```

Install pre required appium stuff 

```bash
brew install node or sudo npm cache clean -f && sudo npm install -g n && sudo n 9.8.0 (https://nodejs.org/en/download/releases/)
brew install libimobiledevice --HEAD
brew install ios-deploy --HEAD
brew install ideviceinstaller --HEAD
brew install carthage --HEAD
npm install -g appium (or ...@specific version)
```

### Setup Android

Install adb using brew
```bash
brew cask install android-platform-tools
```

Android uninstall server from the device :

```bash
adb uninstall io.appium.uiautomator2.server
adb uninstall io.appium.uiautomator2.server.test
adb commands
```
#### Useful Links for Android commands
1. https://www.androidcentral.com/10-basic-terminal-commands-you-should-know
2. adb shell pm list packages - http://adbshell.com/commands/adb-shell-pm-list-packages
3. Pull apk file from device : https://stackoverflow.com/questions/4032960/how-do-i-get-an-apk-file-from-an-android-device

To get information about the name of the package and the first activity that has to be launched for the testing
```
Browse through the SDK folder -> Build-Tools -> Version folder
Open cmd and execute command ./aapt dumb badging "path_to_apk"
Find package (in the beginning of logs) and launchable-activity parameters
```

### Setup iOS

1. Switch to WedDriverAgent folder 
``` bash
/usr/local/lib/node_modules/appium/node_modules/appium-webdriveragent
```
2. Run ./Scripts/bootstrap.sh for fetching dependencies
``` bash
sh Scripts/bootstrap.sh -d
```

3. Add Apple-ID account in Xcode -> Preferences -> Account
4. Download manual profiles
5. Switch to WebDriverAgentRunner target in project settings
6. Select your account in Sighing (Signing Certificate will be created)
7. Run WebDriverAgentRunner on real device

Certificates explanation
https://medium.com/ios-os-x-development/ios-code-signing-provisioning-in-a-nutshell-d5b247760bef

#### Resolution for 'xcodebuild failed with code 65'

1. Clear DeriverData : 
```
rm -f /Users/$USER/Library/Developer/Xcode/DerivedData
```
2. Open the WebDriverAgent.xcodeproj
3. Select 'Targets' -> 'WebDriverAgentRunner'
4. Open 'Build Phases' -> 'Copy frameworks'
5. Click '+' -> add 'RoutingHTTPServer' -> add 'YYCache.framework'
 https://github.com/facebook/WebDriverAgent/issues/902

#### XCode version switching command
```
sudo xcode-select --switch /Applications/path_to_xcode
```

#### Example for ~/.bash_profile :
```
export JAVA_HOME="$(/usr/libexec/java_home)"
export ANDROID_HOME=/Users/$USER/Library/Android/sdk
export PATH=${PATH}:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools:$JAVA_HOME$
export PATH=$PATH:/usr/local/bin/
```
