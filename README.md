# iOS Command CheatSheet

This is a console command cheat sheet for iOS developers.

Command CheetSheet for iOS Developer

 - Certificates / Provisioning Profiles
 - CocoaPods
 - Carthage
 - Swift Package Manager
 - Fastlane
 - Swift Compiler
 - SwiftLint
 - Xcode
 - Simulator
 - Homebrew
 - .gitignore
 - Firebase

## Certificates / Provisioning Profiles

Create Private Key
```bash
openssl genrsa -out private.key 2048
```

Create CSR
```bash
openssl req -new -key private.key -out CertificateSigningRequest.certSigningRequest -subj "/emailAddress=[YourMailAddress], CN=[CommonName], C=JP"
```

Print certificates in keychain
```bash
security find-identity -p codesigning -v
```

Print provisioning profiles (〜Xcode 15)
```bash
ls ~/Library/MobileDevice/Provisioning\ Profiles/
```

Print provisioning profiles (Xcode 16〜)
```bash
ls ~/Library/Developer/Xcode/UserData/Provisioning\ Profiles/
```

## CocoaPods

Install 
```bash
sudo gem install cocoapods
```

Delete Pods
```bash
rm -rf Pods
```

Delete Pods
```bash
rm Podfile
```

Delete Pods
```bash
rm Podfile.lock
```

Init Podfile
```bash
pod init
```

Install libraries
```bash
pod install
```

Update libraries
```bash
pod update
```

Create PodSpec
```bash
pod spec create pod_name
```

Lint PodSpec
```bash
pod lib lint
```

Create your trunk account 
```bash
pod trunk register mail_address 'your_name'
```

Publish pods
```bash
pod trunk push pod_name.podspec
```

Delete caches
```bash
pod cache clean --all
```

Delete caches
```bash
rm -rf ~/Library/Caches/CocoaPods/
```

## Carthage

Install
```bash
brew install Carthage
```

Install Libraries
```bash
carthage bootstrap --platform iOS --cache-builds
```

Update Libraries
```bash
carthage update --platform iOS --cache-builds
```

Create XCFileList
```bash
ls Carthage/Build/iOS | grep -E .+framework$ | sed 's/.*/$(SRCROOT)\/Carthage\/Build\/iOS\/&/' > Carthage.xcfilelist
```

Build
```bash
carthage build --no-skip-current 
```

Delete Caches
```bash
rm -rf ~/Library/Caches/org.carthage.CarthageKit 
```

Delete Caches
```bash
rm -rf ~/Library/Caches/carthage
```

## Swift Package Manager

Delete Caches
```bash
rm -rf ~/Library/Caches/org.swift.swiftpm
```

## Fastlane

Install
```bash
brew cask install fastlane
```

Init fastlane
```bash
fastlane init
```

Download Metadata
```bash
fastlane deliver download_metadata --force
```

Upload Metadata
```bash
fastlane deliver --force --skip_screenshots --skip_binary_upload --skip_app_version_update --skip_metadata false
```

Download Screenshot
```bash
fastlane deliver download_screenshots --force
```

Create Screenshot
```bash
fastlane frameit(path: './fastlane/screenshots/', white: false)
```

Upload Screenshot
```bash
fastlane deliver --force --skip_binary_upload --skip_metadata --skip_app_version_update --overwrite_screenshots --skip_screenshots false
```

Upload Binary
```bash
fastlane deliver --force --skip_screenshots --skip_metadata --skip_app_version_update
```

Submit for AppStore review
```bash
fastlane deliver --force --skip_screenshots --skip_metadata --skip_app_version_update  --skip_binary_upload --automatic_release --submit_for_review
```

Delete session cookie
```bash
rm ~/.fastlane/spaceship/**/cookie
```

## Swift Compiler
Parse and type-check input file(s) and pretty print AST(s)
```bash
swiftc -print-ast file
```

Parse and type-check input file(s) and dump AST(s)
```bash
swiftc -dump-ast file
```

## SwiftLint

Install
```bash
brew install swiftlint
```

Lint
```bash
swiftlint
```

AutoCorrect
```bash
swiftlint autocorrect
```

Print Docs
```bash
swiftlint generate-docs
```

Copy All Opt-In Rules
```bash
swiftlint rules | awk -F "|" '$3 ~ "yes" { print $2 }' | tr -d ' ' | sed 's/^/  - /' | pbcopy
```

Delete Caches
```bash
rm -rf ~/Library/Caches/SwiftLint
```

## Xcode

Switch the developer path to the specified Xcode application
```bash
sudo xcode-select --switch /Applications/Xcode.app
```

Check the number of cores on the system
```bash
system_profiler SPHardwareDataType | grep "Cores"
```

Set the number to use for building
```bash
defaults write com.apple.dt.Xcode IDEBuildOperationMaxNumberOfConcurrentCompileTasks [number_of_cores]
```

Enable Xcode to show the build duration
```bash
defaults write com.apple.dt.Xcode ShowBuildOperationDuration YES
```

Print out the targets, configurations, and schemes in the current project
```bash
xcodebuild -list
```

Print out the available SDKs that Xcode can build against
```bash
xcodebuild -showsdks
```

Clean the disk by removing old build archives to save space
```bash
rm -rf ~/Library/Developer/Xcode/Archives
```

Remove iOS Device Support data to save disk space
```bash
rm -rf ~/Library/Developer/Xcode/iOS DeviceSupport/
```

Remove old iPhone Simulator data
```bash
rm -rf ~/Library/Application Support/iPhone Simulator
```

Clean build by deleting the build cache
```bash
xcodebuild -alltargets clean
```

Remove Xcode's derived data to clear any cached build settings or intermediates
```bash
rm -rf ~/Library/Developer/Xcode/DerivedData/
```

Clear Xcode's cache to ensure a clean build environment
```bash
rm -rf ~/Library/Caches/com.apple.dt.Xcode/
```

Remove cache files related to iOS Device Support
```bash
rm -rf ~/Library/Developer/Xcode/iOS\ DeviceSupport/*/Symbols/System/Library/Caches
```

Delete Xcode's cache files
```bash
xcrun --kill-cache
```

Terminate the Xcode build service to stop any ongoing build processes
```bash
killall XCBBuildService
```

Remove Clang module cache to prevent potential conflicts or outdated modules
```bash
rm -rf "$(getconf DARWIN_USER_CACHE_DIR)/org.llvm.clang/ModuleCache"
```

Remove Clang module cache to prevent potential conflicts or outdated modules
```bash
rm -rf "$(getconf DARWIN_USER_CACHE_DIR)/org.llvm.clang.$(whoami)/ModuleCache"
```

Remove temporary Clang module cache
```bash
rm -rf "$TMPDIR/../C/clang/ModuleCache"
```

## Simulator

List all available devices, device types, runtimes, and device pairs
```bash
xcrun simctl list
```

List all available device types that can be created
```bash
xcrun simctl list devicetypes
```

List only the devices that are currently booted
```bash
xcrun simctl list | grep Booted
```

Open a URL in a device with the specified UUID
```bash
xcrun simctl openurl <UUID> <URL scheme>
```

Open a URL in the currently booted device
```bash
xcrun simctl openurl booted <URL scheme>
```

Grant the Photos app permission for the booted device using the specified bundle ID
```bash
xcrun simctl privacy booted grant photos <Bundle ID>
```

Revoke the Photos app permission for the booted device using the specified bundle ID
```bash
xcrun simctl privacy booted revoke photos <Bundle ID>
```

Reset the privacy permissions for all apps on the booted device using the specified bundle ID
```bash
xcrun simctl privacy booted reset all <Bundle ID>
```

Send a simulated push notification to the booted device from the specified payload file
```bash
xcrun simctl push booted payload.json
```

Override the status bar display for the booted device to a specific time, cellular bars, network type, and Wi-Fi mode
```bash
xcrun simctl status_bar booted override --time 12:01 --cellularBars 1 --dataNetwork 3g --wifiMode failed
```

Clear any status bar overrides and revert to the device's default status bar settings
```bash
xcrun simctl status_bar booted clear
```

Add a root certificate to the booted device's keychain from the specified file
```bash
xcrun simctl keychain booted add-root-cert myCA.pem
```

Record a video of the booted device's screen and save it to a file
```bash
xcrun simctl io booted recordVideo video.mp4
```

Record a video of the booted device's screen with the specified codec and ignore the mask
```bash
xcrun simctl io booted recordVideo --codec h264 --mask ignored video.mp4
```

Record a video of an externally displayed screen of the booted device
```bash
xcrun simctl io booted recordVideo --display external video.mp4
```

Paste the contents of the device's clipboard to the host machine
```bash
xcrun simctl pbpaste booted
```

Synchronize the clipboard content from the host to the booted device
```bash
xcrun simctl pbsync host booted
```

Get information about the booted device's clipboard
```bash
xcrun simctl pbinfo booted
```

Send a simulated APNS push notification to the booted device using the specified bundle ID and payload
```bash
xcrun simctl push booted <Bundle ID> payload.apns
```

Delete all simulators that are set to show in the device previews
```bash
xcrun simctl --set previews delete all
```

Erase all content and settings from all simulators
```bash
xcrun simctl erase all
```

## Homebrew

Install
```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Delete Caches
```bash
rm -rf ~/Library/Caches/Homebrew
```

Delete Caches
```bash
brew cleanup -s
```

Delete Caches
```bash
rm -rf $(brew --cache)
```

## .gitignore

Create .gitignore
```bash
brew install gibo
```

Create .gitignore
```bash
gibo dump Swift Xcode >> .gitignore
```

Quick Commit .gitignore
```bash
git add .gitignore
```

Quick Commit .gitignore
```bash
git commit -m "add .gitignore"
```

Quick Commit Igonored Files
```bash
git rm -r --cached .
```

Quick Commit Igonored Files
```bash
git add .
```

Quick Commit Igonored Files
```bash
git commit -m "rm ignore files"
```

## Firebase

Find dSYM UUID
```bash
find ./ -name "*.dSYM" -maxdepth 2 -type d -print0 \
| xargs -0 -I{} dwarfdump --uuid "{}"
```

Upload dSYM
```bash
./Pods/FirebaseCrashlytics/upload-symbols -gsp GoogleService-Info.plist -p ios ~/Downloads/appDsyms.zip
```

Upload dSYM
```bash
Scripts/upload-symbols -gsp GoogleService-Info.plist -p ios ~/Downloads/appDsyms*.zip
```

Upload dSYM
```bash
./Frameworks/Firebase/FirebaseCrashlytics/upload-symbols -gsp GoogleService-Info.plist -p ios ~/Downloads/appDsyms*.zip
```
