# Kaggle Data Science Bowl 2018 튜토리얼

머신러닝에서 수 많은 framework들이 존재합니다.

몇개월간 어떤 framework을 사용해서 어떤 식으로 data를 변환하고 data pipe-line을 구축해야하는지 정말 고민을 많이 하다가 찾아낸 방법으로 코드를 변경해서 구현을 해보았습니다.

## 참고 사이트(Kaggle)
 * https://www.kaggle.com/keegil/keras-u-net-starter-lb-0-277

## Data Science Bowl 2018이란?
Data Science Bowl 2018은 다양한 세포 이미지들에서 핵을 찾는 competition입니다.<br>
제공된 Data는 각 train dataset에선 2D 이미지(png)로 각 id별로 RGB 형태인 이미지와, mask가 그려진 label image data가 존재합니다.<br>
또한 test data는 mask이미지는 없이 RGB 형태의 이미지만 존재합니다.<br>

우리는 이 데이터들을 U-Net 알고리즘을 사용해서 Image Segmentation에 맞게 train을 시켜주고 label data가 없는 test data로 잘 mask가 씌어지는지 확인할 것 입니다.<br>

> &nbsp;&nbsp;&nbsp; 이 튜토리얼에서는 제공된 CSV파일에 적혀져 있는 mask pixel 값을 참고 안하고 오직 mask된 image로만 label로 참고를 하게 됩니다.<br> 
> &nbsp;&nbsp;&nbsp;하지만 이 방법 말고 csv파일을 mask를 그리는 경우는 해당 링크를 참고해주시기 바랍니다. <br>
> &nbsp;&nbsp;&nbsp;https://www.kaggle.com/kmader/nuclei-overview-to-submission


#### Training data
Training data는 각 Id 폴더 안에 세포 핵 들의 Image와 Mask가 폴더 안에 각각 존재합니다.
- train Image : 670
- train Mask : 670

#### Test data
Test data는 Id 폴더 안에 세포 핵 들의 Image가 폴더 내부에 존재합니다.
- Test Image :65

#### Validation data
Training data에서 "train_test_split"를 통해서 .1의 비율로 분할을 해주었습니다.

#### 데이터셋 구조

```
|-- stage1_train
      |-- bowlfile_id # 각각 폴더별로 ID
            |-- images  
                  |-- bowl_id.png

            |-- mask # bowl ID
                  |-- bowl_id_mask1.png
                  |-- bowl_id_mask2.png
                  |-- bowl_id_mask3.png
                  ...
             ...
|-- stage1_test
      |-- bowlfile_id
            |-- images # 질의 이미지 폴더
                  |-- bowl_id.png
            ...
```
