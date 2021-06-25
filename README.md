# Face_mask_detection_system

| Details            |              |
|-----------------------|---------------|
| Programming Language: |  [![Python 3.7](https://img.shields.io/badge/python-3.7-blue.svg)](https://www.python.org/downloads/release/python-370/) |
| Intel OpenVINO ToolKit: |[![OpenVINO 2020.2](https://img.shields.io/badge/openvino-2020.2-blue.svg)](https://software.intel.com/content/www/us/en/develop/tools/openvino-toolkit/choose-download.html)|
| Docker (Ubuntu OpenVINO pre-installed): | [durgabhavaniv/face_mask_detection](https://hub.docker.com/repository/docker/durgabhavaniv/face_mask_detection)|
| Hardware Used: | Intel(R) Core(TM) i7-9850H CPU @ 2.60GHz |
| Device: | CPU |

Face Mask Detection application uses Deep Learning/Machine Learning to recognize if a user is not wearing a mask and issues an alert.

By utilizing pre-trained models and Intel OpenVINO toolkit with OpenCV. This enables us to use the async API which can improve overall frame-rate of the application, rather than wait for inference to complete, the application can continue operating on the host while accelerator is busy.

This application executes 2 parallel infer requests for the Face Mask Detection and Face Detection networks that run simultaneously.

Using a set of the following pre-trained models:
- [face-detection-adas-0001](https://docs.openvinotoolkit.org/latest/_models_intel_face_detection_adas_0001_description_face_detection_adas_0001.html), which is a primary detection network for finding faces.
- face-mask-detection, which is a pretrained model for detecting a mask.

This application can be improved and then integrated with CCTV or other types cameras to detect and identify people without masks in public areas such as shopping centres and etc. This the ever increasing COVID-19 cases world-wide these application could be useful in controlling the spread of the virus.

**What is OpenVino?**

OpenVino (OpenVisual Inferencing and Neural Network Optimization) is toolkit to develop Deep Learning Application especially for Computer Vision by Intel. OpenVino Enables deep learning inference at the edge and supports heterogeneous execution across computer vision accelerators—CPU, GPU, Intel® Movidius™ Neural Compute Stick, and FPGA—using a common API. [read more](https://docs.openvinotoolkit.org/)

### Tutorial

#### YouTube Tutorial

The first of many...

[![Watch the video](https://user-images.githubusercontent.com/7910856/88237923-a8514500-cc80-11ea-9cc8-0692eb0c4d6e.gif)](https://www.youtube.com/watch?v=6r6foGbCHQ0)

## Hardware Requirement

- Minimum Intel Gen 6 processors


## Installation

- Download the docker images with a pre-installed version of OpenVINO 2020.2
```bash
docker pull durgabhavaniv/face_mask_detection
```

## Usage

```bash
$ python main.py -h

usage: main.py [-h] -f FACE_MODEL -m MASK_MODEL -i INPUT [-d DEVICE]
               [--face_prob_threshold FACE_PROB_THRESHOLD]
               [--mask_prob_threshold MASK_PROB_THRESHOLD] [--enable-speech]
               [--tts TTS] [--ffmpeg] [--show-bbox] [--debug]

optional arguments:
  -h, --help            show this help message and exit
  -f FACE_MODEL, --face-model FACE_MODEL
                        Path to an xml file with a trained model.
  -m MASK_MODEL, --mask-model MASK_MODEL
                        Path to an xml file with a trained model.
  -i INPUT, --input INPUT
                        Path to image or video file or 'cam' for Webcam.
  -d DEVICE, --device DEVICE
                        Specify the target device to infer on: CPU, GPU, FPGA
                        or MYRIAD is acceptable. Sample will look for a
                        suitable plugin for device specified (CPU by default)
  --face_prob_threshold FACE_PROB_THRESHOLD
                        Probability threshold for face detections filtering
                        (Default: 0.8)
  --mask_prob_threshold MASK_PROB_THRESHOLD
                        Probability threshold for face mask detections
                        filtering(Default: 0.3)
  --enable-speech       Enable speech notification.
  --tts TTS             Text-to-Speech, used for notification.
  --ffmpeg              Flush video to FFMPEG.
  --show-bbox           Show bounding box and stats on screen [debugging].
  --debug               Show output on screen [debugging].

```

### Example Usage

```bash
sudo make run-bootstrap
```
or
```bash
sudo docker run --rm -ti --volume "$PWD":/app --env DISPLAY=:0 --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" --device /dev/snd --device /dev/video0 "durgabhavaniv/face_mask_detection" bash -c "source /opt/intel/openvino/bin/setupvars.sh && export NO_AT_BRIDGE=1 && python main.py --face-model models/face-detection-adas-0001 --mask-model models/face_mask -i resources/mask.mp4 --enable-speech --tts "please-wear-your-mask-properly" --ffmpeg --debug --show-bbox"
```
