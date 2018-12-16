# iOS CheatSheet
iOSデベロッパー向けのチートシートです。
CheetSheet for iOS Developer

 - Certificates / Provisioning Profiles
 - CocoaPods
 - Carthage
 - Fastlane
 - Create Gif
 - Swift Compiler
 - SwiftLint
 - Xcode
 - HomeBrew
 - Git

## Certificates / Provisioning Profiles

```bash
# print certificates in keychain
security find-identity -p codesigning -v

# print provisioning profiles
ls ~/Library/MobileDevice/Provisioning\ Profiles/
```

## CocoaPods

```bash
# install
sudo gem install cocoapods

# Clear Pods
rm -rf Pods; rm Podfile; rm Podfile.lock 

# Init Pods
pod init

# Install Libraries
pod install

# Update Libraries
pod update

# Create PodSpec
pod spec create pod_name

# Lint PodSpec
pod lib lint

# Create Trunk Account 
pod trunk register mail_address 'your_name'

# Publish Pods
pod trunk push pod_name.podspec

# Delete Caches
pod cache clean --all
```

## Carthage

```bash
# install
brew install Carthage

# Install Libraries
carthage bootstrap --platform iOS --cache-builds

# Update Libraries
carthage update --platform iOS --cache-builds

# Create XCFileList
ls Carthage/Build/iOS | grep -E .+framework$ | sed 's/.*/$(SRCROOT)\/Carthage\/Build\/iOS\/&/' > CarthageInput.xcfilelist

# Build for Check Library
carthage build --no-skip-current 

# Delete Caches
rm -rf ~/Library/Caches/org.carthage.CarthageKit 
rm -rf ~/Library/Caches/carthage
```

## Fastlane

```bash
# install
brew cask install fastlane

# Init fastlane
fastlane init
fastlane add_plugin versioning

# Download Metadata
fastlane deliver download_metadata　 --force

# Upload Metadata
fastlane deliver --force --skip_screenshots --skip_binary_upload --skip_app_version_update

# Download Screenshot
fastlane deliver download_screenshots --force

# Create Screenshot
fastlane frameit(path: './fastlane/screenshots/', white: false)

# Upload Screenshot
fastlane deliver --force --skip_binary_upload --skip_metadata --skip_app_version_update --overwrite_screenshots

# Upload Binary
fastlane deliver --force --skip_screenshots --skip_metadata --skip_app_version_update

# Submit for Review
fastlane deliver --force --skip_screenshots --skip_metadata --skip_app_version_update  --skip_binary_upload --automatic_release --submit_for_review

# Delete Cookie
rm ~/.fastlane/spaceship/**/cookie
```

## Create Gif
```bash
ffmpeg -i sample_01.mov -vf scale=400:-1 -r 20 sample_01.gif
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
# check number of cores, and set number to build
system_profiler SPHardwareDataType | grep "Cores"
defaults write com.apple.dt.Xcode IDEBuildOperationMaxNumberOfConcurrentCompileTasks [number_of_core]

# show build time
defaults write com.apple.dt.Xcode ShowBuildOperationDuration YES

# print targets, configurations, schemes
xcodebuild -list

# print sdks
xcodebuild -showsdks

## Clean
xcodebuild -alltargets clean
rm -rf ~/Library/Developer/Xcode/DerivedData/
rm -rf ~/Library/Caches/com.apple.dt.Xcode/
rm -rf ~/Library/Developer/Xcode/iOS\ DeviceSupport/*/Symbols/System/Library/Caches
rm -rf "$(getconf DARWIN_USER_CACHE_DIR)/org.llvm.clang/ModuleCache"
rm -rf "$(getconf DARWIN_USER_CACHE_DIR)/org.llvm.clang.$(whoami)/ModuleCache"
xcrun --kill-cache
xcrun simctl erase all
```

## HomeBrew

```bash
# install
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# Delete Caches
rm -rf ~/Library/Caches/Homebrew
brew cleanup -s
rm -rf $(brew --cache)
```

## Git

```bash
# Create .gitignore
brew install gibo
gibo dump Swift Xcode >> .gitignore

# Quick Push .gitignore
git add .gitignore;git commit -m "add .gitignore"

# Quick Push Igonored Files
git rm -r --cached .;git add .;git commit -m "rm ignore files"

# Quick Push Fix
git add .;git commit -m "fix";git push
```

