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
echo TensorFlow/models >> .gitignore
```


