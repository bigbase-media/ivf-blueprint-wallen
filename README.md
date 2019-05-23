# 1.	关于轨迹的使用方法案例
有些时候素材的运动的路线和速度比较灵活多变，只通过起始和结束两个点，无法准确的表现，或者即使能通过多组action来表现，也因为action过多而过于复杂，不方便维护；在这种情况下，对action引入了轨迹的track属性。track的值是一个资源url，该资源主要是用来指示每一个相对时间点素材的位置情况，## 1.1 "projectionType": "normal"
### 形式如下：
#### timescale:1000
 #### 0:0,0,1,1 #### 100:0,0,1,1 #### 250:0,0,1,1 #### 300:0.1,0.1,0.9,0.9 
#### 400:0,0,1,1 #### 500:0.1,0.1,0.9,0.9 #### 600:0,0,1,1 #### 700:0.1,0.1,0.9,0.9#### 800:0,0,1,1 #### 900:0.1,0.1,0.9,0.9 #### 1000:0,0,1,1#### 1100:0.1,0.1,0.9,0.9 #### 1200:0,0,1,1 #### 1300:0.1,0.1,0.9,0.9 
#### 1400:0,0,1,1#### 1500:0.1,0.1,0.9,0.9 
#### 1550:0,0,1,1

### 第1行timescale:1000
timescale时间刻度，1秒时间被分为的粒度，1000，表示毫秒精度；### 第2行0:0,0,1,1 
冒号左边是时间点，0即第0秒；冒号右边是对应这个时间点的位置信息，0,0,1,1表示素材占据整个画面；在"projectionType": "normal"时，位置信息有用逗号隔开的4个值，分别为左上水平坐标，左上竖直坐标，右下水平坐标，右下竖直坐标，并且是相对于整个屏幕的相对值### 第5行500:0.1,0.1,0.9,0.9 
冒号左边的500，表示这个位置的时间点在第0.5秒；冒号右边是对应这个时间点的位置信息，0.1,0.1,0.9,0.9 表示素材在画面的位置是占据画面的左上10%,10%到右下90%,90%这个部分## 1.2"projectionType": "perspective"
每个时间点后面的位置信息是四边形的顺时针顺序的4个点相对坐标位置。### 案例：
[设计图](https://github.com/bigbase-media/ivf-blueprint-wallen/tree/master/samples/抖动.json) 
# 2.	关于文字渐变显示方法案例
可以通过subaction中的四边形动态裁切ploygon来实现文字逐步显示效果### 案例：[设计图 ](https://github.com/bigbase-media/ivf-blueprint-wallen/tree/master/samples/textDisplay.json)
# 3.	手工实现转场方法案例
除了一些固定风格的转场可以通过类型指定关键字来加载外，也可以通过多个action的衔接来达到转场的效果### 案例1：
[设计图](https://github.com/bigbase-media/ivf-blueprint-wallen/tree/master/samples/manualTransition.json) ### 案例2：
[设计图](https://github.com/bigbase-media/ivf-blueprint-wallen/tree/master/samples/manualTransition2.json) # 4.	文字镂空填入素材方法案例
文字中可以填入图像或者视频纹理，来达到比较丰富的效果### 案例1：
[设计图](https://github.com/bigbase-media/ivf-blueprint-wallen/tree/master/samples/textWithTexture.json) ### 案例2：
[设计图](https://github.com/bigbase-media/ivf-blueprint-wallen/tree/master/samples/textWithVidTexture.json) 
5.	文字描边和阴影案例给文字加入描边或者加入阴影### 案例1：
[设计图](https://github.com/bigbase-media/ivf-blueprint-wallen/tree/master/samples/textWithColorBorder.json) ### 案例2：
[设计图](https://github.com/bigbase-media/ivf-blueprint-wallen/tree/master/samples/textWithVidTexture.json) # 6.	透视的使用案例
通过透视变换来完成转场过渡案例：[设计图](https://github.com/bigbase-media/ivf-blueprint-wallen/tree/master/samples/perspectiveTransition.json) 
# 7.	多个subaction的使用案例

可以通过多个相同或不同的subaction的组合来生成更复杂的特效### 案例：[设计图](https://github.com/bigbase-media/ivf-blueprint-wallen/tree/master/samples/multipleSubactions.json) # 8.	带alpha通道的mov视频的处理
因为OpenCV不支持视频的alpha通道的读入，带alpha通道的mov视频都需要将视频内容分离成alpha通道视频文件和前景内容视频文件，再分别作为素材添加到设计图json中将mov视频通过ffmpeg分离成alpha视频和前景视频的命令行为：### 获取alpha视频：ffmpeg -i xxx.mov -vf extractplanes="a",format=yuv420p -f mp4 -y xxx_alpha.mp4
### 获取前景视频：ffmpeg -i xxx.mov -vf format=yuv420p -f mp4 -y xxx_fg.mp4
