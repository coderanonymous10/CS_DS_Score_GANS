# CS_DS_Score_GANS
There are five types of GAN mentioned:
1: AAE
2: conditional GAN
3: Deep convolutional GAN
4: WGAN
5: INFO GAN
===========================================================================================================
There are two types of evaluation done:
1: Classification score(CS)
	a: Direct_classification(C2)
	b: Indirect_classification(C3)
	c: Blind_classification(C4)
2: Distribution score(DS)
============================================================================================================
mnist_splitter_dataset:

This dataset contains randomly splitted mnist dataset
-------->mnist-splitter/stdash_dataloader
-------->mnist-splitter/svdash_dataloader

USE:
	use above data as a input to trainloader for GAN training
	"train_loader = torch.load('../input/mnist-splitter/stdash_dataloader')"
============================================================================================================
CNN C1 MODEL:
mnist_cnn_c1
-------> Above folder contains the pt file of the cnn_c1 model which will be use to predict the label of the images generated from GAN.

USE:
	use above data as a input to cnn_c1 model
	cnn_c1 = torch.load('../input/cnn-c1/cnn_c1(2).pt')
============================================================================================================

1: Classification score(CS):
Each gan is mentioned as MNIST_gan_name.ipynb

After running the above file with required dataset(mnist_splitter and cnn_c1)
each gan will generated the images as dataloader and save as well and (FID,IS,PSNR,MMD) will be calculated and print on screen for below epochs:
"checkpoint = [1,10,20,30,40,50,100,150,200]"
==================================================================================================================
A: Direct_classification(C2):
to calulate the direct classification values for each epochs we need to run the file mnist-cnn-c2_direct_classification.ipynb
use this "train_loader = torch.load('../input/mnist-splitter/stdash_dataloader')" to train the convolutional neural network
and use "dcgan_loader = torch.load('../input/conditional-gan/gan_data_epoch_EPOCH')" where EPOCH=[1,10,20,30,40,50,100,150,200] to test and get the result

==================================================================================================================

B: Indirect_classification(C3):
to calulate the indirect classification values for each epochs we need to run the file mnist-cnn-c3_indirect_classification.ipynb
use this "cgan_data = torch.load('../input/conditional-gan/gan_data_epoch_EPOCH')" where EPOCH=[1,10,20,30,40,50,100,150,200] to train the convolutional neural network
and use "testloader = torch.load('../input/mnist-splitter/svdash_dataloader')" to test and get the result

==================================================================================================================

C: Blind_classification(C4):
to calulate the blind classification values for each epochs we need to run the file mnist-cnn-c4_blind_classification.ipynb
use this "testloader = torch.load('../input/mnist-splitter/svdash_dataloader')" to train the convolutional neural network
and use "cgan_data = torch.load('../input/conditional-gan/gan_data_epoch_EPOCH')" where EPOCH=[1,10,20,30,40,50,100,150,200]  to test and get the result

==================================================================================================================
Datset "mnist_distribution_score_loader" : this datset contains below distribution
class: Number_of_images
0: 	5000
1: 	5000
2: 	5000
3: 	5000
4: 	5000
5: 	3000
6: 	3000
7: 	3000
8: 	3000
9: 	3000

1: Distribution score(CS):
RUN each GAN mentioned as distribution_score_GAN_NAME.ipynb
and use "mnist_distribution_score_loader" as input to these gans and then images will be saved as dataloader for each mentioned epochs. 
EPOCH=[1,10,20,30,40,50,100,150,200]

Now use distribution-score-of-gans.xpynb to calculate the distribution scores of gans and use 
to load gan genereted images.
" gan_loader= torch.load('../input/wgan-implementation/gan_data_epoch_1',map_location = torch.device('cpu'))" 
to load custom filtered images from "mnist_distribution_score_loader" 
"train_loader= torch.load('../input/mnist_distribution_score_loader',map_location = torch.device('cpu'))" 

:::change the input to gan_loader to calculate the distribution scores of each gan

