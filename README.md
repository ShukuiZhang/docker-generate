```
vim keras-dlib.docker # create a docker file

# in the docker file
FROM keras:latest 
USER root 
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y python-dev python-pip && pip install --upgrade pip
RUN apt-get install -y libboost-python-dev cmake vim python-matplotlib python-numpy python-pil python-scipy curl
RUN pip install opencv-python scikit-image mtcnn

docker build -f keras-dlib.docker -t keras-dlib:1 . # build the docker image
docker run -it -v /data:/data -v /home/shukui/Nauto/distraction/resnet_hyperface_keras:/data/shukui --runtime=nvidia --name shukui-keras-dlib keras-dlib:shukui bash # run the container

'''
