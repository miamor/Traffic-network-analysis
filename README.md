# Detect botnet traffic flows with unsupervised learning  

<https://github.com/miamor/Traffic-network-analysis>  

Navigate to this [drive link](https://drive.google.com/drive/folders/1UEFAo7bS0zTSOc5F28CId7jWGASZNDPM?usp=sharing) to download all data, models and result.   


## Result
### iForest on 7 sets of features
| iForest |	Exp01 |	Exp02 |	Exp03 |	Exp04 |	Exp05 |	Exp06 |	Exp07 |
--- | --- | --- | --- | --- | --- | --- | --- | 
| Training time |	27.7s |	27.4s |	46.4s |	36.2s |	42.6s |	31.9s |	31.1s |
| Testing time |	9.46s |	10.1s |	16.2s |	10.6s |	11.6s |	9.8s |	9.16s |
| Recall (class 1) |	9.28 |	15.43 |	59.32 |	**65.02** |	58.95 |	51.99 |	53.58 |
| Precision (class 1) |	2.90 |	5.31 |	14.17 |	**17.36** |	15.48 |	14.55 |	15.87 |
| f1 (class 0) |	99.22 |	99.30 |	99.22 |	99.33 |	99.29 |	99.31 |	99.35 |
| f1 (class 1) |	4.42 |	7.90 |	22.88 |	27.40 |	24.53 |	22.74 |	24.49 |
| AUC |	54.04 |	57.18 |	78.96 |	**81.91** |	78.85 |	75.40 |	76.24 |
| Accuracy	98.45 |	98.61 |	98.45 |	98.67 |	98.59 |	98.63 |	98.72 |

### With post-processing technique
| thresh_p |	thresh_score |	Precision (class 1) |	Recall (class 1) |	f1 (class 0) |	f1 (class 1) |	Accuracy |	AUC |
--- | --- | --- | --- | --- | --- | --- | --- | 
| - |	- |	17.36 |	65.02 |	99.33 |	27.40 |	98.67 |	81.91 |
| 2 |	-0.44918331 |	13.51 |	69.75 |	99.07 |	22.64 |	98.15 |	**84.01** |
| 1 |	-0.47863293 |	24.05 |	62.09 |	99.54 |	34.67 |	99.09 |	80.66 |
| 0.5 |	-0.53062718 |	46.27 |	59.72 |	99.79 |	52.14 |	99.58 |	79.73 |
| 0.45 |	-0.54221799 |	51.24 |	59.52 |	99.81 |	55.07 |	99.62 |	79.65 |
| 0.4 |	-0.55450336 |	56.98 |	58.85 |	99.83 |	57.90 |	99.67 |	79.34 |

### More results on `Report.pdf` and `vv5.iforest.__1__.ipynb` and `vv5.lof.__1__.ipynb`.

## Folder description
`vv1` : Generate features  
`vv2` : Feature analysis  
`vv3` : Encode  
`vv4` : Test & evaluate on validation set  
`vv5` : Experiment algorithms on 7 sets of features  
`vv6` : Evaluate and analyse scores, threshold. Analyse detection result  


| Filename | Description | Input file | Output file | Variables to be modified |
|---|---|---|---|---|
| `vv1-1.ft_gen.__train__.ipynb` | Generate features for train set. <br>One-hot encode some fields. Save values to be one-hot to txt files. | Original train csv <br>*Eg:* `data/tr.csv` | csv file with generated features <br>*Format:* `data/{set}.vv1.csv` <br>*Eg:* `data/tr.vv1.csv` | `dt` |
| `vv1-2.ft_gen.__testval__.ipynb` | Generate features for test / validation set. <br>One-hot encode some fields. Use values from saved txt files. | Original train csv <br>*Eg:* `data/t.csv` | csv file with generated features <br>*Format:* `data/{set}.vv1.csv` <br>*Eg:* `data/t.vv1.csv` | `dt` |
| `vv2-1.ft_sel_1.ipynb` | Features analysis with statistical | validation csv with generated features <br>*Eg:* `data/v.vv1.csv` |  |  |
| `vv2-1.ft_sel_2.ipynb` | Features selection with methods reported by Miller (UniMelb) in KDD challenge | validation csv with generated features <br>*Eg:* `data/v.vv1.csv` |  |  |
| `vv2-1.ft_sel_3.ipynb` | Features selection with MI | validation csv with generated features <br>*Eg:* `data/v.vv1.csv` |  |  |
| `vv2-1.ft_sel_4.ipynb` | Features selection with StepForward | validation csv with generated features <br>*Eg:* `data/v.vv1.csv` |  |  |
| `vv3.enc.__1__.ipynb` | Encode | csv with generated features <br>*Eg:* `data/vv1.tr.csv` | Encoded files <br>*Format:*<br>`data/vv3.{set}.{type}.__1__.npy` <br>*Eg:*<br>`data/vv3.tr.X.__1__.npy`,<br>`data/vv3.t.y.__1__.npy`,<br>`...` |  |
| `vv4.iforest.__1__.ipynb`<br>`vv4.lof.__1__.ipynb`<br>`...` | Test and evaluate on validation set | csv with generated features <br>*Eg:* `data/vv1.tr.csv` |  |  |
| `vv5.iforest.__1__.ipynb` | Run `iForest` on 7 sets of features | Encoded files <br>*Format:* `data/vv3.{set}.{type}.__1__.npy` <br>*Eg:* `data/vv3.tr.X.__1__.npy` | Model, features used, X used, ... <br>*Format:*<br>`result/vv5.__1__.{model_name}.{expname}.__{ra}__.{outtype}.{ext}` <br>*Eg:*<br>`result/vv5.__1__.iforest.exp04_play.__81.91__.model.pkl`,<br>`result/vv5.__1__.iforest.exp04_play.__81.91__.data.t.X.npy`,<br>`...` |  |
| `vv5.lof.__1__.ipynb` | Run `LOF` as `novelty detection` on 7 sets of features | Encoded files <br>*Format:* `data/vv3.{set}.{type}.__1__.npy` <br>*Eg:* `data/vv3.tr.X.__1__.npy` | Model, features used, X used, ... <br>*Format:*<br>`result/vv5.__1__.{model_name}.{expname}.__{ra}__.{outtype}.{ext}` <br>*Eg:*<br>`result/vv5.__1__.lof.exp05_mi1.__78.40__.model.pkl`,<br>`result/vv5.__1__.lof.exp05_mi1.__78.40__.data.t.X.npy`,<br>`...` |  |
| `vv5.lof.__1__.testonly.ipynb` | Run `LOF` as `outlier detection` on 7 sets of features | Encoded files <br>*Format:* `data/vv3.{set}.{type}.__1__.npy` <br>*Eg:* `data/vv3.tr.X.__1__.npy` | Model, features used, X used, ... <br>*Format:*<br>`result/vv5.__1__.{model_name}.{expname}.__{ra}__.{outtype}.{ext}` <br>*Eg:*<br>`result/vv5.__1__.lof.exp05_mi1.__78.40__.model.pkl`,<br>`result/vv5.__1__.lof.exp05_mi1.__78.40__.data.t.X.npy`,<br>`...` |  |
| `vv6.after_predict.iforest.ipynb` | Evaluate `iForest` model and analyse scores & threshold... | Output of `vv5.iforest.__1__.ipynb` |  | `expname = 'exp04_play'`<br>`ra = '81.91'`<br>`model_name = 'iforest'` |
| `vv6.after_predict.lof.ipynb` | Evaluate `LOF` model and analyse scores & threshold... | Output of `vv5.lof.__1__.ipynb` or `vv5.lof.__1__.testonly.ipynb` |  | `expname = 'exp05_mi1'`<br>`ra = '78.40'`<br>`model_name = 'lof'` |


## Citation
`vv2-1.ft_sel_2.ipynb` is heavily referenced from [this repo](https://github.com/solegalli/feature-selection-for-machine-learning), which is the implementation of  
```
@inproceedings{miller2009predicting,
  title={Predicting customer behaviour: The University of Melbourne’s KDD Cup report},
  author={Miller, Hugh and Clarke, Sandy and Lane, Stephen and Lonie, Andrew and Lazaridis, David and Petrovski, Slave and Jones, Owen},
  booktitle={KDD-Cup 2009 Competition},
  pages={45--55},
  year={2009},
  organization={PMLR}
}
```