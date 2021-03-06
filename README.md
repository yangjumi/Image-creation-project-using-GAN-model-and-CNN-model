# Image creation project using GAN model and CNN model
GAN model(pix2pix), CNN model(autoencoder)을 활용하여 이미지채색화, 모네화풍으로 변환, 만화화풍으로 변환을 수행

## 1. Introduction
### Needs
GAN(Generative Adversarial Networks), 적대적 생성 신경망을 활용한 이미지 생성 및 변환 기술은 인공 신경망이 다양한 노이즈 입력을 받아 원하는 카테고리의 기존에 존재하지 않는 새로운 이미지를 생성해내거나 입력 이미지나 비디오를 다른 형태나 정보를 지닌 이미지 또는 비디오로 변환하는 기술로 최근 몇 년간 급속도로 발전하여 많은 관심을 받고 활발하게 연구되고 있는 분야이다. 최근에는 이미지 편집을 많이 활용하는 디자인 분야를 겨냥하여 이미지를 손쉽게 편집하거나 그릴 수 있는 프로그램으로 실제 서비스에 적용되고 있다. GAN은 기존의 딥러닝 기술에서 활용한 인공 신경망과는 다른 학습 방법을 활용하여 사람이 보기에 진짜와 구분하기 힘들 정도로 정교한 가짜 이미지를 만들어 내는 기술이다. 따라서 이미지 생성에 주목받는 GAN 모델 중 하나인 pix2pix를 활용하여 다양한 이미지를 생성해보고자 한다. 이와 대조하여 기존 인공신경망 모델인 autoencoder로써 다양한 이미지를 생성해봄으로써 두 모델 간의 성능을 비교해보고자 한다.

### Main contents
1) 흑백이미지 채색화
2) 원본이미지 모네화풍으로 변환
3) 원본이미지 만화화풍으로 변환  
▶ 본 프로젝트에서는 위의 총 3가지 스타일의 이미지들을 생성해보고자 한다. 3가지 스타일의 이미지를 생성하는 과정에서 pix2pix 및 autoencoder 모델을 활용하여 각각 생성해본 후, 모델 평가 지표인 MSE, PSNR, SSIM을 활용하여 성능을 비교해보고자 한다.

### Goals
#### 사용할 방법론 및 과정
pix2pix 및 autoencoder을 통해 이미지를 학습시킬 때, paired data가 필요하다. 해당 dataset은 kaggle을 통해 구했으며, 원본 이미지와 생성해내고 싶은 이미지를 동시에 학습시켜서 Predicted Image(결과이미지)를 생성해낸다. 이러한 과정을 통해 이미지 생성모델들을 비교 분석하고 이해하고자 한다.
#### 정량적 평가  
MSE, PSNR, SSIM 평가지표를 활용하여 모델 성능을 비교 분석한다. 우선적으로는 GAN 모델에 대한 성능이 높게 나올 것이라 가정하였다.
#### 정성적 평가  
실제 이미지와 결과 이미지에 대해 육안으로도 분석하여, 어떤 모델이 더 정교하게 결과 이미지를 도출해냈는지를 판단하고자 한다.
 
## 2. Analysis
### Prepare for analysis
▶ 모델 수립 : 사용할 GAN 모델 > pix2pix, 사용할 CNN 모델 > autoencoder  
▶ 모델 이미지 : 위 모델을 통해 이미지를 학습시키기 위해서는 원본 이미지와 결과 이미지가 함께 있는 paired image가 필요하다. 현재 사용하는 데이터는 kaggle로부터 다운받았다.

### Analysis plan
#### (1) pix2pix, autoencoder model study
우선 GAN 모델인 pix2pix를 이해하기 위해서 MNIST를 활용하여 그림 속에 숨겨진 숫자를 찾는 연습을 한다. 또한 GAN 모델을 활용하여 이미지 복원 및 채색을 진행한 논문들을 리뷰함으로써 적합한 GAN 모델을 선택하고, 학습한다. 기존 인공신경망 모델과의 성능비교를 위해, 기존 이미지 생성 모델들을 찾아보고 가장 적합한 모델을 선택한다. 현재는 autoencoder로 선택하였으며, 해당 모델 구조 등에 대해 이해한다.
#### (2) Data construction and model design
각 dataset에 맞는 모델을 구축한다. 특히 모델 결과가 최대한 잘 나올 수 있도록 generator, discriminator 등 layer을 설계하는 과정을 거친다.
#### (3) Image creation
구축한 모델을 활용하여 이미지를 생성해낸다. 먼저 kaggle의 데이터셋을 통해 모델을 학습시킨 후, 최종적으로 구현하고자 할 각 3가지 스타일에 대해 이미지를 생성한다.
#### (4) Experiment, performance improvement
정량적, 정성적 평가를 통해 이미지 채색화의 결과가 잘 나올 수 있도록 모델의 파라미터 및 구조를 바꿔가면서 모델을 학습시킨다.
  
## 3. Results
### Model structure
### (1) pix2pix
#### Generator 구조
Generator와 Discriminator로 나눠진 구조이다. Genrator 구조는 아래 그림과 같다. Generator는 Unet 구조를 따르며, 논문에 나온 generator 구조를 활용하여 오른쪽 그림처럼 generator을 구축하였다.  
![image01](https://user-images.githubusercontent.com/60904652/121556779-23fde100-ca4f-11eb-81da-b40a999c6a6e.png)  
![image02](https://user-images.githubusercontent.com/60904652/121556814-2a8c5880-ca4f-11eb-9784-3d81368a1dcb.png)  
▶ 인코더 부분  
입력값으로 필터는 몇 개를 사용할 것인지, 필터 사이즈는 몇인지, 배치 정규화는 할 것인지를 두고, 시퀀셜에 2d conv 레이어를 해당 사이즈에 맞게 생성해서 추가한다. stride는 2로, padding은 입력 데이터와 동일한 사이즈가 되도록 same으로 두었다. 활성화 함수로는 Leaky ReLU를 사용하였다. 필터수 3, 크기 4로 하여 만들고, 256x256 크기의 데이터를 넣어준 결과를 보면, 1/2 사이즈가 되어 128x128이 되고, 필터 개수인 3개가 생성되게 된다.  
▶ 디코더 부분  
Generator에서 실제로 데이터를 생성해내는 레이어 부분인 디코더를 만들었다. 디코더 부분은 인코딩된 데이터를 다시 복원하기 때문에, Conv2D의 역이라 할수있는 Conv2DTranspose, 즉 Transpose CNN 계층을 만들었다. 즉, 입력값은 거의 동일한데, 실제로 데이터가 2배로 커지도록 설정하였다. 배치 정규화는 각 레이어별로 꼭 들어가고, 활성화 함수로는 ReLU를 사용하였다. 디코더 부분에 필터수 3, 크기 4로 하여 넣어준 결과를 보면, 다운 샘플링에서 얻어낸 1x128x128x3의 데이터 크기가 2배가 되고, 그 필터값에 따라서 데이터가 생성됨을 볼 수 있다.  
▶ Generator 구축  
위 인코더와 디코더 레이어 생성 함수를 사용하고 통합하여 실제 제너레이터를 만들어내는 함수를 만들었다.  

#### Discriminator 구조
Discriminator의 구조는 아래와 같다.  
![image03](https://user-images.githubusercontent.com/60904652/121556823-2ceeb280-ca4f-11eb-8c40-119079aa026f.png)  
판별자는 PatchGAN을 사용하였다. Conv -> BatchNorm -> Leaky ReLU 구조를 사용했으며, 마지막 출력값은 batch_size, 30, 30, 1이고, 이는 입력 이미지의 70x70 범위를 판별한 값이다. 즉, 범위별로 참 거짓을 나누는 것으로, 이를 PatchGAN이라 한다. 입력을 원본 이미지와, 그에 대한 condition이미지 2개 받는다. 이를 concat하고, downsampling을 한다. 출력값이 32x32x256으로 내려가면, 따로 차원을 맞추기 위해, 좌우 상하로 0으로 패딩을 붙여서 34x34로 만들어준다. 그리고 Conv-> BatchNorm-> Leaky ReLU를 해주고, 다시 패딩을 입히고 conv연산을 해주어 최종적으로 30x30x1의 출력값이 나오도록 해주고, 이를 모델 객체로 만들어 반환한다.

#### 손실함수 생성
generator, discriminator 모델에 대한 판별자는 크로스 엔트로피를 사용한다. real 이미지에 대해선 1로 판단하고, gen 이미지에 대해선 0으로 판단하는 것을 기준으로 학습을 한다.

### (2) autoencoder
autoencoder은 encoder과 decoder로 이뤄졌다. bottleneck을 기준으로 output shape가 8*8, channel이 512까지 줄어들었다가 다시 원래 크기인 256*256, channel은 3으로 되돌아오는 구조로 이뤄졌다.  
![image04](https://user-images.githubusercontent.com/60904652/121556830-2eb87600-ca4f-11eb-91da-9cd3a1a61c07.png)
![image05](https://user-images.githubusercontent.com/60904652/121556840-30823980-ca4f-11eb-9d7c-0fb641d20117.png)  

### Analysis evaluation index
학습 결과에 대한 성능은 MSE, PSNR, SSIM을 이용하여 판단하였다. 해당 평가 지표에 대한 코드는 아래와 같이 구현하였다.  
![image06](https://user-images.githubusercontent.com/60904652/121556852-31b36680-ca4f-11eb-869d-039e4c3443e5.png)  
![image07](https://user-images.githubusercontent.com/60904652/121556863-3415c080-ca4f-11eb-9109-598710929433.png)  

### Train result
#### 1. 흑백이미지 채색화
:　pix2pix 결과 정리  
![image08](https://user-images.githubusercontent.com/60904652/121556868-35df8400-ca4f-11eb-98ce-3fb7a4bbb961.png)  
：autoencoder 결과 정리  
![image09](https://user-images.githubusercontent.com/60904652/121556877-3841de00-ca4f-11eb-9a58-2d6434370b55.png)  

#### 2. 원본이미지 모네화풍으로 변환
: pix2pix 결과 정리  
![image10](https://user-images.githubusercontent.com/60904652/121556884-3a0ba180-ca4f-11eb-9b6f-d08354442815.png)  
: autoencoder 결과 정리  
![image11](https://user-images.githubusercontent.com/60904652/121556892-3bd56500-ca4f-11eb-9fbb-cb8779c0900c.png)  

#### 3. 원본이미지 만화화풍으로 변환
: pix2pix 결과 정리  
![image12](https://user-images.githubusercontent.com/60904652/121556897-3d9f2880-ca4f-11eb-90ff-d0d2ec553bd1.png)  
: autoencoder 결과 정리  
![image13](https://user-images.githubusercontent.com/60904652/121556907-3f68ec00-ca4f-11eb-9082-5381e6d10348.png)  

### Total result
![image14](https://user-images.githubusercontent.com/60904652/121556910-4132af80-ca4f-11eb-9af2-1b2426eff59e.png)  
각 평가지표별 수치를 나타낸 것이다. 육안상으로도 pix2pix의 결과가 더 좋아보이는 것으로 보아 이미지 생성에 있어 GAN 모델인 pix2pix가 더 좋음을 확인할 수 있다.
 
## 4. Expected effect and Application plan
현재 이미지 생성에 많이 쓰이는 GAN 모델과 기존에 쓰였던 인공신경망 모델 두 가지를 통해 여러 가지의 이미지들을 생성해보고, 결과를 도출해보면서 GAN 모델의 우수성을 알 수 있었다. 이처럼 다양한 방식으로 이미지 생성을 할 수 있다면 디자인 분야에 많은 도움이 될 수 있다고 생각한다. 기존 디자이너들이 수작업으로 하던 일을 모델을 통해 손쉽게 할 수 있다는 점에서 높은 평가를 받을 수 있다고 생각한다.
 
## 5. Conclusions and Suggestions
두가지 모델을 통해 이미지 생성을 해본 후, 크게 2가지의 한계점이 도출되었다. 첫 번째로, 최종 결과물 사진의 화질을 더 좋게 만들 수 있는 방식에 대해 생각해보게 되었고, 두 번째로, 파라미터 수정을 통해 모델을 강화할 수 있는 방식에 대해 생각해보게 되었다. 현재의 모델 결과보다 더 좋은 방식으로 발전할 수 있는 방안에 대해 더 고안해보고 싶어졌다. 또한 처음 도전해보는 GAN 모델 구축인만큼 어려움이 많았지만, 모델 구조 뿐 아니라 인공지능(AI) 분야에 대해 깊게 이해할 수 있는 시간이 되어 유익한 프로젝트였다.
