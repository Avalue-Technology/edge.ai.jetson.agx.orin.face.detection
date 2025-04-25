# TensorFlow and FaceNet Setup on JetPack 5.1

This guide walks through the installation of system packages, Python dependencies, TensorFlow with NVIDIA support, and setting up the FaceNet model with MTCNN using TensorRT.

---

## 📦 Install System Dependencies

```bash
sudo apt update
sudo apt install -y \
  libhdf5-serial-dev hdf5-tools libhdf5-dev \
  zlib1g-dev zip libjpeg8-dev \
  liblapack-dev libblas-dev gfortran
```

---

## 🐍 Install and Upgrade `pip3`

```bash
sudo apt install -y python3-pip
sudo python3 -m pip install --upgrade pip
sudo pip3 install -U testresources setuptools==65.5.0
```

---

## 📚 Install Python Package Dependencies

```bash
sudo pip3 install -U \
  numpy==1.22 \
  future==0.18.2 \
  mock==3.0.5 \
  keras_preprocessing==1.1.2 \
  keras_applications==1.0.8 \
  gast==0.4.0 \
  protobuf \
  pybind11 \
  cython \
  pkgconfig \
  packaging \
  h5py==3.6.0
```

---

## ⚙️ Install TensorFlow for JetPack 5.1

```bash
sudo pip3 install --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v51 \
  tensorflow==2.11.0+nv23.01
```

---

## 📥 Download FaceNet Model

```bash
wget https://github.com/apollo-time/facenet/raw/master/model/resnet/facenet.pb
```

Place the file in your project directory.

---

## 🔄 Convert `.pb` Model to UFF

```bash
cd path/to/project
python3 step01_pb_to_uff.py
```

---

## 🤖 Clone and Setup MTCNN TensorRT

```bash
cd path/to/project/..
git clone https://github.com/PKUZHOU/MTCNN_FaceDetection_TensorRT

# Move the models into your project folder
mv MTCNN_FaceDetection_TensorRT/det* path/to/project/mtCNNModels
```

---

## 🛠️ Build the Project

```bash
mkdir -p path/to/project/build
cd path/to/project/build

cmake -DCMAKE_BUILD_TYPE=Release ..
make -j$(nproc)
```
