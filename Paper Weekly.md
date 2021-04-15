# paper reading

This is a document of my weekly paper reading from April, 2021.

## keyword

#abr #video_system #live

## papers

+ **PiTree: Practical Implementation of ABR Algorithms Using Decision Trees**  

19 MM Tsinghua University  #abr

采用决策树来转化传统的DRL-based ABR算法，使得算法更轻量级且性能不受大的影响。

+ **Ekya: Continuous Learning of Video Analytics Models on Edge Compute Servers**  

20 UC Berkeley #video analysis; #video_system

将continuous learning加入视频分析中，边推断边学习。

Continuous training on limited edge resources requires smartly deciding **when** to retrain each video stream’s model, **how much resources** to allocate, and **what configurations** to use. But making these decisions has two challenges.    

什么时候分配：每次训练完分配。资源：多少unit的GPU resources。configuration：number of training epochs, batch sizes, number of neurons in the last layer, number of frozen layers, and fraction of training data.

作者设计了一个启发式算法进行分配。估计分配后的准确率时，采用小的分析器进行估计。

+ **HotDASH: Hotspot Aware Adaptive Video Streaming using Deep Reinforcement Learning**  

18 ICNP，IIT Kharagpur, Kharagpur, India #abr

这一篇做的是热点视频片段的提前下载。观看视频时，经常会有用户更感兴趣的片段（比如比赛关键时刻），在网络状况好时，提前下载这些片段的高清版本，使得这些片段有更高的质量。

作者改进自pensieve，采用DRL求解，对于每个时刻，决定下一个普通chunk的码率，决定下一个hotspot chunk的码率，再决定是否要下载hotspot chunk。

作者实现了一个比较完整的系统，ABR决策在服务端作为一个service。计算hotspot时采用不同的QoE质量函数，得到的值会更高。

+ **User Centered Adaptive Streaming of Dynamic Point Clouds with Low Complexity Tiling**

这篇文章没有完全get到。讲的是volumetric video的传输，可以跟360度视频一样分割tile。本文是依据拍摄的摄像机进行分割，从object中心映射到各个point，然后看该向量跟哪个摄像头的向量接近（我的理解）。分割成tile后，就可以有不同的质量表示，然后依据用户的坐标和视野请求对应的tile。

+ **MultiLive: Adaptive Bitrate Control for Low-delay Multi-party Interactive Live Streaming**

20 infocom, Tsinghua University  #live

这篇文章解决的是多端视频通信问题（连麦），每一端既为上传方又为下载方。作者首先建立问题，最大化QoE，包含质量、质量变化、卡顿和延时，同时设置带宽上限，优化的变量是各个streamer上传和receiver下载的码率。

作者采用Non-linear Programming方法求解问题，得到一个时间窗口固定的传输码率，同时每一帧中利用PID controller校正误差，得到从每一帧发送方到接收方的（下载）传输码率。上传方面，作者又设计了一个基于聚类的方法，来决定一个stream应该上传哪种码率。（这里作者说上传一个SVC码率，按我理解SVC分为基础层和增强层，确实可以上传一个码率，后面算法又可以上传多种码率，有点不太理解）。

这篇文章从问题到求解到参数设置，还有挺多部分有待商榷，不过场景和idea不错。问题：1、作者看似是基于CS架构，但是整体的场景和设置又有点像P2P；2、作者在问题设置定义了上传和下载的带宽上限，一个用户可以同时充当sender和receiver，怎么区别这两种类型的带宽占用比例呢，平衡这两个过程呢，能否跟其他paper一样把带宽约束去掉呢；3、作者说避免转码，采用多码率SVC编码。如何比较转码和SVC的差异呢，因为CS架构转码传输还是一个比较常见的模型。4、作者问题定义有些是以帧为单位的，后面有些是以time interval为单位的，感觉有点混乱。5、公式4有点不是很直观，加入是减慢，后一项就变成正的？如果缓存变空了，会有影响吗。目标缓存大小能否作为优化变量呢。碰到阈值播放速度就改变，改变多久呢，速度改变对QoE的影响呢。6、作者看起来是一帧帧调整码率，这样会造成码率的抖动吗。

------------------------------------------------------------------------------------------------------------------------------------------------------





