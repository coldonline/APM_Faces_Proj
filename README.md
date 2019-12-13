# Bias in Age & Gender Prediction CNN
___

#### Examining bias in VGG-Face through the lens of age and gender prediction to encourage the development of fair, accountable, and transparent machine learning.

![AI](artificial-intelligence-2167835_1920.jpg)

The initial approach focuses in predicting the age and gender of people based on their facial images, with the academic goal of implementing real-time image classification. 

While some stores already use visual recognition for theft control. The business implication of this could be facial recognition to enhance store loyalty programs or for customization of services. A Forbes article points out that loyalty members have generally already agreed to share personal data with the brand, so enhancement of loyalty programs through facial recognition may not be far in the future.

With its burgeoning ubiquity, it felt important to understand this technology, so the inner workings of image detection and classification are explored by building a convolutional neural net capable of predicting a person’s age and gender from his or her image. With the use of transfer learning, a model trained with a large image set can be re-trained with a dataset of photos of people "in-the-wild", which are more suited for the interests of the project. Then using predictions from the model, a further examination of any bias the model might have is made. Although the findings may not be perfectly representative of the models being used in commercial deployment today, this project aims to shed light on bias in machine learning and to highlight the importance of thoughtful development of fair, accountable, and transparent machine learning.

## Requirements
This repository was tested on the following environment. It can be re-created using the environment.yml file.

name: jerry
channels:
  - defaults
dependencies:
  - _tflow_select=2.1.0=gpu
  - absl-py=0.8.0=py36_0
  - astor=0.8.0=py36_0
  - attrs=19.2.0=py_0
  - backcall=0.1.0=py36_0
  - blas=1.0=mkl
  - bleach=3.1.0=py36_0
  - ca-certificates=2019.8.28=0
  - certifi=2019.9.11=py36_0
  - colorama=0.4.1=py36_0
  - cudatoolkit=9.0=1
  - cudnn=7.6.0=cuda9.0_0
  - cycler=0.10.0=py36h009560c_0
  - decorator=4.4.0=py36_1
  - defusedxml=0.6.0=py_0
  - entrypoints=0.3=py36_0
  - freetype=2.9.1=ha9979f8_1
  - gast=0.3.2=py_0
  - grpcio=1.16.1=py36h351948d_1
  - h5py=2.8.0=py36hf7173ca_2
  - hdf5=1.8.20=hac2f561_1
  - icc_rt=2019.0.0=h0cc432a_1
  - icu=58.2=ha66f8fd_1
  - intel-openmp=2019.4=245
  - ipykernel=5.1.2=py36h39e3cac_0
  - ipython=7.8.0=py36h39e3cac_0
  - ipython_genutils=0.2.0=py36h3c5d0ee_0
  - jedi=0.15.1=py36_0
  - jinja2=2.10.3=py_0
  - joblib=0.13.2=py36_0
  - jpeg=9b=hb83a4c4_2
  - jsonschema=3.0.2=py36_0
  - jupyter_client=5.3.3=py36_1
  - jupyter_core=4.5.0=py_0
  - keras=2.2.4=0
  - keras-applications=1.0.8=py_0
  - keras-base=2.2.4=py36_0
  - keras-preprocessing=1.1.0=py_1
  - kiwisolver=1.1.0=py36ha925a31_0
  - libopencv=3.4.2=h20b85fd_0
  - libpng=1.6.37=h2a8f88b_0
  - libprotobuf=3.9.2=h7bd577a_0
  - libsodium=1.0.16=h9d3ae62_0
  - libtiff=4.0.10=hb898794_2
  - m2w64-gcc-libgfortran=5.3.0=6
  - m2w64-gcc-libs=5.3.0=7
  - m2w64-gcc-libs-core=5.3.0=7
  - m2w64-gmp=6.1.0=2
  - m2w64-libwinpthread-git=5.0.0.4634.697f757=2
  - markdown=3.1.1=py36_0
  - markupsafe=1.1.1=py36he774522_0
  - matplotlib=3.1.1=py36hc8f65d3_0
  - mistune=0.8.4=py36he774522_0
  - mkl=2019.4=245
  - mkl-service=2.3.0=py36hb782905_0
  - mkl_fft=1.0.14=py36h14836fe_0
  - mkl_random=1.1.0=py36h675688f_0
  - msys2-conda-epoch=20160418=1
  - nbconvert=5.6.0=py36_1
  - nbformat=4.4.0=py36h3a5bc1b_0
  - notebook=6.0.1=py36_0
  - numpy=1.15.4=py36h19fb1c0_0
  - numpy-base=1.15.4=py36hc3f5095_0
  - opencv=3.4.2=py36h40b0b35_0
  - openssl=1.1.1d=he774522_2
  - pandas=0.25.1=py36ha925a31_0
  - pandoc=2.2.3.2=0
  - pandocfilters=1.4.2=py36_1
  - parso=0.5.1=py_0
  - pickleshare=0.7.5=py36_0
  - pip=19.2.3=py36_0
  - prometheus_client=0.7.1=py_0
  - prompt_toolkit=2.0.10=py_0
  - protobuf=3.9.2=py36h33f27b4_0
  - py-opencv=3.4.2=py36hc319ecb_0
  - pygments=2.4.2=py_0
  - pyparsing=2.4.2=py_0
  - pyqt=5.9.2=py36h6538335_2
  - pyrsistent=0.15.4=py36he774522_0
  - python=3.6.9=h5500b2f_0
  - python-dateutil=2.8.0=py36_0
  - pytz=2019.3=py_0
  - pywin32=223=py36hfa6e2cd_1
  - pywinpty=0.5.5=py36_1000
  - pyyaml=5.1.2=py36he774522_0
  - pyzmq=18.1.0=py36ha925a31_0
  - qt=5.9.7=vc14h73c81de_0
  - scikit-learn=0.21.3=py36h6288b17_0
  - scipy=1.1.0=py36h29ff71c_2
  - send2trash=1.5.0=py36_0
  - setuptools=41.4.0=py36_0
  - sip=4.19.8=py36h6538335_0
  - six=1.12.0=py36_0
  - sqlite=3.30.0=he774522_0
  - tensorboard=1.12.2=py36h33f27b4_0
  - tensorflow=1.12.0=gpu_py36ha5f9131_0
  - tensorflow-base=1.12.0=gpu_py36h6e53903_0
  - tensorflow-gpu=1.12.0=h0d30ee6_0
  - termcolor=1.1.0=py36_1
  - terminado=0.8.2=py36_0
  - testpath=0.4.2=py36_0
  - tornado=6.0.3=py36he774522_0
  - tqdm=4.28.1=py36h28b3542_0
  - traitlets=4.3.3=py36_0
  - vc=14.1=h0510ff6_4
  - vs2015_runtime=14.16.27012=hf0eaf9b_0
  - wcwidth=0.1.7=py36h3d5aa90_0
  - webencodings=0.5.1=py36_1
  - werkzeug=0.16.0=py_0
  - wheel=0.33.6=py36_0
  - wincertstore=0.2=py36h7fe50ca_0
  - winpty=0.4.3=4
  - xz=5.2.4=h2fa13f4_4
  - yaml=0.1.7=hc54c509_2
  - zeromq=4.3.1=h33f27b4_3
  - zlib=1.2.11=h62dcd97_3
  - zstd=1.3.7=h508b16e_0
  - pip:
    - imutils==0.5.3
    - pillow==6.2.1
    - seaborn==0.9.0

## License
This project is released under the MIT license. However, the [IMDB-WIKI dataset](https://data.vision.ee.ethz.ch/cvl/rrothe/imdb-wiki/) used in this project is originally provided under the following conditions. 

> Please notice that this dataset is made available for academic research purpose only. All the images are collected from the Internet, and the copyright belongs to the original owners. If any of the images belongs to you and you would like it removed, please kindly inform us, we will remove it from our dataset immediately.

Therefore, the pretrained model(s) included in this repository is restricted by these conditions (available for academic research purpose only).

## References and Acknowledgments
### Datasets:
* [UTK-Face](https://susanqq.github.io/UTKFace/)
* [IMDB-WIKI](https://data.vision.ee.ethz.ch/cvl/rrothe/imdb-wiki/)

### Github Repos:
* https://github.com/yu4u/age-gender-estimation
* https://github.com/serengil/tensorflow-101
