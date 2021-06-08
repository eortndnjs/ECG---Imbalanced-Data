# ECG-Imbalanced-Data  

# How to run  
## 0. Prerequisite
+ Download mitbih_train.csv and mitbih_test.csv from [ECG Data](https://www.kaggle.com/shayanfazeli/heartbeat)  
+ Put csv files to 'Data' folder  

## 1. If possible, please use jupyter notebook to view the file (ECG_Classify.ipynb)  
+ I have coded with CoLab, since I don't have an access to any private GPU.

## 2. Choosing different augmentation methods
In 'Choose Augmentation' Secction, replace (X_augmented, Y_augmented) into (X_train, Y_train), (X_train_smote,  Y_train_smote), (X_train_ada, Y_train_ada)

   train_ds = MyDataset(Signal = pd.DataFrame(X_augmented), Label = pd.Series(Y_augmented))

## 3. Choose whether or not to use weight in criterion  
+ In 'Transiter' function, modify the variable 'weight' and choose between  


    criterion = nn.CrossEntropyLoss().to(device)
  
  
and


   criterion = nn.CrossEntropyLoss(weight = weight).to(device)
   




# Project Summary

## 0. Data Info
+ Input: 187 long time series 1-D data
+ Output: 5 different Arrhythmia Classes (N, S, V, F, Q)
+ Characteristic: Extremely imbalanced data  
   (For Train set, N, S, V, F, Q each 72470, 2223, 5788, 641, 6431)
+ Train/Validation Ratio: 3 to 1 (To generate general model)  
   
## 1. Network Info
+ LSTM : Advanced structure of RNN, which memorizes former information in the time series signal  (Sample Code from [LSTM](https://github.com/yunjey/pytorch-tutorial/blob/master/tutorials/02-intermediate/recurrent_neural_network/main.py#L39-L58))
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
  ![image](https://github.mit.edu/storage/user/13072/files/b67a6680-c83c-11eb-94c7-f45527095ea8)  

 + ^ Signal augmented with TSAug

## 3. My Trials  
+ A. Without Augmentation : For comparison
+ B. Without Augmentation, weight on cross entorpy loss : Compensate data imbalance by adjusting weight  
+ C-1. With SMOTE  
+ C-2. With ADASYN  
+ D. With Time Series Augmentation  

## 4. Results (Since Test Data is imbalanced, F1 score metric is used)
![image](https://github.mit.edu/storage/user/13072/files/f3555600-c85a-11eb-92b1-788502c03661)


