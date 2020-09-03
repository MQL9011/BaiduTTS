##Coding仓库地址
https://e.coding.net/billionbook/baiduyuyin_tts/baiduTTS.git

## 百度语音合成TTS离线二次封装
> 百度官方的SDK不支持cocoapods集成,所以就有了这个库. 其中官方的SDK中有个静态库libBaiduSpeechSDK.a比较大有200M+, 用了`git lfs` 才传上来 pod installs时估计也会比较久,请耐心等待.
> APPID,APPKEY,SecretKey这三个请自行去百度云官网上申请,语音TTS是免费的.
我自己主要是将百度SDK做了二次封装,简化了调用方式,并且支持cocoapods集成.


## Installation

```ruby
pod 'BaiduTTS'
```

## How to Use

- 支持 男声, 女声, 语速快慢

```
//初始化
- (void)setUpTTS{
NSString* APP_ID = @"";
NSString* API_KEY = @"";
NSString* SECRET_KEY = @"";
self.tts = [[BaiduTTS alloc]initWithAppID:APP_ID ApiKey:API_KEY SecretKey:SECRET_KEY];
self.tts.delegate = self;
}


/**
开始播放
*/
- (void)playTTS{
self.tts.text = self.tv.text;
[self.tts startSpeech];
}


/**
暂停播放
*/
- (void)pauseTTS{
[self.tts ttsPause];
}


/**
继续播放
*/
- (void)resumeTTS{
[self.tts ttsResume];
}

/**
停止播放
*/
- (void)stopTTS{
[self.tts stopSpeech];
}
```

- 代理回调,其中当前朗读位置可以通过已经朗读的长度来获取

```
#pragma mark TTS代理回调
/**
开始朗读
*/
- (void)speechStartSentence{
NSLog(@"开始朗读");
}

/**
朗读结束
*/
- (void)speechEndSentence{
NSLog(@"朗读结束");
}


/**
朗读取消
*/
- (void)speechCancel{
NSLog(@"朗读取消");
}

/**
下一批文字长度
*/
- (void)newDataArrived:(NSNumber *)length{
NSLog(@"新数据长度:%@",length);
}


/**
当前已经朗读的长度
*/
- (void)currentTextSpeakLengthChanged:(NSNumber *)length{
NSLog(@"已经朗读的长度:%@",length);
}

```


## Author
301063915@qq.com

## License

BaiduTTS is available under the MIT license. See the LICENSE file for more info.
