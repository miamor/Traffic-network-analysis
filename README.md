# Detect botnet traffic flows with unsupervised learning  

## Data, model, result: 
<https://github.com/miamor/Traffic-network-analysis>


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
