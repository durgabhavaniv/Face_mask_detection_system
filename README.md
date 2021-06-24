# Face_mask_detection_system

'''sudo docker run --rm -ti --volume "$PWD":/app --env DISPLAY=:0 --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" --device /dev/snd --device /dev/video0 "test/face_mask_detection_openvino" bash -c "source /opt/intel/openvino/bin/setupvars.sh && export NO_AT_BRIDGE=1 && python main.py --face-model models/face-detection-adas-0001 --mask-model models/face_mask -i resources/mask.mp4 --enable-speech --tts "Husband-please-wear-your-mask" --ffmpeg --debug --show-bbox"'''
