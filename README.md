# iOS Command CheatSheet
iOSデベロッパー向けのコマンドチートシートです。

Command CheetSheet for iOS Developer

 - Certificates / Provisioning Profiles
 - CocoaPods
 - Carthage
 - Fastlane
 - ffmpeg
 - Swift Compiler
 - SwiftLint
 - Xcode
 - Homebrew
 - .gitignore

## Certificates / Provisioning Profiles

```bash
# 秘密鍵を作成 / Create Private Key
openssl genrsa -out private.key 2048

# CSRを作成 / Create CSR
openssl req -new -key private.key -out CertificateSigningRequest.certSigningRequest -subj "/emailAddress=[メールアドレス], CN=[コモンネーム], C=JP"

# キーチェーンの証明書一覧を表示 / Print certificates in keychain
security find-identity -p codesigning -v

# ローカルに保存されたプロビジョニングプロファイル一覧を表示 / Print provisioning profiles
ls ~/Library/MobileDevice/Provisioning\ Profiles/
```

## CocoaPods

```bash
# インストール / Install
sudo gem install cocoapods

# Podsの削除 / Delete Pods
rm -rf Pods; rm Podfile; rm Podfile.lock 

# Podfileの初期化 / Init Podfile
pod init

# ライブラリのインストール / Install libraries
pod install

# ライブラリのアップデート / Update Libraries
pod update

# Podspecの初期化 / Create PodSpec
pod spec create pod_name

# Podspecのチェック / Lint PodSpec
pod lib lint

# Trunkアカウントの登録 / Create Trunk Account 
pod trunk register mail_address 'your_name'

# Podsライブラリの公開 / Publish Pods
pod trunk push pod_name.podspec

# キャッシュの削除 / Delete Caches
pod cache clean --all
```

## Carthage

```bash
# インストール / Install
brew install Carthage

# ライブラリのインストール / Install Libraries
carthage bootstrap --platform iOS --cache-builds

# ライブラリのアップデート / Update Libraries
carthage update --platform iOS --cache-builds

# XCFileListの生成 / Create XCFileList
ls Carthage/Build/iOS | grep -E .+framework$ | sed 's/.*/$(SRCROOT)\/Carthage\/Build\/iOS\/&/' > CarthageInput.xcfilelist

# ビルド / Build
carthage build --no-skip-current 

# キャッシュの削除 / Delete Caches
rm -rf ~/Library/Caches/org.carthage.CarthageKit 
rm -rf ~/Library/Caches/carthage
```

## Fastlane

```bash
# インストール / Install
brew cask install fastlane

# 初期設定 / Init fastlane
fastlane init

# メタデータのダウンロード / Download Metadata
fastlane deliver download_metadata　 --force

# メタデータのアップロード / Upload Metadata
fastlane deliver --force --skip_screenshots --skip_binary_upload --skip_app_version_update

# スクリーンショットのダウンロード / Download Screenshot
fastlane deliver download_screenshots --force

# スクリーンショットの生成（frameit） / Create Screenshot
fastlane frameit(path: './fastlane/screenshots/', white: false)

# スクリーンショットのアップロード / Upload Screenshot
fastlane deliver --force --skip_binary_upload --skip_metadata --skip_app_version_update --overwrite_screenshots

# バイナリのアップロード / Upload Binary
fastlane deliver --force --skip_screenshots --skip_metadata --skip_app_version_update

# 自動リリースで申請 / Submit for Review
fastlane deliver --force --skip_screenshots --skip_metadata --skip_app_version_update  --skip_binary_upload --automatic_release --submit_for_review

# セッションクッキーの削除 / Delete Session Cookie
rm ~/.fastlane/spaceship/**/cookie
```

## ffmpeg
```bash
# インストール / Install
brew install ffmpeg

# Gifの生成 / Create Gif
ffmpeg -i sample_01.mov -vf scale=400:-1 -r 20 sample_01.gif
```

## Swift Compiler
```bash
# ASTの整形出力 / Parse and type-check input file(s) and pretty print AST(s)
swiftc -print-ast file
# ASTのダンプ / Parse and type-check input file(s) and dump AST(s)
swiftc -dump-ast file
```

## SwiftLint

```bash
# インストール / Install
brew install swiftlint

# Lint
swiftlint

# 自動修正 / AutoCorrect
swiftlint autocorrect

# ドキュメントの出力 / Print Docs
swiftlint generate-docs

# オプトインルールの全コピー / Copy All Opt-In Rules
swiftlint rules | awk -F "|" '$3 ~ "yes" { print $2 }' | tr -d ' ' | sed 's/^/  - /' | pbcopy

# キャッシュの削除 / Delete Caches
rm -rf ~/Library/Caches/SwiftLint
```

## Xcode

```bash
# コア数を確認してコンパイルに利用するコア数を設定 / check number of cores, and set number to build
system_profiler SPHardwareDataType | grep "Cores"
defaults write com.apple.dt.Xcode IDEBuildOperationMaxNumberOfConcurrentCompileTasks [number_of_core]

# ビルド時間を出力 / show build time
defaults write com.apple.dt.Xcode ShowBuildOperationDuration YES

# targets, configurations, schemes一覧を出力 / print targets, configurations, schemes
xcodebuild -list

# SDK一覧を出力 / print sdks
xcodebuild -showsdks

## ディスク容量削減
rm -rf ~/Library/Developer/Xcode/Archives
rm -rf ~/Library/Developer/Xcode/iOS DeviceSupport/
rm -rf ~/Library/Application Support/iPhone Simulator

## クリーン / Clean
xcodebuild -alltargets clean
rm -rf ~/Library/Developer/Xcode/DerivedData/
rm -rf ~/Library/Caches/com.apple.dt.Xcode/
rm -rf ~/Library/Developer/Xcode/iOS\ DeviceSupport/*/Symbols/System/Library/Caches
rm -rf "$(getconf DARWIN_USER_CACHE_DIR)/org.llvm.clang/ModuleCache"
rm -rf "$(getconf DARWIN_USER_CACHE_DIR)/org.llvm.clang.$(whoami)/ModuleCache"
xcrun --kill-cache
xcrun simctl erase all
```

## Homebrew

```bash
# インストール / Install
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# キャッシュの削除 / Delete Caches
rm -rf ~/Library/Caches/Homebrew
brew cleanup -s
rm -rf $(brew --cache)
```

## .gitignore

```bash
# .gitignoreの生成 / Create .gitignore
brew install gibo
gibo dump Swift Xcode >> .gitignore

# .gitignoreのクイックコミット / Quick Commit .gitignore
git add .gitignore;git commit -m "add .gitignore"

# git管理されないファイルの削除コミット /  Quick Commit Igonored Files
git rm -r --cached .;git add .;git commit -m "rm ignore files"
```

