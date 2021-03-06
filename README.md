# AssetDownloadWrapper
A wrapper to download videos using AVAssetDownloadURLSession.

## About
This is the library that wraps the function of AVAssetDownloadURLSession.
Download the video and cache it to local storage.
## How to implement

- Download the video
```swift
    let url = URL(string: "https://mnmedias.api.telequebec.tv/m3u8/29880.m3u8")!
    let urlAsset = AVURLAsset(url: url)
    let asset = AssetWrapper(urlAsset: urlAsset, assetTitle: "hoge")
    AssetDownloadManager.shared.downloadStream(for: asset) { (result) in
      switch result {
        case .success(let response):
        print(response)
        case .failure(let error):
        print(error)
      }
    }
```

- Load local cache
```swift
    guard let arg = AssetDownloadManager.shared.retrieveLocalAsset(with: "hoge") else {
         return
     }
     let vc = AVPlayerViewController()
     let item = AVPlayerItem(asset: arg.0.urlAsset)
     player.replaceCurrentItem(with: item)
     vc.player = player
     present(vc, animated: true, completion: nil)
```

## Requirements
- Xcode 11.4
- Swift 5.1

## Installation
### [CocoaPods](https://guides.cocoapods.org/using/using-cocoapods.html)
Add the pod AssetDownloadWrapper
```ruby
# Podfile
use_frameworks!
target 'YOUR_TARGET_NAME' do
    pod 'AssetDownloadWrapper'
end
```

```sh
$ pod install
```

### [Carthage](https://github.com/Carthage/Carthage)
Add this to Cartfile
```
git "git@github.com:t-osawa-009/AssetDownloadWrapper.git"
```

```sh
$ carthage update
```

## Reference Resources
- https://blog.foresta.me/posts/swift_hls_download_bug/
- https://developer.apple.com/documentation/avfoundation/media_assets_playback_and_editing/using_avfoundation_to_play_and_persist_http_live_streams
- https://developer.apple.com/library/archive/documentation/AudioVideo/Conceptual/MediaPlaybackGuide/Contents/Resources/en.lproj/HTTPLiveStreaming/HTTPLiveStreaming.html#//apple_ref/doc/uid/TP40016757-CH11-SW1

## CONTRIBUTING
There's still a lot of work to do here. We would love to see you involved. You can find all the details on how to get started in the [Contributing Guide](https://github.com/t-osawa-009/AssetDownloadWrapper/blob/master/CONTRIBUTING.md).

## License
AssetDownloadWrapper is released under the MIT license. See LICENSE for details.
