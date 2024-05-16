# FastSpeech 2 - Russian

This is a text-to-speech system FastSpeech 2: Fast and High-Quality End-to-End Text to Speech russian language.

![](./img/model.png)

# Quickstart

## Dependencies
You can install the Python dependencies with
```
pip3 install -r requirements.txt
```

## Inference

You have to download the [pretrained models](https://drive.google.com/drive/folders/1I5DVpP4-v1vNdCcVz28m_Pvt1duSdCDY?usp=sharing) 

Run
```
python3 synthesize.py --text "YOUR_DESIRED_TEXT" --restore_step 250000 --mode single -p config/RUSLAN/preprocess.yaml -m config/RUSLAN/model.yaml -t config/RUSLAN/train.yaml
```


The generated utterances will be put in ``output/result/``.



## Controllability
The pitch/volume/speaking rate of the synthesized utterances can be controlled by specifying the desired pitch/energy/duration ratios.
For example, one can increase the speaking rate by 20 % and decrease the volume by 20 % by

```
python3 synthesize.py --text "YOUR_DESIRED_TEXT" --restore_step 900000 --mode single -p config/LJSpeech/preprocess.yaml -m config/LJSpeech/model.yaml -t config/LJSpeech/train.yaml --duration_control 0.8 --energy_control 0.8
```

# Training

## Datasets

The supported datasets are

- (https://drive.google.com/drive/folders/13BJUDUrB43HXBVdeJNNoYC9Ms4qlWr7g?usp=drive_link) a single-speaker Russian dataset consists of 10918 short audio.

Create a folder raw_data and copy the dataset there.

## Preprocessing
 
First, run 
```
The preprocessing script by
```
python3 preprocess.py config/RUSLAN/preprocess.yaml
```


## Training

Train your model with
```
python3 train.py -p config/RUSLAN/preprocess.yaml -m config/RUSLAN/model.yaml -t config/RUSLAN/train.yaml
```


# TensorBoard

Use
```
tensorboard --logdir output/log/RUSLAN
```

to serve TensorBoard on your localhost.
The loss curves, synthesized mel-spectrograms, and audios are shown.

# Implementation Issues

- Following [xcmyz's implementation](https://github.com/xcmyz/FastSpeech), I use an additional Tacotron-2-styled Post-Net after the decoder, which is not used in the original FastSpeech 2.
- Gradient clipping is used in the training.


```
