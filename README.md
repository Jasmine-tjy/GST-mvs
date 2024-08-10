# GST-mvs 
GST-mvs is a 3D reconstruction framework based on multi-view stereo methd.

## About :blush:
This repository contains the code for Generalized Sampling of Non-Local Textural Clues Multi-View Stereo Framework. Our paper was accepted by ACM MM 2024, if you find our work useful in your research, please consider citing:
  ```
@inproceedings{Tang2024Generalized,
  title={Generalized Sampling of Non-Local Textural Clues Multi-View Stereo Framework},
  author={Tang, Jingyuan and Cai, Yangang and Gao, Xuesong and Sun, Songlin},
  booktitle={Proceedings of the 32st ACM International Conference on Multimedia},
  year={2024}
}
  ```

## Dependencies :hammer:
The code has been tested on Ubuntu 22.04 with i9 14900K/RTX4090, and you can modify the CMakeList.txt to compile on Windows.

* [Cuda](https://developer.nvidia.cn/cuda-toolkit) >= 6.0
* [OpenCV](https://opencv.org/) >= 2.4
* [cmake](https://cmake.org/) >= 2.8

Besides make sure that your GPU Compute Capability matches the CMakeList.txt! Otherwise you can only get the empty result without any warnings. For example, according to GPU Compute Capability, RTX 4090's Compute Capability is 8.9. So you should set the cuda compilation parameter 'arch=compute_89,code=sm_89' or add a '-gencode arch=compute_89,code=sm_89'.

Due to version matching issues among cuda, opencv, and cmake, the construction environment is quite complex. For this purpose, we have uploaded a __Docker image__ suitable for this model, which allows users to create an environment and directly run the software in the image to achieve 3D reconstruction. The available image can be found in [cmake_cuda_opencv](https://hub.docker.com/r/tangjas111/cmake_cuda_opencv/tags)

__!__ The provided image is mainly for the code executing which is not for Python, you can prepare the dataset first by using personal python environment.
### Tips of using docker :whale2:
* Login in your docker account first
* Pull the docker image from docker hub
  ```
  docker pull tangjas111/cmake_cuda_opencv:latest
  ```
* Run docker container
  ```
  docker run -itd --name GST-test --runtime=nvidia --gpus all tangjas111/cmake_cuda_opencv:latest
  ```
* Copy the source code and preprocessed dataset into the container
  ```
  docker cp <dataset> <container id>:<work directory>
  docker cp <source code> <container id>:<work directory>
  ```
## Usage :rocket:
### Complie GST-mvs
```
cmake .    
make
```
### Testing dataset :open_file_folder:
Download train and test dataset (style as xxx_dslr_undistorted.7z) from [ETH3D](https://www.eth3d.net/datasets), and use the script colmap2mvsnet.py to convert the dataset format(you may refer to MVSNet).
```
python colmap2mvsnet.py --dense_folder <ETH3D data path, such as ./ETH3D/office> --save_folder <The path to save>
```
To make our code testing easier, we provide a preprocessed dataset in the folder "__dataset_kicker__", which is one of the training datasets in ETH3D. This dataset can be used for simple testing.
### Run :arrow_left:
After the code and dataset preparation, the code can be run as follows:
```
./GST <ETH3D root path>/dataset_kicker
```
It is very easy to use, and you can modify our code as you need.

## Demo Video :clapper:
demo.mp4 is provided as a whole installation instruction.

## Acknowledgements
This code largely benefits from the following repositories: [ACMMP](https://github.com/GhiXu/ACMMP). Thanks to their authors for opening the source of their excellent works.

