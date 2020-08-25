# windows audio render & mic capture with simple api and single dll


## AudioCaptureWinSdk简介
极简的Windows音频采集、混音DLL封装接口：

* 1、支持系统默认扬声器采集。
* 2、支持系统默认麦克风采集。
* 3、支持系统默认扬声器和麦克风混音后采集。
* 4、支持重采样到用户指定的采样率和声道数。
* 5、仅由一个DLL组成，占用空间小，无第三方依赖，集成简易。
* 6、C++开发，支持C、C++、C#


## AudioCaptureWinSdk C API

### 
* 环境初始化，系统只需调用一次<br>
@param: outputPath：日志文件输出的目录，若目录不存在将自动创建<br>
@param: outputLevel：日志输出的级别，只有等于或者高于该级别的日志输出到文件<br>
@return: <br>
void  `SDAudioCapture_Enviroment_Init`(const char * outputPath,  int outputLevel);

### 
* 环境反初始化，系统只需调用一次<br>
@return:<br>
void  `SDAudioCapture_Enviroment_Free`();

### 
* 创建SDAudioCapture，仅支持16bit<br>
@return: 返回模块指针，为NULL则失败<br>
void*  `SDAudioCapture_New`();

### 
* 销毁SDAudioCapture，使用者应该做好与其他API之间的互斥保护<br>
@param ppAudioCapture: 模块指针<br>
@return: <br>
void  `SDAudioCapture_Delete`(void** ppAudioCapture);

### 
* 开始采集<br>
@param pAudioCapture: 模块指针<br>
@param nSampleRate: 采集输出的采样率<br>
@param nChannelNum: 采集输出的声道数<br>
@param nBitsPerSample: 采集输出的样点比特数，目前仅支持16bit<br>
@param nOutputByteNum: 采集单次输出的样点字节数<br>
@param eCapType: 采集的类型，麦克风或扬声器或二者混音<br>
@param pfOutputCaptureData: 采集音频数据输出回调接口<br>
@param pObject: 上述输出回调接口的透传指针，将通过回调函数形参方式透传外层<br>
@return: TURE成功，FALSE失败<br>
BOOL  `SDAudioCapture_Start`(void* pAudioCapture, unsigned int nSampleRate, unsigned int nChannelNum, unsigned int nBitsPerSample, unsigned int nOutputByteNum, AUDIO_CAPTURE_SRC_TYPE eCapType, OutputCapturedData pfOutputCaptureData, OutputCapturedStatus pfOutputCapStatus, void* pObject);

### 
* 停止采集<br>
@param pAudioCapture: 模块指针<br>
@return: <br>
void  `SDAudioCapture_Stop`(void* pAudioCapture);



### 本库仅做演示用途，若需要商业用途与技术支持请联系 www.mediapro.cc
