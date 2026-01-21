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

```bash
# Create Private Key
openssl genrsa -out private.key 2048

# Create CSR
openssl req -new -key private.key -out CertificateSigningRequest.certSigningRequest -subj "/emailAddress=[YourMailAddress], CN=[CommonName], C=JP"

# Print certificates in keychain
security find-identity -p codesigning -v

# Print provisioning profiles
# 〜Xcode 15
ls ~/Library/MobileDevice/Provisioning\ Profiles/
# Xcode 16〜
ls ~/Library/Developer/Xcode/UserData/Provisioning\ Profiles/
```

## CocoaPods

```bash
# Install 
sudo gem install cocoapods

# Delete Pods
rm -rf Pods; rm Podfile; rm Podfile.lock 

# Init Podfile
pod init

# Install libraries
pod install

# Update libraries
pod update

# Create PodSpec
pod spec create pod_name

# Lint PodSpec
pod lib lint

# Create your trunk account 
pod trunk register mail_address 'your_name'

# Publish pods
pod trunk push pod_name.podspec

# Delete caches
pod cache clean --all
rm -rf ~/Library/Caches/CocoaPods/
```

## Carthage

```bash
# Install
brew install Carthage

# Install Libraries
carthage bootstrap --platform iOS --cache-builds

# Update Libraries
carthage update --platform iOS --cache-builds

# Create XCFileList
ls Carthage/Build/iOS | grep -E .+framework$ | sed 's/.*/$(SRCROOT)\/Carthage\/Build\/iOS\/&/' > Carthage.xcfilelist

# Build
carthage build --no-skip-current 

# Delete Caches
rm -rf ~/Library/Caches/org.carthage.CarthageKit 
rm -rf ~/Library/Caches/carthage
```

## Swift Package Manager

```bash
# Delete Caches
rm -rf ~/Library/Caches/org.swift.swiftpm
```

## Fastlane

```bash
# Install
brew cask install fastlane

# Init fastlane
fastlane init

# Download Metadata
fastlane deliver download_metadata --force

# Upload Metadata
fastlane deliver --force --skip_screenshots --skip_binary_upload --skip_app_version_update --skip_metadata false

# Download Screenshot
fastlane deliver download_screenshots --force

# Create Screenshot
fastlane frameit(path: './fastlane/screenshots/', white: false)

# Upload Screenshot
fastlane deliver --force --skip_binary_upload --skip_metadata --skip_app_version_update --overwrite_screenshots --skip_screenshots false

# Upload Binary
fastlane deliver --force --skip_screenshots --skip_metadata --skip_app_version_update

# Submit for AppStore review
fastlane deliver --force --skip_screenshots --skip_metadata --skip_app_version_update  --skip_binary_upload --automatic_release --submit_for_review

# Delete session cookie
rm ~/.fastlane/spaceship/**/cookie
```

## Swift Compiler
```bash
# Parse and type-check input file(s) and pretty print AST(s)
swiftc -print-ast file
# Parse and type-check input file(s) and dump AST(s)
swiftc -dump-ast file
```

## SwiftLint

```bash
# Install
brew install swiftlint

# Lint
swiftlint

# AutoCorrect
swiftlint autocorrect

# Print Docs
swiftlint generate-docs

# Copy All Opt-In Rules
swiftlint rules | awk -F "|" '$3 ~ "yes" { print $2 }' | tr -d ' ' | sed 's/^/  - /' | pbcopy

# Delete Caches
rm -rf ~/Library/Caches/SwiftLint
```

## Xcode

```bash

# Switch the developer path to the specified Xcode application
sudo xcode-select --switch /Applications/Xcode.app

# Check the number of cores on the system and set the number to use for building
system_profiler SPHardwareDataType | grep "Cores"
defaults write com.apple.dt.Xcode IDEBuildOperationMaxNumberOfConcurrentCompileTasks [number_of_cores]

# Enable Xcode to show the build duration
defaults write com.apple.dt.Xcode ShowBuildOperationDuration YES

# Print out the targets, configurations, and schemes in the current project
xcodebuild -list

# Print out the available SDKs that Xcode can build against
xcodebuild -showsdks

# Clean the disk by removing old build archives to save space
rm -rf ~/Library/Developer/Xcode/Archives

# Remove iOS Device Support data to save disk space
rm -rf ~/Library/Developer/Xcode/iOS DeviceSupport/

# Remove old iPhone Simulator data
rm -rf ~/Library/Application Support/iPhone Simulator

# Clean build by deleting the build cache
xcodebuild -alltargets clean

# Remove Xcode's derived data to clear any cached build settings or intermediates
rm -rf ~/Library/Developer/Xcode/DerivedData/

# Clear Xcode's cache to ensure a clean build environment
rm -rf ~/Library/Caches/com.apple.dt.Xcode/

# Remove cache files related to iOS Device Support
rm -rf ~/Library/Developer/Xcode/iOS\ DeviceSupport/*/Symbols/System/Library/Caches

# Delete Xcode's cache files
xcrun --kill-cache

# Terminate the Xcode build service to stop any ongoing build processes
killall XCBBuildService

# Remove Clang module cache to prevent potential conflicts or outdated modules
rm -rf "$(getconf DARWIN_USER_CACHE_DIR)/org.llvm.clang/ModuleCache"
rm -rf "$(getconf DARWIN_USER_CACHE_DIR)/org.llvm.clang.$(whoami)/ModuleCache"

# Remove temporary Clang module cache
rm -rf "$TMPDIR/../C/clang/ModuleCache"
```

## Simulator

```bash
# List all available devices, device types, runtimes, and device pairs
xcrun simctl list

# List all available device types that can be created
xcrun simctl list devicetypes

# List only the devices that are currently booted
xcrun simctl list | grep Booted

# Open a URL in a device with the specified UUID
xcrun simctl openurl <UUID> <URL scheme>

# Open a URL in the currently booted device
xcrun simctl openurl booted <URL scheme>

# Grant the Photos app permission for the booted device using the specified bundle ID
xcrun simctl privacy booted grant photos <Bundle ID>

# Revoke the Photos app permission for the booted device using the specified bundle ID
xcrun simctl privacy booted revoke photos <Bundle ID>

# Reset the privacy permissions for all apps on the booted device using the specified bundle ID
xcrun simctl privacy booted reset all <Bundle ID>

# Send a simulated push notification to the booted device from the specified payload file
xcrun simctl push booted payload.json

# Override the status bar display for the booted device to a specific time, cellular bars, network type, and Wi-Fi mode
xcrun simctl status_bar booted override --time 12:01 --cellularBars 1 --dataNetwork 3g --wifiMode failed

# Clear any status bar overrides and revert to the device's default status bar settings
xcrun simctl status_bar booted clear

# Add a root certificate to the booted device's keychain from the specified file
xcrun simctl keychain booted add-root-cert myCA.pem

# Record a video of the booted device's screen and save it to a file
xcrun simctl io booted recordVideo video.mp4

# Record a video of the booted device's screen with the specified codec and ignore the mask
xcrun simctl io booted recordVideo --codec h264 --mask ignored video.mp4

# Record a video of an externally displayed screen of the booted device
xcrun simctl io booted recordVideo --display external video.mp4

# Paste the contents of the device's clipboard to the host machine
xcrun simctl pbpaste booted

# Synchronize the clipboard content from the host to the booted device
xcrun simctl pbsync host booted

# Get information about the booted device's clipboard
xcrun simctl pbinfo booted

# Send a simulated APNS push notification to the booted device using the specified bundle ID and payload
xcrun simctl push booted <Bundle ID> payload.apns

# Delete all simulators that are set to show in the device previews
xcrun simctl --set previews delete all

# Erase all content and settings from all simulators
xcrun simctl erase all
```

## Homebrew

```bash
# Install
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# Delete Caches
rm -rf ~/Library/Caches/Homebrew
brew cleanup -s
rm -rf $(brew --cache)
```

## .gitignore

```bash
# Create .gitignore
brew install gibo
gibo dump Swift Xcode >> .gitignore

# Quick Commit .gitignore
git add .gitignore;git commit -m "add .gitignore"

# Quick Commit Igonored Files
git rm -r --cached .;git add .;git commit -m "rm ignore files"
```

## Firebase

```bash
# Find dSYM UUID
find ./ -name "*.dSYM" -maxdepth 2 -type d -print0 \
| xargs -0 -I{} dwarfdump --uuid "{}"

# Upload dSYM
./Pods/FirebaseCrashlytics/upload-symbols -gsp GoogleService-Info.plist -p ios ~/Downloads/appDsyms.zip

Scripts/upload-symbols -gsp GoogleService-Info.plist -p ios ~/Downloads/appDsyms*.zip

./Frameworks/Firebase/FirebaseCrashlytics/upload-symbols -gsp GoogleService-Info.plist -p ios ~/Downloads/appDsyms*.zip
```

