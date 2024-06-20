# GST-mvs
GST-mvs is a 3D reconstruction framework based on multi-view stereo methd.

## Dependencies
The code has been tested on Ubuntu 22.04 with i9 14900K/RTX4090, and you can modify the CMakeList.txt to compile on Windows.

* Cuda >= 6.0
* OpenCV >= 2.4
* cma090

Besides make sure that your GPU Compute Capability matches the CMakeList.txt! Otherwise you can only get the empty result without any warnings. For example, according to GPU Compute Capability, RTX 4090's Compute Capability is 8.9. So you should set the cuda compilation parameter 'arch=compute_89,code=sm_89' or add a '-gencode arch=compute_89,code=sm_89'.

## Usage
### Complie GST-mvs
```
cmake .    
make
```
### Testing dataset
Download train and test dataset (style as xxx_dslr_undistorted.7z) from [ETH3D](https://www.eth3d.net/datasets), and use the script colmap2mvsnet.py to convert the dataset format(you may refer to MVSNet).
```
python colmap2mvsnet.py --dense_folder <ETH3D data path, such as ./ETH3D/office> --save_folder <The path to save>
```
### Run
After the code and dataset preparation, the code can be run as follows:
```
./GST <ETH3D root path>/office
```
It is very easy to use, and you can modify our code as you need.
