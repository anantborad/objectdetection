# How to Run TensorFlow Lite Models on Windows

![](https://img.shields.io/github/directory-file-count/anantborad/objectdetection?color=g)
![](https://img.shields.io/github/languages/code-size/anantborad/objectdetection?color=purple)
![License](https://img.shields.io/badge/license-MIT-blue)

##### Read the [repository license](LICENSE.md) for the terms and conditions of downloading this software.

This guide shows how to set up a TensorFlow Lite Runtime environment on a Windows PC. We'll use [Anaconda](https://www.anaconda.com/) to create a Python environment to install the TFLite Runtime in. It's easy!
![](https://github.com/EdjeElectronics/TensorFlow-Lite-Object-Detection-on-Android-and-Raspberry-Pi/raw/master/doc/BSR_demo.gif)
## Step 1. Download and Install Anaconda
First, install [Anaconda](https://www.anaconda.com/), which is a Python environment manager that greatly simplifies Python package management and deployment. Anaconda allows you to create Python virtual environments on your PC without interfering with existing installations of Python. Go to the [Anaconda Downloads page](https://www.anaconda.com/products/distribution) and click the Download button.

When the download finishes, open the downloaded .exe file and step through the installation wizard. Use the default install options.

## Step 2. Set Up Virtual Environment and Directory
Go to the Start Menu, search for "Anaconda Command Prompt", and click it to open up a command terminal. We'll create a folder called `tflite1` directly in the C: drive. (You can use any other folder location you like, just make sure to modify the commands below to use the correct file paths.) Create the folder and move into it by issuing (copy and paste by right clicking and clicking on the options) the following commands in the terminal:

```shell
mkdir C:\tflite1
cd C:\tflite1
```

Next, create a Python 3.9 virtual environment by issuing:

```shell
conda create --name tflite1-env python=3.9
```

Enter "y" when it asks if you want to proceed. Activate the environment and install the required packages by issuing the commands below. We'll install TensorFlow, OpenCV, and a downgraded version of protobuf. TensorFlow is a pretty big download (about 450MB), so it will take a while.

```shell
conda activate tflite1-env
pip install tensorflow opencv-python protobuf==3.20.*
```

Download the detection scripts from this repository by issuing:

```shell
curl https://raw.githubusercontent.com/anantborad/objectdetection/master/TFLite_detection_image.py --output TFLite_detection_image.py
curl https://raw.githubusercontent.com/anantborad/objectdetection/master/TFLite_detection_video.py --output TFLite_detection_video.py
curl https://raw.githubusercontent.com/anantborad/objectdetection/master/TFLite_detection_webcam.py --output TFLite_detection_webcam.py
curl https://raw.githubusercontent.com/anantborad/objectdetection/master/TFLite_detection_stream.py --output TFLite_detection_stream.py
```

## Step 3. Move TFLite Model into Directory
Next, take the custom TFLite model that was trained and downloaded from the Colab notebook and move it into the `C:\tflite1` directory. If you downloaded it from Colab, it should be in a file called `custom_model_lite.zip`. (If you haven't trained a model yet and just want to test one out, download my "bird, squirrel, raccoon" model by clicking this Dropbox link.) Move that file to the `C:\tflite1` directory. Once it's moved, unzip it using:

```shell
tar -xf custom_model_lite.zip
```

At this point, you should have a folder at `C:\tflite1\custom_model_lite` which contains at least a `detect.tflite` and `labelmap.txt` file.

## Step 4. Run TensorFlow Lite Model!
There are four Python scripts to run the TensorFlow Lite object detection model on an image, video, web stream, or webcam feed. The scripts are based off the label_image.py example given in the [TensorFlow Lite examples GitHub repository](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/lite/examples/python/label_image.py).

* [TFLite_detection_image.py](TFLite_detection_image.py)
* [TFLite_detection_video.py](TFLite_detection_video.py)
* [TFLite_detection_stream.py](TFLite_detection_stream.py)
* [TFLite_detection_webcam.py](TFLite_detection_webcam.py)

The following instructions show how to run the scripts. These instructions assume your .tflite model file and labelmap.txt file are in the `TFLite_model` folder in your `tflite1` directory as per the instructions given in the [Setup TFLite Runtime Environment](#step-2-setup-tflite-runtime-environment-on-your-device) guide.

<p align="center">
   <img width="500" src="https://github.com/EdjeElectronics/TensorFlow-Lite-Object-Detection-on-Android-and-Raspberry-Pi/raw/master/doc/squirrels!!.png">
</p>

If you’d like try using the sample TFLite object detection model provided by Google, simply download it [here](https://storage.googleapis.com/download.tensorflow.org/models/tflite/coco_ssd_mobilenet_v1_1.0_quant_2018_06_29.zip), unzip it to the `tflite1` folder, and rename it to `TFLite_model`. Then, use `--modeldir=coco_ssd_mobilenet_v1_1.0_quant_2018_06_29` rather than `--modeldir=TFLite_model` when running the script. 

<details>
   <summary>Webcam</summary>
Make sure you have a USB webcam plugged into your computer. If you’re on a laptop with a built-in camera, you don’t need to plug in a USB webcam. 

From the `tflite1` directory, issue: 

```shell
python TFLite_detection_webcam.py --modeldir=TFLite_model 
```

After a few moments of initializing, a window will appear showing the webcam feed. Detected objects will have bounding boxes and labels displayed on them in real time.
</details>

<details>
   <summary>Video</summary>
To run the video detection script, issue:

```shell
python TFLite_detection_image.py --modeldir=TFLite_model
```

A window will appear showing consecutive frames from the video, with each object in the frame labeled. Press 'q' to close the window and end the script. By default, the video detection script will open a video named 'test.mp4'. To open a specific video file, use the `--video` option:

```shell
python TFLite_detection_image.py --modeldir=TFLite_model --video='birdy.mp4'
```

Note: Video detection will run at a slower FPS than realtime webcam detection. This is mainly because loading a frame from a video file requires more processor I/O than receiving a frame from a webcam.
</details>

<details>
   <summary>Web stream</summary>
To run the script to detect images in a video stream (e.g. a remote security camera), issue: 

```shell
python TFLite_detection_stream.py --modeldir=TFLite_model --streamurl="http://ipaddress:port/stream/video.mjpeg" 
```

After a few moments of initializing, a window will appear showing the video stream. Detected objects will have bounding boxes and labels displayed on them in real time.

Make sure to update the URL parameter to the one that is being used by your security camera. It has to include authentication information in case the stream is secured.

If the bounding boxes are not matching the detected objects, probably the stream resolution wasn't detected. In this case you can set it explicitly by using the `--resolution` parameter:

```shell
python TFLite_detection_stream.py --modeldir=TFLite_model --streamurl="http://ipaddress:port/stream/video.mjpeg" --resolution=1920x1080
```
</details>

<details>
   <summary>Image</summary>
To run the image detection script, issue:

```shell
python TFLite_detection_image.py --modeldir=TFLite_model
```

The image will appear with all objects labeled. Press 'q' to close the image and end the script. By default, the image detection script will open an image named 'test1.jpg'. To open a specific image file, use the `--image` option:

```shell
python TFLite_detection_image.py --modeldir=TFLite_model --image=squirrel.jpg
```

It can also open an entire folder full of images and perform detection on each image. There can only be images files in the folder, or errors will occur. To specify which folder has images to perform detection on, use the `--imagedir` option:

```shell
python TFLite_detection_image.py --modeldir=TFLite_model --imagedir=squirrels
```

Press any key (other than 'q') to advance to the next image. Do not use both the --image option and the --imagedir option when running the script, or it will throw an error.

</details>

**See all command options**

For more information on options that can be used while running the scripts, use the `-h` option when calling them. For example:

```shell
python TFLite_detection_image.py -h
```
