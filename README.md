#vim keras-dlib.docker

'''
FROM keras:latest # start from an existing image

USER root # set the image to use the root 
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y python-dev python-pip && pip install --upgrade pip
RUN apt-get install -y python-opencv libboost-python-dev cmake python-matplotlib python-numpy python-pil python-scipy curl
RUN apt-get update && apt-get upgrade -y
RUN pip install dlib # install dlib
'''

#docker build -f keras-dlib.docker -t keras-dlib:1 . # build the docker image
#docker run -it -v /data:/data -v /home/shukui/Nauto/distraction/resnet_hyperface_keras:/data/shukui --runtime=nvidia -- name #shukui-keras-dlib keras-dlib:shukui bash # run the container

# apt-get install vim
