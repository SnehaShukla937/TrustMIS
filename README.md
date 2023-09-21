# *TrustMIS* (*Trust*worthy *M*edical *I*mage *S*egmentation)
## 1. Preface
* This repository provides an implementation of the paper [Trustworthy Medical Image Segmentation with improved performance for in-distribution samples](https://www.sciencedirect.com/science/article/pii/S0893608023003581#tbl2), published in [Neural Networks](https://www.sciencedirect.com/journal/neural-networks). 

* You can contact us at <shukla.sneha825@gmail.com> to resolve your queries regarding our paper and implementation. 

* If you find this repository helpful for your project or research, please cite this paper as [Citation](https://github.com/SnehaShukla937/TrustMIS/tree/main#4-citation).

## 2. Overview
### 2.1  Abstract:
Despite the enormous achievements of Deep Learning (DL) based models, their non-transparent nature led to restricted applicability and distrusted predictions. Such predictions emerge from erroneous In-Distribution (ID) and Out-Of-Distribution (OOD) samples, which results in disastrous effects in the medical domain, specifically in Medical Image Segmentation (MIS). To mitigate such effects, several existing works accomplish OOD sample detection; however, the trustworthiness issues from ID samples still require thorough investigation. To this end, a novel method, TrustMIS (Trustworthy Medical Image Segmentation) is proposed in this paper, which provides the trustworthiness and improved performance of ID samples for DL-based MIS models. TrustMIS works in three folds: IT (Investigating Trustworthiness), INT (Improving Non-Trustworthy prediction) and CSO (Classifier Switching Operation). Initially, the IT method investigates the trustworthiness of MIS by leveraging similar characteristics and consistency analysis of input and its variants. Subsequently, the INT method employs the IT method to improve the performance of the MIS model. It leverages the observation that an input providing erroneous segmentation can provide correct segmentation with rotated input. Eventually, the CSO method employs the INT method to scrutinise several MIS models and selects the model that delivers the most trustworthy prediction. The experiments conducted on publicly available datasets using well-known MIS models reveal that TrustMIS has successfully provided a trustworthiness measure, outperformed the existing methods, and improved the performance of state-of-the-art MIS models.
### 2.2  Flow Diagram :
![](https://ars.els-cdn.com/content/image/1-s2.0-S0893608023003581-gr1.jpg) <br>
Figure.1: Flow diagram of the proposed *IT* method to investigate the trustworthiness of Medical Image Segmentation predictions.<br>


![](https://ars.els-cdn.com/content/image/1-s2.0-S0893608023003581-gr3.jpg) <br>
Figure.2: Flow diagram of the proposed *INT* method to improve the performance of non-trustworthy Medical Image Segmentation predictions.<br>


![](https://ars.els-cdn.com/content/image/1-s2.0-S0893608023003581-gr4.jpg) <br>
Figure.3: Flow diagram of the proposed *CSO* method that selects the most trustworthy Medical Image Segmentation model.<br>
### 2.3  Qualitative Results:
![](https://ars.els-cdn.com/content/image/1-s2.0-S0893608023003581-gr5.jpg) <br>
Figure.4: Qualitative result of our proposed INT method, depicting success and failure case. <br>

## 3. Steps for implementation
### 3.1  IT (Investigating Trustworthiness) method:
1. Download the dataset from <https://github.com/DengPingFan/PraNet.git>.
2. Create input variants by rotating the dataset at 90, 180 and 270 degrees as given in `TrustMIS.ipynb`.
3. Clone the following repositories of various existing medical image segmentation models:
   * [PraNet](https://github.com/DengPingFan/PraNet)
   * [SSFormer](https://github.com/Qiming-Huang/ssformer)
   * [UACANet](https://github.com/plemeri/UACANet)
   * [CaraNet](https://github.com/AngeLouCN/CaraNet)
5. Download the pre-trained weights from the above-mentioned repositories.
6. Get predictions by applying the input and input variants dataset into these  above-mentioned medical image segmentation models.
7. Invert rotate the input variant predictions as given in `TrustMIS.ipynb`.
8. Run the final cell of `TrustMIS.ipynb` that computes the consistency (dice) between input predictions and inver-rotated input variant prediction. It investigates their trustworthiness and provides the confidence measure of each sample.
### 3.2  INT (Improving Non-Trustworthy prediction) method:
1. Following the [IT method](https://github.com/SnehaShukla937/TrustMIS/tree/main#31--it-investigating-trustworthiness-method) to investigate trustworthiness of each sample.
2. If the medical image segmentation prediction is found to be non-trustworthy, then compute the `YA` and `YB` masks as given in `TrustMIS.ipynb`
   (follow [paper]<https://www.sciencedirect.com/science/article/pii/S0893608023003581#tbl2> ).    
4. Run the final cell of `TrustMIS.ipynb` that provides the improved performance of medical image segmentation prediction (*c<sup>INT</sup>*).
### 3.3  CSO (Classifier Switching Operation) method:
1. Following the [INT method](https://github.com/SnehaShukla937/TrustMIS/tree/main#32--int-improving-non-trustworthy-prediction-method).
2. Run `TrustMIS.ipynb` that computes the dice metric between `YA` and `YB` for each sample prediction and stores it to `dice_cso`.
3. Repeat steps 1 and 2 for all the models (mentioned in [IT method](https://github.com/DengPingFan/PraNet)) and get the `dice_cso` for each dataset across all the models.
4. Among all the models, the most trustworthy model is selected based on the maximum dice for each sample and their final performance is considered from [INT method](https://github.com/SnehaShukla937/TrustMIS/tree/main#32--int-improving-non-trustworthy-prediction-method).
## 4. Citation
If you find this repository helpful for your project or research, please cite this paper as,
```
@article{shukla2023trustworthy,
  title={Trustworthy Medical Image Segmentation with improved performance for in-distribution samples},
  author={Shukla, Sneha and Birla, Lokendra and Gupta, Anup Kumar and Gupta, Puneet},
  journal={Neural Networks},
  volume={166},
  pages={127--136},
  year={2023},
  publisher={Elsevier}
}
```

## 5. Contact
For any query, kindly mail us at <shukla.sneha825@gmail.com>.

## 6. Reference
1. Fan, D. P., Ji, G. P., Zhou, T., Chen, G., Fu, H., Shen, J., & Shao, L. (2020). Pranet: Parallel reverse attention network for polyp segmentation. In Medical Image Computing and Computer Assisted Intervention–MICCAI 2020: 23rd International Conference, Lima, Peru, October 4–8, 2020, Proceedings, Part VI 23 (pp. 263-273). Springer International Publishing.
2. Wang, J., Huang, Q., Tang, F., Meng, J., Su, J., & Song, S. (2022, September). Stepwise feature fusion: Local guides global. In International Conference on Medical Image Computing and Computer-Assisted Intervention (pp. 110-120). Cham: Springer Nature Switzerland.
3. Kim, T., Lee, H., & Kim, D. (2021, October). Uacanet: Uncertainty augmented context attention for polyp segmentation. In Proceedings of the 29th ACM International Conference on Multimedia (pp. 2167-2175).
4. Lou, A., Guan, S., & Loew, M. (2023). Caranet: Context axial reverse attention network for segmentation of small medical objects. Journal of Medical Imaging, 10(1), 014005-014005.

