# Commands

## Download gitignore using curl

```bash
curl https://raw.githubusercontent.com/c17hawke/FSDS-DVC-NLP-Project-with-docs/main/.gitignore > .gitignore
```

## Download init_setup.sh using curl

```bash
curl https://raw.githubusercontent.com/c17hawke/general_template/main/init_setup.sh > init_setup.sh
```

## Run init_setup.sh

```bash
bash init_setup.sh
```

## tensorflow verification

```bash
python -c "import tensorflow as tf;print(tf.config.list_physical_devices('GPU'))"
```

# Installation of Object Detection API


## create a TensorFlow directory
```bash
mkdir TensorFlow && cd TensorFlow
```
## Clone the TensorFlow models folder here
```bash
git clone https://github.com/tensorflow/models.git
```

remove .git dir of models repository to avoid git conflicts

add models folder to .gitignore
```bash
echo "TensorFlow/models" >> .gitignore
```

## Protobuff Installation/Compilation

- Visit the link - https://github.com/protocolbuffers/protobuf/releases
 - windows user - 
   - search for - protoc-3.20.1-win64.zip
 -  for mac users - 
   - search for - protoc-3.20.1-osx-x86_64.zip
 - for linux users -
   ```
   sudo apt install -y protobuf-compiler
   ```
- Unzip into root folder and add `<PATH TO protoc folder>/bin` into system environment variables

## Check protobuff version 

- run the following command

```bash
cd TensorFlow/models/research
protoc --version
```

## Convert all protobuff files into python files

- run the following command

```bash
cd TensorFlow/models/research
protoc object_detection/protos/*.proto --python_out=.
```

## Install COCO API
```bash
pip install git+https://github.com/philferriere/cocoapi.git#subdirectory=PythonAPI
```

## Install Object Detection API
- From within TensorFlow/models/research/

```bash
cp object_detection/packages/tf2/setup.py .
python -m pip install .
```

## test your installation
- From within TensorFlow/models/research/
```bash
python object_detection/builders/model_builder_tf2_test.py
```

# Run examples -

- Create workspace/example_1 directory in project root

  ```bash
  mkdir -p workspace/example_1
  ```

- cd to workspace/example_1
  ```bash
  cd workspace/example_1
  ```

- Download notebook
  ```bash
  curl https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/_downloads/55b1ed8e083cbc9ca3bfc1c18eb6b860/plot_object_detection_saved_model.ipynb > plot_object_detection_saved_model.ipynb
  ```


# Custom model training
```bash
mkdir workspace/training_demo
cd workspace/training_demo
mkdir -p annotations exported-models models pre-trained-models images/test images/train
```




- Source URL: https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/install.html#tensorflow-object-detection-api-installation









