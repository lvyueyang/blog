---
title: Audio, Video 事件集合  
tag: JavaScript  
---  

## 监听事件  
### loadstart  
> 当浏览器开始寻找指定的音频/视频时，即当加载过程开始时   

### durationchange  
> 当指定音频/视频的时长数据发生变化时  

### loadedmetadata  
> 当指定的音频/视频的元数据已加载时  

### progress  
> 当浏览器正在下载指定的音频/视频时 

### suspend  
> 该事件在媒体数据被阻止加载时触发。 可以是完成加载后触发，或者因为被暂停的原因 

### loadeddata  
> 当当前帧的数据已加载，但没有足够的数据来播放指定音频/视频的下一帧时

### canplay  
> 当浏览器能够开始播放指定的音频/视频时

### canplaythrough  
> 当浏览器预计能够在不停下来进行缓冲的情况下持续播放指定的音频/视频时  

### play  
> 开始播放时触发  

### playing  
> 开始回放  

### timeupdate  
> 播放时间改变   这个会一直打印  

### pause  
> 暂停时会触发，当播放完一首歌曲时也会触发  

### ended  
> 当播放完一首歌曲时也会触发  

### abort  
> 客户端主动终止下载（不是因为错误引起）  

### error  
> 请求数据时遇到错误   

### stalled  
> 网速失速  

### waiting  
> 等待数据，并非错误  

### seeking  
> 寻找中

### seeked  
> 寻找完毕  

### ratechange  
> 播放速率改变  

### volumechange  
> 音量改变    
  