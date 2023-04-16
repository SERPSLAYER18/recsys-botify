FROM continuumio/anaconda3

WORKDIR /app

COPY requirements.txt .
RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install make cmake -y
#RUN apk add --no-cache make cmake

RUN pip install --upgrade pip
RUN pip install --upgrade make
RUN pip install --upgrade cmake
RUN pip install -r requirements.txt

RUN conda install -c pytorch/label/nightly faiss-cpu
RUN conda install -c conda-forge gym
RUN pip install -U numpy

COPY sim ./sim
COPY data ./data
COPY config ./config

RUN mkdir -p ./log

ENV PYTHONPATH "${PYTHONPATH}:/app"

CMD python sim/run.py --episodes 1000 --config config/env.yml multi --processes 8