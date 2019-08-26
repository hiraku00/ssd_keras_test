# To Do
- I tried to detect objects in the video
- Object detection algorithm uses SSD(Single Shot MultiBox Detector)

# Summary
- 1. Download the source code
- 2. Download trained model
- 3. Environment construction
- 4. Modify the source code
- 5. Specifying video files
- 6. Object detection execution
- 7. Execution result conversion(png -> gif)

# Operating Environment
- macOS Catalina 10.15 beta
- anaconda 4.6.14
- Python 3.5.4
- tensorflow 1.3.0
- keras 1.2.2
- opencv-python 3.3.0.9
- imageio 2.4.1

# 1. Download the source code
- Download the source code with the following command

```terminal
$ git clone https://github.com/rykov8/ssd_keras.git
$ cd ssd_keras
```

# 2. Download trained model
The trained model is published [here](https://mega.nz/#F!7RowVLCL!q3cEVRK9jyOSB9el3SssIA), so download ```weights_SSD300.hdf5```
<img width="955" alt="スクリーンショット 2019-08-19 8.04.21.png" src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/67194/e93147fb-bff4-507c-fe0e-60e29c645038.png">
- Store the downloaded file directly under the project

# 3. Environment construction
- Download the configuration file for building the Anaconda environment from [here](https://gist.github.com/yampy/4e0fc4aea37cf0f432ab243d76285e98) and store it directly under the project
- Build the Anaconda environment with the following command based on the downloaded configuration file (.yaml)
- Also install 'imageio' separately
- And then activate the environment

```terminal
$ conda env create -f ykov8_ssd_keras.yaml
$ conda install imageio
$ source activate rykov8_ssd_keras
```

# 4. Modify the source code
- In my environment, I fixed the following part
- Output object detection results on console
- The object detection result is saved in 'png' format in the "image" folder of "testing_utils" (line 182)

```python:/testing_utils/videotest.py

#--------------
# Line 12
#--------------
# before
from scipy.misc import imread, imresize
# after
from imageio import imread

#--------------
# Line 87
#--------------
# before
vidw = vid.get(cv2.cv.CV_CAP_PROP_FRAME_WIDTH)
vidh = vid.get(cv2.cv.CV_CAP_PROP_FRAME_HEIGHT)
# after
vidw = vid.get(cv2.CAP_PROP_FRAME_WIDTH)
vidh = vid.get(cv2.CAP_PROP_FRAME_HEIGHT)

#--------------
# Line 99
#--------------
# before

# after
num_frame = 0

#--------------
# Line 162
#--------------
# before

# after
print(text)

#--------------
# Line 182
#--------------
# before
# after
print(text)
cv2.imwrite("./image/frame_" + str('{0:04d}'.format(num_frame)) +".png", to_draw)
num_frame += 1
```

# 5. Specifying video files
- Specify the video file with ```videotest_example.py```
- The video file was downloaded from [Pexels (free video site)](https://www.pexels.com/videos/)

```python:/testing_utils/videotest_example.py
#--------------
# Line 24
#--------------
# before
vid_test.run('path/to/your/video.mkv')
# after
vid_test.run('../movie/1.mp4')
```

# 6. Object detection execution
- Perform object detection with the specified video
- Create the 'image' folder in the 'testing_utils' folder as described on line 182 in 4.

```terminal
$ python videotest_example.py
```

# 7. Execution result conversion(png -> gif)
- When execution is complete, convert the png file in the 'image' folder to gif
- I used [PicGIF Lite](https://apps.apple.com/jp/app/picgif-lite/id844918735?mt=12) to convert png to gif.

# Result (gif file)
1. crowded

![sample1.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/67194/22bbc70c-0d60-d96f-fe70-fbdaaae498a2.gif)

2. Sidewalks and roadways

![sample2.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/67194/a3e854b2-20dc-0aee-e1b1-34144a457ba6.gif)

3. Tourist spots

![sample3.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/67194/8157736e-7948-606c-772a-841bf4a04d4a.gif)

4. Chat

![sample4.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/67194/b755d3e0-ddc0-4f0f-eb4f-e8f0c8def572.gif)

# In Japanese
[Qiita](https://qiita.com/hiraku00/items/6b89c3d54e278056df0a)
