# ECG-Imbalanced-Data

## 0. Data Info
+ Input: 187 long time series 1-D data
+ Output: 5 different Arrhythmia Classes (N, S, V, F, Q)
+ Characteristic: Extremely imbalanced data  
   (For Train set, N, S, V, F, Q each 72470, 2223, 5788, 641, 6431)
+ Train/Validation Ratio: 3 to 1 (To generate general model)  
   
## 1. Network Info
+ LSTM : Advanced structure of RNN, which memorizes former information in the time series signal
+ Batch Size: 256 (As large as CoLab can handle)
+ Learning Rate : 1e-3 (Which shows fairly good performance in the case)  
+ Optimizer : Adam (Known as one of the best optimizers for RNN)  
+ Criterion : Cross Entropy Loss
+ More hyperparamter tuning can be done..

## 2. Data Augmentation
+ SMOTE, Adasyn: Creating new datas based on the K-nearest datas (Library from [Imblearn](https://imbalanced-learn.org/stable/install.html#getting-started))
+ Time Series Augmentation (TSAug): Classic time series augmentation (Library from [TS-Aug](https://tsaug.readthedocs.io/en/stable/)).  
   + Time Warp: Modify the speed of signal in certain random section  
   + Random Noise: Add random jitter to the signal  
   + Pool: Reduce the temporal resolution  
   + Drift: Change the slope of the signal  
      + This may change the characteristic of the signal

![image](https://github.mit.edu/storage/user/13072/files/21c33900-c83b-11eb-8b6e-7c5844fd7e5e) ![image](https://github.mit.edu/storage/user/13072/files/b67a6680-c83c-11eb-94c7-f45527095ea8)  

 + ^ Signal augmented with TSAug, with / without Drift

## 3. My Trials  
+ A. Without Augmentation : For comparison
+ B. Without Augmentation, weight on cross entorpy loss : Compensate data imbalance by adjusting weight  
+ C-1. With SMOTE  
+ C-2. With ADASYN  
+ D. With Time Series Augmentation  

## 4. Results (Since Test Data is imbalanced, F1 score metric is used)
![image](https://github.mit.edu/storage/user/13072/files/f3555600-c85a-11eb-92b1-788502c03661)


