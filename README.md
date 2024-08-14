This repository provides [WhisperX](https://github.com/m-bain/whisperX) in a Docker image.

The image installs Python 3.10 on Ubuntu 22.10 base images, as well as pre-requisites such as PyTorch.

# Using the image
WhisperX can be ran on CPU or GPU, using either of the following Docker images.

## CPU-only
```
docker run -it --rm -v /path/to/audio_files:/app thomasvvugt/whisperx:cpu recording.mp3 --batch_size 4 --compute_type int8
```

## Nvidia CUDA 11.8
Note: Dedicated hardware graphics card (GPU) are much more performant, especially for diarization.

You can also keep track of your cache across runs (e.g. to prevent multiple downloads from HF), by mounting `/root/.cache`.

```
docker run -it --rm --gpus all -v /path/to/audio_files:/app -v /path/to/cache:/root/.cache thomasvvugt/whisperx:cuda118 recording.mp3 --batch_size 8 --diarize --hf_token YOUR_HUGGINGFACE_READ_TOKEN
```

# Building the image
You can either use the pre-built images from Docker Hub, or build the images yourself.

```
docker build -f Dockerfile.cpu -t whisperx:cpu
docker build -f Dockerfile.cuda118 -t whisperx:cuda118
```
