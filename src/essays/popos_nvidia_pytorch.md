

```Dockerfile
FROM nvcr.io/nvidia/pytorch:23.04-py3

ARG USERNAME
ARG USER_UID
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
  && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME

RUN pip install fastai
```

```bash
docker build --build-arg USERNAME="$USER" --build-arg USER_UID="$UID" -t fastai .
```

```bash
docker run  \
  --rm \
  -it \
  -p 8888:8888 \
  --runtime=nvidia \
  --user ${USER} \
  -v ${PWD}:/workspace/code \
  --ipc=host \
  --ulimit memlock=-1 \
  --ulimit stack=67108864 \
  --gpus all \
  nvcr.io/nvidia/pytorch:23.04-py3 \
  jupyter notebook
```
