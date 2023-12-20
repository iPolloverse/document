# 视频说话 (X-me)

## 介绍
"照片扮演角色(X-me)" 是一项创新服务，允许用户的照片在指定视频中扮演角色。这种技术通过处理用户提供的照片和视频文件，创造出一种新颖的视觉体验，让照片在视频中“活”起来。

## 示例

## API 使用说明

### 1.视频生成接口

#### 请求方式
- **方法**: POST
- **URL**: https://obai.ipolloverse.cn/iPollo/twinSync/videotalking_v3

#### 请求参数
请求需要包含以下JSON格式的参数：
```json
{
  "video_url": "https://twinsync.oss-cn-hangzhou.aliyuncs.com/video/1683034663.mp4",
  "text": "大家好，我是一个虚拟人说话，哈哈！",
  "btc_address": "bc1pv0egqadxd60ae4r7v77gewpvjvsza09kccsxztzx8c8pqccn0rgqqw7np5"
}
```
- video_url: 指向要使用的视频文件的云存储地址
- text: 说话内容
- btc_address: 用户的比特币地址

#### 响应格式
请求成功后，将返回包含以下信息的JSON格式数据：
```
{
    "task_id": "生成的任务Id",
    "result_code": 100,
    "msg": "返回的消息"
}
```
- task_id: 分配给执行任务的唯一标识符
- result_code: 表示响应状态的代码值
- msg: 提供有关响应的额外信息或消息

##### 状态码说明
- 200: 请求参数错误或不完整。
- 202: 音频或视频文件的云地址无效或缺失。
- 203: 内部服务器错误，例如视频转换失败或存储失败。

### 2.任务查询接口

#### 请求方式

- **方法**: GET
- **URL**: https://obai.ipolloverse.cn/iPollo/twinSync/videotalking_v3?taskID=***

#### 请求参数
 - taskID：生成接口返回的task_id

```
{
    "result_url": "https://pop.ipolloverse.cn:8090/iPollo/twinSync/example/20230423_11_23_05_10279.mp4",    #生成的视频路径
    "result_code": 100,     #返回的code值
    "msg": "taskID:20230423_11_23_05_10279 has been completed, and the output video url is: https://pop.ipolloverse.cn:8090/iPollo/twinSync/example/20230423_11_23_05_10279.mp4",   #返回的Msg信息
    "api_time_consume": 10, #视频时长（秒）
    "api_time_left": 590,   #剩余时长（秒）
    "video_w": 1920,        #视频宽度 "video_h": 1080,        #视频高度
    "gpu_type": "NVIDIA GeForce RTX 3090",  #对标GPU类型（暂时无用）
    "gpu_time_estimate": 120,   #预估gpu消耗时长（暂时无用）
    "gpu_time_use": 82      #gpu消耗时长
} 
```
code值列表: 
- 100：任务处于成功状态
- 101：任务处于等待状态
- 102：任务处于运行状态
- 103：任务处于失败状态
- 200：taskID字段缺失或者该字段不在服务队列中
