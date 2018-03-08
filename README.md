# Protest Activity Detection and Perceived Violence Estimation from Social Media Images
Implementation of the model used in the paper **_Protest Activity Detection and Perceived Violence Estimation from Social Media Images_** (ACM Multimedia 2017) [\[arxiv\]](https://arxiv.org/abs/1709.06204) by [Donghyeon Won](dhwon.com), [Zachary C. Steinert-Threlkeld](https://zacharyst.com/), [Jungseock Joo](http://home.jsjoo.com/).

![](https://raw.githubusercontent.com/wondonghyeon/protest-detection-violence-estimation/master/files/overview.png)

### Requirements   
[Pytorch](http://pytorch.org/)   
[NumPy](http://www.numpy.org/)   
[pandas](https://pandas.pydata.org/)   
[scikit-learn](http://scikit-learn.org/)   

### UCLA Protest Image Dataset   
![](https://raw.githubusercontent.com/wondonghyeon/protest-detection-violence-estimation/master/files/1-d.png)
You will need to download our UCLA Protest Image Dataset to train the model. Please e-mail me if you want to download our dataset!

#### Dataset Statistics   
\# of images: 40,764   
\# of protest images: 11,659   
##### Protest \& Visual Attributes   

|Fields       |Protest|Sign  |Photo|Fire |Law Enf.|Children|Group>20|Group>100|Flag |Night|Shout|
|-------------|-------|------|-----|-----|--------|--------|--------|---------|-----|-----|-----|
|\# of Images |11,659 |9,669 |428  |667  |792     |347     |8,510   |2,939    |970  |987  |548  |
|Positive Rate|0.286  |0.829 |0.037|0.057|0.068   |0.030   |0.730   |0.252    |0.083|0.085|0.047|
##### Violence   

|Mean |Median |STD  |
|-----|-------|-----|
|0.365|0.352  |0.144|

![](https://raw.githubusercontent.com/wondonghyeon/protest-detection-violence-estimation/master/files/violence_hist.png)

### Model
#### Architecture   
We fine-tuned ImageNet pretrained [ResNet50](https://arxiv.org/abs/1512.03385) to our data. You can download the model I trained from this [Dropbox link](https://www.dropbox.com/s/usolc4qls6wkni4/model_best.pth.tar?dl=0).  
##### Performance
###### Binary Attributes

<!-- |Fields  |Protest|Sign  |Photo|Fire |Law Enf.|Children|Group>20|Group>100|Flag |Night|Shout|
|--------|-------|------|-----|-----|--------|--------|--------|---------|-----|-----|-----|
|Accuracy|0.919  |0.890 |0.967|0.980|0.953   |0.970   |0.793   |0.803    |0.921|0.939|0.952|
|ROC AUC |0.970  |0.922 |0.811|0.985|0.939   |0.827   |0.818   |0.839    |0.828|0.940|0.849| -->

![][protest-roc]

[protest-roc]: https://github.com/wondonghyeon/protest-detection-violence-estimation/blob/master/files/protest.png

###### Violence
![](https://github.com/wondonghyeon/protest-detection-violence-estimation/blob/master/files/violence.png)

### Usage   
#### Training  

```bash
python train.py --data_dir UCLA-protest/ --batch_size 32 --lr 0.002 --print_freq 100 --epochs 100 --cuda
```

#### Evaluation

```bash
python pred.py --img_dir path/to/some/image/directory/ --output_csvpath result.csv --model model_best.pth.tar --cuda
```
