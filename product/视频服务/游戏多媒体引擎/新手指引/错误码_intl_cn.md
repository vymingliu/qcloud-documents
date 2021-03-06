欢迎使用腾讯云游戏多媒体引擎 SDK 。为方便开发者调试和接入腾讯云游戏多媒体引擎产品 API，这里向您介绍适用于游戏多媒体引擎开发的错误码文档。

## GMESDK 客户端错误

|错误码名称     |错误码值|含义           |原因          |建议方案       |
|---- ----|----|--- ----|--------------------|-------------- -----|
|AV_ERR_FAILED                 				|1   	  |一般错误                                                   								|具体原因需要通过分析日志等来定位                                                                                                                                                                                     |分析日志                                                               |
|AV_ERR_REPEATED_OPERATION     		|1001|重复操作                                                  										|"已经在进行某种操作，再次去做同样的操作，则会产生这个错误。如已经在进入房间过程中，再去做进入房间的操作，就会产生这个错误。操作类别主要有：AVContext类、房间类、设备类、成员类。AVContext类型的操作：StartContext/StopContext。房间类型的操作：EnterRoom/ExitRoom。设备类型的操作：打开/关闭某个设备。成员类型的操作：请求画面/取消画面。"|等待上一个操作完成后再进行下一个操作。|
|AV_ERR_EXCLUSIVE_OPERATION    		|1002|互斥操作                                                   										|已经在进行某种操作，再次去做同类型的其他操作，则会产生这个错误。如在进入房间过程中，去做退出房间的操作，就会产生这个错误。                                                                                                                                        						|等待上一个操作完成后再进行下一个操作。                                                																		|
|AV_ERR_HAS_IN_THE_STATE       			|1003|已处于所要状态                                               									|对象已经处于某种状态，再去做使得它进入这种状态的操作时，则会产生这个错误。如已经在房间中，再去做进入房间的操作，就会产生这个错误。                                                                                                                                    					|由于已经处于所要状态，可以认为该操作已经成功，当作成功来处理。                                    														|
|AV_ERR_INVALID_ARGUMENT       		|1004|错误参数                                                  	 									|调用SDK接口时，传入错误的参数，则会产生这个错误。如进入房间时，传入的房间类型不等于AVRoom::ROOM_TYPE_PAIR或AVRoom::ROOM_TYPE_MULTI，就会产生这个错误。                                                                                                  		|详细阅读API文档，搞清楚每个接口的每个参数的有效取值范围，确认哪些参数没有按照规范来取值，保证传入参数的正确性并进行相应的预防处理。		|
|AV_ERR_TIMEOUT               				|1005|超时                                                     										|进行某个操作，在规定的时间内，还未返回操作结果，则会产生这个错误。多数情况下，涉及到信令传输的、且网络出问题的情况下，才容易产生这个错误。如执行进入房间操作时，30s后还没有返回进入房间操作完成的结果的话，就会产生这个错误。	|确认网络是否有问题，并尝试重试。                                                   																			|
|AV_ERR_NOT_IMPLEMENTED        		|1006|未实现                                                    										|调用SDK接口时，如果相应的功能还未支持，则会产生这个错误。                                                                                                                                                                      	 																	|暂不支持该功能，找其他替代方案。                                                   																			|
|AV_ERR_NOT_IN_MAIN_THREAD     		|1007|不在主线程                                                  									|SDK对外接口要求在主线程执行，如果业务侧调用SDK接口时，没有在主线程调用，则会产生这个错误。                                                                                                                                                     												|修改业务侧逻辑，确保在主线程调用SDK接口。                                             																	|
|AV_ERR_RESOURCE_IS_OCCUPIED   		|1008|资源被占用                                                 										|当需要用到某种资源，如摄像头、屏幕等，而这些资源已经被占用了，则会产生这个错误。                                                                                                                                                             														|确认具体要用到哪些资源，及这样资源被谁占用了，确保在正确的时机使用SDK相关功能以保证资源使用不冲突。									|
|AV_ERR_CONTEXT_NOT_EXIST      		|1101|AVContext状态问题                  												|当AVContext对象未处于CONTEXT_STATE_STARTED状态，去调用需要处于这个状态才允许调用的接口时，则会产生这个错误。                                                                                                                                										|修改业务侧逻辑，确保调用SDK接口的时机的正确性。                                          																|
|AV_ERR_CONTEXT_NOT_STOPPED    		|1102|AVContext状态问题            													|当AVContext对象未处于CONTEXT_STATE_STOPPED状态，去调用需要处于这个状态才允许调用的接口时，则会产生这个错误。如不在这种状态下，去调用AVContext::DestroyContext时，就会产生这个错误。          								|修改业务侧逻辑，确保调用SDK接口的时机的正确性。                                          																|
|AV_ERR_ROOM_NOT_EXIST        			|1201|AVRoom状态问题                    												|当AVRoom对象未处于ROOM_STATE_ENTERED状态，去调用需要处于这个状态才允许调用的接口时，则会产生这个错误。                                                                                                                                      										|修改业务侧逻辑，确保调用SDK接口的时机的正确性。                                          																|
|AV_ERR_ROOM_NOT_EXITED        		|1202|AVRoom状态问题                         											|当AVRoom对象未处于ROOM_STATE_EXITED状态，去调用需要处于这个状态才允许调用的接口时，则会产生这个错误。如不在这种状态下，去调用AVContext::StopContext时，就会产生这个错误。                  										|修改业务侧逻辑，确保调用SDK接口的时机的正确性。                                          																|
|AV_ERR_DEVICE_NOT_EXIST      			|1301|设备不存在                                                  									|当设备不存在或者设备初始化未完成时，去使用设备，则会产生这个错误。                                                                                                                                                                    																|确认设备是否真的存在，确保设备id填写的正确性，确保在设备初始化成功后再去使用设备。                         										|
|AV_ERR_ENDPOINT_NOT_EXIST     		|1401|AVEndpoint对象不存在                                       	 							|当成员没有在发语音或视频时，去获取它的AVEndpoint对象时，就可能产生这个错误。                                                                                                                                                          															|修改业务侧逻辑，确保调用SDK接口的时机的正确性。                                         			 													|
|AV_ERR_ENDPOINT_HAS_NOT_VIDEO	|1402|成员没有发视频                                                									|当成员没有在发视频时，去做需要成员发视频的相关操作时，就可能产生这个错误。如当某个成员没有发送视频时，去请求他的画面，就会产生这个错误。                                                                                                 								|修改业务侧逻辑，确保调用SDK接口的时机的正确性。                                          																|
|AV_ERR_TINYID_TO_OPENID_FAILED		|1501|tinyid转identifier失败                                    									|当收到某个成员信息更新的信令时，需要去把tinyid转成identifier，如果IMSDK库相关逻辑存在问题、网络存在问题等，则会产生这个错误。                                                                                                                  									|确认网络是否存在问题，查看日志确认IMSDK相关逻辑是否存在问题。                                  														|
|AV_ERR_OPENID_TO_TINYID_FAILED		|1502|identifier转tinyid失败                                   									|当调用StartContext接口时，需要去把identifier转成tinyid，如果IMSDK库相关逻辑存在问题、网络存在问题、没有处于登录态时等，则会产生这个错误。                                                                                                								|确认网络是否存在问题，查看日志确认IMSDK相关逻辑是否存在问题，确认已经成功调用IMSDK的登录接口。										|
|AV_ERR_DEVICE_TEST_NOT_EXIST  		|1601|AVDeviceTest状态问题														|当AVDeviceTest对象未处于DEVICE_TEST_STATE_STARTED状态，去调用需要处于这个状态才允许调用的接口时，则会产生这个错误。                                                                                                                         									|修改业务侧逻辑，确保调用SDK接口的时机的正确性。                                          																|
|AV_ERR_DEVICE_TEST_NOT_STOPPED	|1602|AVDeviceTest状态问题														|当AVDeviceTest对象未处于DEVICE_TEST_STATE_STOPPED状态，去调用需要处于这个状态才允许调用的接口时，则会产生这个错误。如不在这种状态下，去调用AVContext::StopContext时，就会产生这个错误。    								|修改业务侧逻辑，确保调用SDK接口的时机的正确性。                                          																|
|AV_ERR_INVITE_FAILED          			|1801|发送邀请失败                                                 									|发送邀请时产生的失败。                                                                                                                                                                                          																								|邀请模块只是用于DEMO演示方便用，对外暂不支持邀请功能，所以业务侧不需要处理这些错误码。												|
|AV_ERR_ACCEPT_FAILED         			|1802|接受邀请失败                                                 									|接受邀请时产生的失败。                                                                                                                                                                                          																								|邀请模块只是用于DEMO演示方便用，对外暂不支持邀请功能，所以业务侧不需要处理这些错误码。 												|
|AV_ERR_REFUSE_FAILED          			|1803|拒绝邀请失败                                                 									|拒绝邀请时产生的失败。                                                                                                                                                                                          																								|邀请模块只是用于DEMO演示方便用，对外暂不支持邀请功能，所以业务侧不需要处理这些错误码。   												|
|QAV_ERR_NOT_TRY_NEW_ROOM      		|2001|没有尝试进入新房间，将停留在旧房间。                                     					|切换到新房间失败，但仍然在当前房间                                                                                                                                                                                    																						|在当前房间仍可以正常使用。                                                      																				|
|QAV_ERR_TRY_NEW_ROOM_FAILED   	|2002|尝试进入新房间，但失败了，旧房间也将关闭。                                  				|切换到新房间失败，同时已退出原来的房间                                                                                                                                                                                  																					|退出房间，重新进入。                                                         																					|

## GMESDK 服务端错误

| 错误码名称                          | 错误码值 | 含义       | 原因                                                         | 建议方案                                                     |
| ----------------------------------- | -------- | ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| AV_ERR_SERVER_FAILED                | 10001    | 一般错误   | 具体原因需要通过分析日志确认后台返回给客户端的真正错误码才能知道。 | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| AV_ERR_SERVER_INVALID_ARGUMENT      | 10002    | 错误参数   | 调用SDK接口时，或SDK内部发送信令给后台时，传了错误的参数，具体原因需要通过分析日志确认后台返回给客户端的真正错误码才能知道。 | 确保调用SDK接口时所传的参数的正确性。分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| AV_ERR_SERVER_NO_PERMISSION         | 10003    | 没有权限   | 没有权限使用某个功能，具体原因需要通过分析日志确认后台返回给客户端的真正错误码才能知道。如进入房间时所带的签名错误或过期，就会产生这个错误。 | 确保在设置正确的权限参数后才去使用相应的功能。分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| AV_ERR_SERVER_TIMEOUT               | 10004    | 超时       | 具体原因需要通过分析日志确认后台返回给客户端的真正错误码才能知道。 | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| AV_ERR_SERVER_ALLOC_RESOURCE_FAILED | 10005    | 资源不够   | 执行某些操作时，需要分配更多的资源(如内存)失败了，或者超过最大的资源限制(如超过最大的房间成员人数)，则会产生这个错误。具体原因需要通过分析日志确认后台返回给客户端的真正错误码才能知道。 | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| AV_ERR_SERVER_ID_NOT_IN_ROOM        | 10006    | 不在房间内 | 在不在房间内时，去执行某些操作，则会产生这个错误。具体原因需要通过分析日志确认后台返回给客户端的真正错误码才能知道。 | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| AV_ERR_SERVER_NOT_IMPLEMENT         | 10007    | 未实现     | 调用SDK接口时，如果相应的功能还未支持，则会产生这个错误。    | 暂不支持该功能，找其他替代方案。                             |
| AV_ERR_SERVER_REPEATED_OPERATION    | 10008    | 重复操作   | 具体原因需要通过分析日志确认后台返回给客户端的真正错误码才能知道。 | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| AV_ERR_SERVER_ROOM_NOT_EXIST        | 10009    | 房间不存在 | 房间不存在时，去执行某些操作，则会产生这个错误。             | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| AV_ERR_SERVER_ENDPOINT_NOT_EXIST    | 10010    | 成员不存在 | 某个成员不存在时，去执行该成员相关的操作，则会产生这个错误。 | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| AV_ERR_SERVER_INVALID_ABILITY       | 10011    | 错误能力   | 具体原因需要通过分析日志确认后台返回给客户端的真正错误码才能知道。 | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |

## GMESDK 离线语音错误

| 错误码名称                                  | 错误码值 | 含义           | 原因                                        | 建议方案                                                     |
| ------------------------------------------- | -------- | -------------- | ------------------------------------------- | ------------------------------------------------------------ |
| QAVPTTERROR_RECORDER_PARAM_NULL             | 4097     | 录音错误       | 修改参数                                    | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_RECORDER_INIT_ERROR             | 4098     | 录音错误       | 修改初始化错误                              | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_RECORDER_RECORDING_ERROR        | 4099     | 录音错误       | 正在录制中                                  | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_RECORDER_RECORDING_ERROR        | 4100     | 录音错误       | 正在录制中                                  | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_RECORDER_NO_AUDIO_DATA_WARN     | 4101     | 录音错误       | 没有采集到音频数据，重新尝试                | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_RECORDER_OPENFILE_ERROR         | 4102     | 录音错误       | 文件访问错误                                | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_RECORDER_MIC_PERMISSION_ERROR   | 4103     | 录音错误       | 麦克风未授权错误                            | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_RECORDER_VOICE_RECORD_TOO_SHORT | 4104     | 录音错误       | 录音时间太短错误                            | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_UPLOAD_FILE_ACCESSERROR         | 8193     | 上传错误       | 文件访问错误                                | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_UPLOAD_SIGN_CHECK_FAIL          | 8194     | 上传错误       | 签名校验失败错误                            | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_UPLOAD_NETWORK_FAIL             | 8195     | 上传错误       | 网络错误                                    | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_UPLOAD_GET_TOKEN_NETWORK_FAIL   | 8196     | 上传错误       | 获取上传参数过程中，http 网络失败           | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_UPLOAD_GET_TOKEN_RESP_NULL      | 8197     | 上传错误       | 获取上传参数过程中，回包数据为空            | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_UPLOAD_GET_TOKEN_RESP_INVALID   | 8198     | 上传错误       | 获取上传参数过程中，回包解包失败            | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_UPLOAD_TOKEN_CHECK_EXPIRED      | 8199     | 上传错误       | TLS 签名校验明确过期，需要重新申请 TLS 签名 | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_UPLOAD_APPINFO_UNSET            | 8200     | 上传错误       | 没有设置 appinfo                            | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_DOWNLOAD_FILE_ACCESSERROR       | 12289    | 下载错误       | 文件访问错误                                | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_DOWNLOAD_SIGN_CHECK_FAIL        | 12290    | 下载错误       | 签名校验失败                                | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_DOWNLOAD_NETWORK_FAIL           | 12291    | 下载错误       | 网络错误                                    | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_DOWNLOAD_REMOTEFILE_ACCESSERROR | 12292    | 下载错误       | 服务器文件系统错误                          | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_DOWNLOAD_GET_SIGN_NETWORK_FAIL  | 12293    | 下载错误       | 获取下载参数过程中，http 网络失败           | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_DOWNLOAD_GET_TOKEN_RESP_NULL    | 12294    | 下载错误       | 获取下载参数过程中，回包数据为空            | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_DOWNLOAD_GET_TOKEN_RESP_INVALID | 12295    | 下载错误       | 获取下载参数过程中，回包解包失败            | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_DOWNLOAD_TOKEN_CHECK_EXPIRED    | 12296    | 下载错误       | TLS 签名校验明确过期，需要重新申请 TLS 签名 | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_DOWNLOAD_APPINFO_UNSET          | 12297    | 下载错误       | 没有设置 appinfo                            | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_PLAYER_INIT_ERROR               | 20481    | 播放错误       | 初始化错误                                  | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_PLAYER_PLAYING_ERROR            | 20482    | 播放错误       | 正在播放中                                  | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_PLAYER_PARAM_NULL               | 20483    | 播放错误       | 参数为空                                    | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_PLAYER_OPEN_FILE_ERROR          | 20484    | 播放错误       | 文件访问错误                                | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_V2T_INTERNAL_ERROR              | 32769    | 语音转文字错误 | 内部错误                                    | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_V2T_NETWORK_FAIL                | 32770    | 语音转文字错误 | http网络失败                                | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_V2T_RSP_DATA_NULL               | 32771    | 语音转文字错误 | 回包数据为空                                | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_V2T_RSP_DATA_DECODE_FAIL        | 32772    | 语音转文字错误 | 回包解包失败                                | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_V2T_SIGN_CHECK_EXPIRED          | 32773    | 语音转文字错误 | TLS 签名校验明确过期，需要重新申请 TLS 签名 | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| QAVPTTERROR_V2T_APPINFO_UNSET               | 32774    | 语音转文字错误 | 没有设置 appinfo                            | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
