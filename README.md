# CheatSheet


## Git

```bash
# Download .gitignore for iOS (https://gist.github.com/shtnkgm/dfe0a0478a15de11ce93ca6f39223cd5)
wget https://bit.ly/shtnkgmgi2 -O .gitignore

# Quick Fix Push
git add .;git commit -m "fix";git push
```

## Dependency Manager

```bash
pod install
pod update

carthage bootstrap --platform iOS --cache-builds
carthage update --platform iOS --cache-builds

# Create XCFileList
ls Carthage/Build/iOS | grep -E .+framework$ | sed 's/.*/$(SRCROOT)\/Carthage\/Build\/iOS\/&/' > CarthageInput.xcfilelist 
```

## Fastlane

```bash
# Download Metadata
fastlane deliver download_metadata　

# Upload Metadata
fastlane deliver --force --skip_screenshots --skip_binary_upload --skip_app_version_update

# Download Screenshot
fastlane deliver download_screenshots

# Create Screenshot
fastlane frameit(path: './fastlane/screenshots/', white: false)
fastlane setframe

# Upload Screenshot
fastlane deliver --force --skip_binary_upload --skip_metadata --skip_app_version_update --overwrite_screenshots

# Upload Binary
fastlane deliver --force --skip_screenshots --skip_metadata --skip_app_version_update

# Submit for Review
fastlane deliver --force --skip_screenshots --skip_metadata --skip_app_version_update  --skip_binary_upload --automatic_release --submit_for_review
```

## Create Gif
```bash
ffmpeg -i sample_01.mov -vf scale=400:-1 -r 20 sample_01.gif
```


