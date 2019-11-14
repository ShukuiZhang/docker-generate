# How to create a docker container
Introduce how to create a docker containfer from scratch.
## sample structure
Create a tree structure using bash command `tree -I *.jpg`, where `-I` is not to list any `*.jpg` files:
```
├── base_image
│   ├── Dockerfile
│   └── requirements.txt
├── Dockerfile
├── __init__.py
├── ReadMe.md
├── utils.py
├── video.mp4
└── visualization.py
```
## build base image
```
docker build -f Dockerfile -t bmw-demo:shukui .
```
### base_image/Dockerfile
```
FROM nvidia/cuda:10.0-cudnn7-runtime-ubuntu16.04

COPY requirements.txt /tmp/requirements.txt

RUN apt update && \
  apt install -yq python3-pip libgtk2.0-dev vim && \
  pip3 install --upgrade pip && hash -r pip && \
  pip3 install -r /tmp/requirements.txt
```
### base_image/requirements.txt
```
numpy==1.16.3
opencv-python==4.1.0.25
tensorflow-gpu==1.13.1
Keras==2.2.4
matplotlib==3.0.0
```
### Dockerfile
```
FROM bmw-demo:shukui
# USER root 
COPY raw_models /bmw-demo/raw_models
COPY nauto4.mp4 /bmw-demo/nauto4.mp4
COPY nauto_tmp4 /bmw-demo/nauto_tmp4
COPY ReadMe.md /bmw-demo/ReadMe.md
COPY utils.py /bmw-demo/utils.py
COPY visualization.py /bmw-demo/visualization.py

WORKDIR /bmw-demo
```
## build refined image
```
docker build -f Dockerfile -t bmw-demo-refine:shukui .
```
## Run the container
```
docker run -it -v /data:/data -v /data16:/data16 --runtime=nvidia --name bmw-0 bmw-demo-refine:shukui bash
```
