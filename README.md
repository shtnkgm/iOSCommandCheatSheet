# iOS Command CheatSheet

This is a console command cheat sheet for iOS developers.

Command CheetSheet for iOS Developer

 - Certificates / Provisioning Profiles
 - CocoaPods
 - Carthage
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
ls ~/Library/MobileDevice/Provisioning\ Profiles/
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
# Select developer path
sudo xcode-select --switch /Applications/Xcode.app

# check number of cores, and set number to build
system_profiler SPHardwareDataType | grep "Cores"
defaults write com.apple.dt.Xcode IDEBuildOperationMaxNumberOfConcurrentCompileTasks [number_of_core]

# show build time
defaults write com.apple.dt.Xcode ShowBuildOperationDuration YES

# print targets, configurations, schemes
xcodebuild -list

# print sdks
xcodebuild -showsdks

## Clean for disk
rm -rf ~/Library/Developer/Xcode/Archives
rm -rf ~/Library/Developer/Xcode/iOS DeviceSupport/
rm -rf ~/Library/Application Support/iPhone Simulator

## Delete cache
xcodebuild -alltargets clean
rm -rf ~/Library/Developer/Xcode/DerivedData/
rm -rf ~/Library/Caches/com.apple.dt.Xcode/
rm -rf ~/Library/Developer/Xcode/iOS\ DeviceSupport/*/Symbols/System/Library/Caches
rm -rf "$(getconf DARWIN_USER_CACHE_DIR)/org.llvm.clang/ModuleCache"
rm -rf "$(getconf DARWIN_USER_CACHE_DIR)/org.llvm.clang.$(whoami)/ModuleCache"
xcrun --kill-cache
xcrun simctl erase all
rm -rf "$TMPDIR/../C/clang/ModuleCache"
```

## Simulator

```bash
xcrun simctl list
xcrun simctl list devicetypes
xcrun simctl list | grep Booted
xcrun simctl openurl <UUID> <URL scheme>
xcrun simctl openurl booted <URL scheme>
xcrun simctl privacy booted grant photos <Bundle ID>
xcrun simctl privacy booted revoke photos <Bundle ID>
xcrun simctl privacy reset all
xcrun simctl push booted payload.json
xcrun simctl status_bar booted override --time 12:01 --cellularBars 1 --dataNetwork 3g --wifiMode failed
xcrun simctl status_bar booted clear
xcrun simctl keychain booted add-root-cert myCA.pem
xcrun simctl io booted recordVideo video.mp4
xcrun simctl io booted recordVideo --codec h264 --mask ignored video.mp4
xcrun simctl io booted recordVideo --display external video.mp4
xcrun simctl pbpaste booted
xcrun simctl pbsync host booted
xcrun simctl pbinfo booted
xcrun simctl push booted <Bundle ID> payload.apns
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
# Upload dSYM
./Pods/FirebaseCrashlytics/upload-symbols -gsp GoogleService-Info.plist -p ios ~/Downloads/appDsyms.zip

Scripts/upload-symbols -gsp GoogleService-Info.plist -p ios ~/Downloads/appDsyms*.zip

./Frameworks/Firebase/FirebaseCrashlytics/upload-symbols -gsp GoogleService-Info.plist -p ios ~/Downloads/appDsyms*.zip
```

