# TensorFlow 2 Object Detection

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


### Create label map file in training_demo/annotations with name label_map.pbtxt

and write content as -

```
item {
    id: 1
    name: 'helmet'
}

item {
    id: 2
    name: 'head'
}

item {
    id: 3
    name: 'person'
}
```
# Create TensorFlow Records

- It is time to convert our annotations into the so called TFRecord format.

## curl the generate_tfrecord.py file under root of training_demo dir

```bash
curl https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/_downloads/da4babe668a8afb093cc7776d7e630f3/generate_tfrecord.py > generate_tfrecord.py
```

## generate_tfrecord

#### for train data:
```bash
python generate_tfrecord.py -x images/train -l annotations/label_map.pbtxt -o annotations/train.record
```
#### for test data:
```bash
python generate_tfrecord.py -x images/test -l annotations/label_map.pbtxt -o annotations/test.record
```
# Configuring a Training Job

## Go to [model Zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2_detection_zoo.md) and download SSD ResNet50 V1 FPN 640X640 (RetinaNet50)

- extract the downloaded model into training_demo/pre-trained-model directory

## Configure training pipeline
- create a folder my_ssd_resnet50_v1_fpm in training_demo/models folder,
- copy pipeline.config from to my_ssd_resnet50_v1_fpm from pre-trained_model directory,
- update it as per the documentation - [link](https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/training.html)

## Copy training file from TensorFlow/models/reserch/object_detection/ to the root of training_demo folder

```bash
cp ../../TensorFlow/models/reserch/object_detection/model_main_tf2.py .
```

## Start training by running the following command - 
```bash
python model_main_tf2.py --model_dir=models/my_ssd_resnet50_v1_fpn --pipeline_config_path=models/my_ssd_resnet50_v1_fpn/pipeline.config
```

## Exporting a Trained Model

```bash
cp ../../TensorFlow/models/research/object_detection/exporter_main_v2.py .

python exporter_main_v2.py --input_type image_tensor --pipeline_config_path ./models/my_ssd_resnet50_v1_fpn/pipeline.config --trained_checkpoint_dir ./models/my_ssd_resnet50_v1_fpn/ --output_directory ./exported-models/my_model
```









- Source URL: https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/install.html#tensorflow-object-detection-api-installation









