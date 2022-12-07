# Installation

## Requirements

Follow the installation in this order to make sure the package versions are compatible with each other.

## Python, PyTorch and TorchVision
- Python >= 3.8 (Python 3.9 does not support torchvision build with ffmpeg). Details in this [issue](https://github.com/facebookresearch/SlowFast/issues/181#issuecomment-1241692131) and mentioned in torchvision source code with a FIXME comment (https://github.com/pytorch/vision/blob/15a9a93b9e0e6173b936691a2cddced0ecfd271f/setup.py#L374)
- PyTorch >= 1.3 and [torchvision](https://github.com/pytorch/vision/) that matches the PyTorch installation.
  You can install them together at [pytorch.org](https://pytorch.org) to make sure of this. If you follow the installation steps here, you won't need to install torchvision from source for ffmpeg support, it will be automatically handled.

## Video backend
SlowFast supports two video backends: torchvision and PyAV
- ffmpeg: `conda install ffmpeg=4.2` This version works well with newer pytorch and torchvision distibutions. By default torchvision will be used, and Facebook updates the framework according to torchvision.
- PyTorchVideo: `pip install "git+https://github.com/facebookresearch/pytorchvideo.git"`. DO NOT use `pip install pytorchvideo` as included in the official repo since it misses some functions needed.
- PyAV: Will be installed along with PyTorchVideo, so DO NOT use: `conda install av -c conda-forge` as included in the original repo as this conda-forge installation can have contradictions with current ffmpeg version. Also, this video backend does not work out of box. In the newer SlowFast versions, there are type mismatches in the slowfast/datasets/decoder.py file. In order to make it run, please read this [pull request](https://github.com/facebookresearch/SlowFast/pull/541) and this [comment in this issue](https://github.com/facebookresearch/SlowFast/issues/181#issuecomment-1122954279). You need to update the decoder.py file yourself as the pull request still hasn't been finalized.

## Other Requirements
- Numpy
- [fvcore](https://github.com/facebookresearch/fvcore/): `pip install 'git+https://github.com/facebookresearch/fvcore'`
- simplejson: `pip install simplejson`
- GCC >= 4.9
- PyYaml: (will be installed along with fvcore)
- tqdm: (will be installed along with fvcore)
- iopath: `pip install -U iopath` or `conda install -c iopath iopath`
- psutil: `pip install psutil`
- OpenCV: `pip install opencv-python`
- tensorboard: `conda install tensorboard`. Use conda install to have the necessary requirements instead of the pip command included in the official repo.
- scikit-learn: ̣̣̣̣̣̣̣̣̣̣̣̣̣̣̣̣̣̣̣`pip install scikit-learn` (sklearn is not supported anymore)
- moviepy: (optional, for visualizing video on tensorboard) `conda install -c conda-forge moviepy` or `pip install moviepy`
- FairScale: `pip install 'git+https://github.com/facebookresearch/fairscale'`
- cython: `pip install cython`
- [Detectron2](https://github.com/facebookresearch/detectron2):

```
    pip install -U 'git+https://github.com/facebookresearch/fvcore.git' 'git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI'
    git clone https://github.com/facebookresearch/detectron2 detectron2_repo
    pip install -e detectron2_repo
    # You can find more details at https://github.com/facebookresearch/detectron2/blob/master/INSTALL.md
```

## PySlowFast

Clone the PySlowFast Video Understanding repository.
```
git clone https://github.com/facebookresearch/slowfast
```

Add this repository to $PYTHONPATH.
```
export PYTHONPATH=/path/to/SlowFast/slowfast:$PYTHONPATH
```

## Build PySlowFast

After having the above dependencies, run:
```
git clone https://github.com/facebookresearch/slowfast
cd SlowFast
python setup.py build develop
```

Now the installation is finished, run the pipeline with:
```
python tools/run_net.py --cfg configs/Kinetics/C2D_8x8_R50.yaml NUM_GPUS 1 TRAIN.BATCH_SIZE 8 SOLVER.BASE_LR 0.0125 DATA.PATH_TO_DATA_DIR path_to_your_data_folder
```
