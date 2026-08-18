# A Novel Graph Neural Network for Zone-Level Urban-Scale Building Energy Use Estimation

This is the official implementation of our paper:
   
>  Halaçlı, E. G., Canlı, İ., İşeri, O. K., Yavuz, F., Akgül, Ç. M., Kalkan, S., & Dino, İ. G. (2023, November). A novel graph neural network for zone-level urban-scale building energy use estimation. In Proceedings of the 10th ACM International Conference on Systems for Energy-Efficient Buildings, Cities, and Transportation (pp. 169-176). 
  https://dl.acm.org/doi/10.1145/3600100.3623747

Upon detecting some errors in our code, we decided to rerun the experiments and update our results. Fortunately, this update in our results did not change the validity of our arguments in our paper.

## Setting the Environment and Datasets

The notebooks can be run in Google Colab or locally. ROOT variable should be changed according to the notebooks location. For running the notebooks within Colab run this line on top of the notebook:

```shell
from google.colab import drive
drive.mount('/content/drive')
```

The dataset can be found in the model_data folder. For descaling the results, scalers.pkl file can be used which is a scikit-learn scaler. Usage details can be found in the notebooks.

## Training the Model and Reproducing the Results


Training can be done in two ways:

- For training the models with preselected hyperparameters, call the ```train``` function with a ```Config```object filled with desired training configurations.

- Hyperparameter tuning is performed through Wandb. For running a hyperparameter search, call ```run_sweep``` after ```wandb.login()```.

For reproducing the results, model weights are provided in the models folder -- each model is named after its test set score. These models can be run with `reproduce_from_checkpoint` function provided in the bottom of their related notebooks. 

In addition to the experiments reported in the paper, we also trained the baseline GNN models with the normalization applied to GUBEM which is LayerNorm and L2 normalization applied in given order. Those results can be found in the table below with the "+Norms" suffix. Other GNN baselines have no normalization. Normalization is applied by default to GUBEM so we don't add the "+Norms" suffix. The ```no_norm``` parameter of `reproduce_from_checkpoint` function should be set according to the `+Norms` suffix.

## Updated Result Table (R2 & RMSE)
 
|            | Test           | Val             | Train          |
|------------|----------------|-----------------|----------------|
| GUBEM      | 0.9330 12.9940 | 0.9304 12.8032  | 0.9398 11.9580 |
| GAT        | 0.9298 13.2921 | 0.9279 13.0319  | 0.9462 11.3067 |
| GAT+Norms  | 0.9262 13.6327 | 0.9262 13.1828  | 0.9334 12.5815 |
| SAGE       | 0.9289 13.3815 | 0.9246 13.3243  | 0.9428 11.6571 |
| SAGE+Norms | 0.9258 13.6718 | 0.9266 13.1485  | 0.9417 11.7671 |
| GCN        | 0.7861 23.2111 | 0.7810 22.7066  | 0.7835 22.6805 |
| GCN+Norms  | 0.7863 23.2012 | 0.7795 22.7852  | 0.7903 22.3232 |
| MLP        | 0.9272 13.5377 | 0.9269 13.1217  | 0.9424 11.6998 |


# Citation

```
@inproceedings{halaccli2023novel,
  title={A novel graph neural network for zone-level urban-scale building energy use estimation},
  author={Hala{\c{c}}l{\i}, Eren G{\"o}kberk and Canl{\i}, {\.I}lkim and {\.I}{\c{s}}eri, Or{\c{c}}un Koral and Yavuz, Feyza and Akg{\"u}l, {\c{C}}a{\u{g}}la Meral and Kalkan, Sinan and Dino, {\.I}pek G{\"u}rsel},
  booktitle={Proceedings of the 10th ACM International Conference on Systems for Energy-Efficient Buildings, Cities, and Transportation},
  pages={169--176},
  year={2023}
}
```
